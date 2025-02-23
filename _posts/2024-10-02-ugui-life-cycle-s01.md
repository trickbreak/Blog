---
title: "부록. UGUI 라이프사이클 응용 사례"
date: 2024-10-02 00:00:00 +/-TTTT
categories: [Main, Unity]
tags: [Unity]
toc: true
---

## 가이드

[UGUI 라이프사이클](../ugui-life-cycle) 의 선행 학습이 필요합니다.

---

## 시나리오

UI 팝업이 있으며, **LayoutGroup** 및 **ContentSizeFitter**를 사용하여 팝업 내부의 컨텐츠 크기에 맞춰 자동으로 크기가 조정됩니다.

### 문제점

- 컨텐츠 크기가 너무 크면 팝업이 화면을 벗어나는 문제가 발생함.
- 일정 크기 이상이면 스크롤 뷰(ScrollView)를 활성화하고, 팝업 크기를 화면에 맞게 조정해야 함.

---

## 레이아웃에서 계산한 컨텐츠의 크기를 확인하는 방법

Unity의 UGUI는 프레임 내에서 특정 시점에 **레이아웃을 자동으로 계산**합니다.  
따라서 컨텐츠의 크기를 정확히 알기 위해 **레이아웃이 모두 계산된 후** 값을 확인해야 합니다.

### 일반적인 방법

`WaitForEndOfFrame`을 사용하여 **현재 프레임이 끝날 때까지 기다리면** 정확한 크기를 얻을 수 있습니다.

```c#
IEnumerator WaitAndCheckSize()
{
    yield return new WaitForEndOfFrame();
    Debug.Log("컨텐츠 크기: " + content.sizeDelta);
}
```

### 문제점 

- `WaitForEndOfFrame`에서 content의 크기를 조정해야 하다면 **현재 프레임이 아니라 다음 프레임에서 반영됨.** (이전 단계에서 이미 렌더링에 필요한 계산이 끝났기 때문에) 
- 현재 시나리오에서는 컨텐츠의 사이즈가 화면을 넘어가면 다시 크기를 재조정 해야함.

---

## 레이아웃을 강제로 자동 계산

```c#
LayoutRebuilder.ForceRebuildLayoutImmediate(rectTransform);
```

ForceRebuildLayoutImmediate를 이용하면 해당 rectTransform의 크기를 강제로 다시 계산 할 수 있습니다.

### 문제점

- ForceRebuildLayoutImmediate는 자기 자신만 다시 계산을 하는 방식
- 부모나 자식의 크기나 위치에 영향을 받아 크기가 달라지는 경우에는 먼저 부모나 자식의 크기와 위치를 먼저 다시 계산해야 함.
- 구조가 간단한 경우 순차적으로 계산해 줄 수 있지만 구조가 복잡한 경우 영향을 받는 요소를 모두 찾아 순차적으로 크기를 다시 계산 하기는 쉽지 않음.

---

## Canvas.willRenderCanvases 이벤트 사용

해당 시나리오 같은 상황에서 추천하는 방식은 Canvas.willRenderCanvases 이벤트를 사용하는 방법 입니다.

Canvas.willRenderCanvases 이벤트는 레이아웃 계산은 끝났고, 렌더링에 필요한 부분은 계산하기 전 상태이기 때문에 계산이 끝난 레이아웃의 크기를 구하고, 컨텐츠의 사이즈를 강제한뒤 현재 프레임에서 다시 그릴 수 있습니다.

### 예시 코드

```c#

private void OpenPopup(ContentInfo contentInfo)
{
	// contentInfo에 정보를 기반으로 팝업 내부에 content에 요소를 추가 합니다.
	...
	
	// 팝업이 열리고 willRenderCanvases 타이밍에 SetContentSize를 실행 합니다.
	Canvas.willRenderCanvases += SetContentSize;
}

private void SetContentSize()
{
	// willRenderCanvases에서 제거해 주지 않으면 매 프레임 호출 됩니다.
	Canvas.willRenderCanvases -= SetContentSize;
	
	// willRenderCanvases 타이밍에 실행되었기 때문에 
	// 레이아웃 계산이 끝난 content.sizeDelta의 크기를 알 수 있습니다.
	if (content.sizeDelta.y > MaxHeight)
	{
		SetScrollMode();
	}
	else
	{
		SetNotScrollMode();
	}



	void SetScrollMode()
	{
		if (!scrollRect.vertical)  
		{
			// 스크롤 지원을 위한 수정
			...

			// 비 스크롤 모드 -> 스크롤 모드로 변경되었기 때문에 UI요소를 다시 그립니다.
			Canvas.ForceUpdateCanvases();
		}
	}

	void SetNotScrollMode()
	{
		if (scrollRect.vertical)  
		{
			// 비 스크롤 지원을 위한 수정
			...

			// 스크롤 모드 -> 비 스크롤 모드로 변경되었기 때문에 UI요소를 다시 그립니다.
			Canvas.ForceUpdateCanvases();
		}
	}
}

```

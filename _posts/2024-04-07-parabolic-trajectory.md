---
title: "포물선 궤적 계산"
date: 2024-04-07 00:00:00 +/-TTTT
categories: [Main]
tags: [GameMath]
toc: true
math: true
---

> 샘플 코드는 Unity6 LTS 버전에서 작성 되었습니다.
{: .prompt-info }

## 시나리오

방향과 힘을 지정하면 포물선을 그리며 날아가는 미사일이 있다고 가정해 봅시다. 플레이어는 미사일 발사를 위해 방향과 힘을 조절하지만, 난이도가 높다는 피드백이 있어 발사 전에 미사일이 어디로 날아갈지 가이드 라인을 보여주려고 합니다. 이를 위해 미리 포물선 궤적을 계산해야 합니다.

## 무중력 상황에서의 미사일 진행

먼저 중력이 없는 상황을 고려해 보겠습니다. 중력이 없다면 미사일은 지정한 방향으로만 날아갑니다. 시간에 따른 위치는 아래와 같이 계산할 수 있습니다.

$$ 위치 = 진행방향 \times 힘 \times 시간$$

```c#
private Vector3 GetMissilePosition(Vector direction, float power, float time)
{
	Vector3 startPosition = transform.position;

	// 진행방향 X 힘 X 시간
	Vector3 movePosition = direction * power * time;
	
	return startPosition + movePosition;
}
```

time이 0이면 startPosition에 미사일이 위치하고, 시간이 지날 수록 미사일은 direction 방향으로 이동하게 됩니다.

## 중력이 적용된 경우의 진행

이제 중력이 작용하는 상황을 고려해 보겠습니다. 중력 때문에 미사일은 직선이 아닌 포물선 경로를 따르게 됩니다. 중력에 의한 낙하 거리는 아래 공식으로 계산됩니다.

$$
거리 = 0.5 \times g(중력) \times t^2(시간)
$$

```c#
private Vector3 GetMissilePosition(Vector direction, float power, float time)
{
	Vector3 startPosition = transform.position;

	// 진행방향 X 힘 X 시간
	Vector3 movePosition = direction * power * time;

	// 중력가속도로 인해 감소되는 거리
	Vector3 fallPosition = 0.5f * -Physics.gravity * Mathf.Pow(time, 2);

	return startPosition + movePosition - fallPosition;
}
```

- `movePosition` 중력을 무시하고 힘과 방향에 의해 미사일이 이동한 거리입니다.
- `fallPosition` 은 중력에 의해 미사일이 이동한 거리입니다.
- `-Physics.gravity` 를 사용한 이유는 유니티에서 위에서 아래로 중력을 나타낼 때 -값으로 나타내기 때문에 이를 반전 시키기 위해 `Physics.gravity` 값에 -1을 곱해주었습니다.

이 두 값을 조합하여, 미사일이 실제로 날아갈 포물선 궤적을 정확하게 예측할 수 있습니다.

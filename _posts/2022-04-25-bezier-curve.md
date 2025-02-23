---
title: "베지에 곡선"
date: 2022-04-25 00:00:00 +/-TTTT
categories: [Main]
tags: [GameMath]
toc: true
math: true
---

## 베지에 곡선이란?

베지에 곡선은 **최소 2개 이상의 제어점** 을 사용하여 만들어지는 곡선입니다.  
제어점의 개수에 따라 곡선의 차수가 결정되며, 일반적으로는 다음과 같이 표현할 수 있습니다.

- **2개의 제어점:** 1차 베지에 곡선
- **3개의 제어점:** 2차 베지에 곡선
- **4개의 제어점:** 3차 베지에 곡선
- **...**
- **n개의 제어점:** (n-1)차 베지에 곡선

이러한 곡선들은 **이항정리(Binomial Theorem)** 를 기반으로 정의할 수 있습니다.  
즉,

$$
((1-t) + t)^n
$$

여기서 $t$ 는 0과 1 사이의 값을 가지며, $t = 0$ 일 때 시작 제어점, $t = 1$ 일 때 종료 제어점에 해당합니다.

---

## 3차 베지어 곡선

많은 그래픽 프로그램에서는 **시작점, 종료점, 시작 컨트롤 점, 종료 컨트롤 점** 총 4개의 제어점을 사용하여 곡선을 표현합니다.  

다음 그림은 3차 베지에 곡선의 제어점 구성을 보여줍니다.

![그림](https://i.namu.wiki/i/rAQw_pmOVaYJakNr24vb3wZGREyak9koc7tCF_4gg202Rq4Q5gSCN4QNe2Fbtd6r2xxFpdO8C59Rdm0pRX_RfR3XiWicQ-QcHPsQQvWNrdTEJM-jgJdQWLSdLqxVchzEiWy-rSOyleu85czCSq--tg.webp)

4개의 제어점을 사용하기 때문에 이것을 **3차 베지에 곡선**이라고 부릅니다.

### 수학적 유도

3차 베지에 곡선은 $n = 3$ 인 경우의 이항정리를 이용하여 다음과 같이 전개할 수 있습니다.

우선,

$$
\begin{align}

& ((1 - t) + t)^3
\\
\\
& ((1 - t) + t)((1 - t) + t)((1 - t) + t)
\\
\\
& (1 - t)^3 + 3(1-t)^2t + 3(1-t)t^2 + t^3

\end{align}
$$

여기서 각 항에 해당하는 계수를 제어점에 곱해주면,

$$
\begin{align}

& (1 - t)^3 + 3(1-t)^2t + 3(1-t)t^2 + t^3

\\
\\

& (1 - t)^3P_0 + 3(1-t)^2tP_1 + 3(1-t)t^2P_2 + t^3P_3

\end{align}	
$$

	- $P_0$ : 시작점
	- $P_1$ : 시작 컨트롤 점
	- $P_2$ : 종료 컨트롤 점
	- $P_3$ : 종료점

이 공식을 사용하면 $t$ 의 값(0 ~ 1)에 따라 베지에 곡선 상의 점을 계산할 수 있습니다.

### 코드 구현 예제 (C#)

아래는 위의 3차 베지에 곡선 공식을 C# 코드로 구현한 예제입니다.

```c#
public class BezierCurve
{
	public static Vector2 Calculate2D(Vector2 start, Vector2 start_control, Vector2 end, Vector2 end_control, float t_value)
	{
		float t = Mathf.Clamp (t_value, 0.0f, 1.0f);
		float tt = t * t;
		float ttt = tt * t;

		float u = 1.0f - t;
		float uu = u * u;
		float uuu = uu * u;

		Vector2 p = uuu * start;
		p += 3 * uu * t * start_control;
		p += 3 * u * tt * end_control;
		p += ttt * end;

		return p;
	}
}
```

이 함수는 매개변수 t_value (0 ~ 1)를 입력받아 해당 위치의 베지에 곡선상의 좌표를 계산해 줍니다.

---

이와 같이 베지에 곡선은 제어점과 t 값의 조합을 통해 부드러운 곡선을 생성할 수 있으며, 특히 3차 베지에 곡선은 다양한 그래픽 애플리케이션에서 널리 사용됩니다.

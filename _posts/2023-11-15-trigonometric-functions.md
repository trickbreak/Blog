---
title: "삼각함수"
date: 2023-11-15 00:00:00 +/-TTTT
categories: [Main]
tags: [GameMath]
toc: true
math: true
---

## 가이드

- 함수에 대한 이해가 필요 합니다. [함수](../function) 글을 참조 하세요.
- 일반적으로 삼각함수의 입력값인 각도값은 라디안을 사용 합니다. 해당 글에서는 이해를 돕기위해 디그리 방식으로 설명했습니다. 라디안에 대한 내용은 [각도를 표현하는 단위 라디안(radian)](../radian) 글을 참조 하세요.

---

## 삼각함수

삼각함수라는 이름에서 알 수 있듯이 함수입니다.

그렇다면 어떤 입력값과 출력값을 가지는 함수일까요?

바로 직각 삼각형에서 **입력값으로는 각도(빗변과 밑변의 사이각)** 를 **출력값으로는 삼각비** 를 나타내는 함수를 삼각함수라고 합니다.

삼각비라니 생소한 단어가 나왔습니다. 차근차근 알아봅시다.

우선 직각삼각형을 봅시다.

![trigonometric_function_01.png](https://1drv.ms/i/c/faa1d6b4af8fb38d/IQQmvrwo21kKQKOMEAoKfBDUASyXZQom6egej1LqQqfOGO8?width=720&height=640)

직각삼각형의 구성으로 **빗변**, **밑변**, **높이** 그리고 빗변과 밑변의 **각도** 이렇게 4개의 구성요소가 있습니다. (삼각함수에서는 빗변과 밑변의 각도가 기준입니다.)

삼각비란 3개의 선분 중 임이의 2개의 선분에 대한 비율을 의미합니다.

예를 들어 **각도**(입력값)를 넣어서 **높이 / 빗변**(출력값) 이 출력된다면 이 함수는 sin함수입니다.

이렇게 어떤 선분의 삼각비가 출력되는지에 따라서 

sin(사인)함수, cos(코사인)함수, tan(탄젠트)함수 3가지 종류의 삼각함수가 있습니다.

![trigonometric_function_02.png](https://1drv.ms/i/c/faa1d6b4af8fb38d/IQRY3McIx3JJRoVGEt9KSGYYAQheg_Yxg7jFo1J27N6QL3I?width=720&height=640)

---

## sin 함수

먼저 sin함수부터 봅시다.  

$$
sin(각도) = 높이 / 빗변
$$
  
이미 한번 설명한 것과 같이 sin함수는 **각도**(입력값)에 따른 직각 삼각형의 3선분 (높이, 밑변, 빗변)중 2개의 선분(**높이와 빗변**)간의 비율을 나타내는 함수입니다.

우선 단위원을 그리고 그 위에 직각 삼각형을 그려 봅시다.

![trigonometric_function_03.png](https://1drv.ms/i/c/faa1d6b4af8fb38d/IQS3sPaHeuFOR7-w0o9Vq7odASgxaknxQh3Gkizqs7hlMSg?width=720&height=640)

$$
sin(\theta) = 높이 / 빗변
$$
  
빗변은 단위원이기 때문에 1 입니다.

$$
\begin{align}
sin(\theta) & = 높이 / 1
\\
sin(\theta) & = 높이
\end{align}
$$
  
그렇기 때문에 각도가 0도이면 높이도 0이 됩니다.

반대로 각도가 90도가 되면 빗변과 높이가 같아지기 때문에 높이가 1이 됩니다. 

즉 사인함수는 0도에서 90도로 입력값이 변화할 때 출력값이 0에서 1로 변화하는 것을 알 수 있습니다.

그럼 각도가 0도에서 360도 한 바퀴 돌게 될 때 출력값은
  
0도 => 0
90도 => 1
180도 => 0
270도 => -1
360도 => 0

와같은 변화를 보입니다.

조금 더 직관적인 이해를 돕기 위해서 아래 영상을 참조하세요.

<iframe src="https://1drv.ms/v/c/faa1d6b4af8fb38d/IQTKl92SRednSY62lbuzkuVpAU3U2Mrxi91p1tdtwY0Buss" width="640" height="360" frameborder="0" scrolling="no" allowfullscreen></iframe>

각도가 1바퀴 돌때 사인함수의 출력값(높이)이 -1 ~ 1을 왔다 갔다 하는 것을 알 수 있습니다.  

이 출력값을 그래프로 그려보면

<iframe src="https://1drv.ms/v/c/faa1d6b4af8fb38d/IQSRc-ROp6DFTb1RRuiW8BTZAQ6-mw2-gviZVRaks-qUMR0" width="840" height="360" frameborder="0" scrolling="no" allowfullscreen></iframe>

바로 사인 그래프가 완성됩니다.

사인 그래프가 있다면 언제든지 각도에 따른 (높이 / 빗변)의 값을 알아낼 수 있습니다.  
  
이것이 sin함수입니다.

---

## cos 함수

코사인함수는 사인함수와 비슷합니다.

사인함수와 마찬가지로 출력값인 삼각비의 분모로 **빗변**을 사용하기 때문에

단위원에서 cos(θ) 의 값은 **밑변**과 같습니다.

$$
\begin{align}
cos(\theta) & = 밑변 / 빗변
\\
cos(\theta) & = 밑변 / 1
\\
cos(\theta) & = 밑변
\end{align}
$$

때문에 각도가 0도이면 밑변의 길이는 1이 됩니다.  
  
그리고 각도가 90도가 된다면 밑변의 길이는 0이 될 것 입니다.  
  
그럼 각도가 0도에서 360도 한 바퀴 돌게 될 때 출력값은  
  
0도 => 1  
90도 => 0  
180도 => -1  
270도 => 0  
360도 => 1  
  
와 같은 변화를 보입니다.

각도의 변화에 따른 밑변의 길이가 어떻게 변하는지 확인해 보세요.

<iframe src="https://1drv.ms/v/c/faa1d6b4af8fb38d/IQTMEqoLsrRwTbBZptd2ypK4AQRODH2x_0VpXv-aqtDtoi4" width="640" height="360" frameborder="0" scrolling="no" allowfullscreen></iframe>

변화하는 각도와 밑변의 관계를 그래프로 그리면 아래와 같습니다.

<iframe src="https://1drv.ms/v/c/faa1d6b4af8fb38d/IQR3LS0swHJITqgmRNhzb52lAUqYY_TnCrd7X6nt1ZYd3Hk" width="360" height="840" frameborder="0" scrolling="no" allowfullscreen></iframe>

이 그래프를 사인그래프와 같은 공간에 그려보면 시작점이 다를 뿐 같은 파형을 가지는 것을 알 수 있습니다.

<iframe src="https://1drv.ms/v/c/faa1d6b4af8fb38d/IQSBzYN2xdlTSprVG3xSX3qPAUXXHjPO-IIAcxdTwwqgmW8" width="840" height="360" frameborder="0" scrolling="no" allowfullscreen></iframe>

---

## tan 함수

탄젠트함수는 기존에 공부한 사인, 코사인 함수와는 조금 다릅니다.

빗변을 1로 고정한 직각삼각형을 그려도 탄젠트함수에서 출력하는 삼각비는 빗변을 사용하지 않기 때문입니다.

이번엔 조금 다른 방식으로 단위 원에 직각삼각형을 그려 보겠습니다. 바로 밑변을 1로 고정한 직각삼각형입니다.

![trigonometric_function_09.png](https://1drv.ms/i/c/faa1d6b4af8fb38d/IQT9G58uoQY1SLuHis9LVc9qAUmLCsXqPsDMlNGH9ijui7Q?width=720&height=640)

그러면 이 상태로 각도를 한 바퀴 돌려보겠습니다.

<iframe src="https://1drv.ms/v/c/faa1d6b4af8fb38d/IQR3K2evl4ElRJq1jKdpf4kjAU_eEjpC4s0INE0DR87W2R8" width="640" height="360" frameborder="0" scrolling="no" allowfullscreen></iframe>

사인, 코사인 함수와는 무언가 다른 움직임을 보이는 것 같습니다.

각도가 90도를 넘어갔을 때를 보면 사인, 코사인 그래프를 그리기 위해 그렸던 직각삼각형과 방식이 다름을 볼 수 있습니다.

밑변을 1로 고정했기 때문에 삼각형은 항상 중심을 기준으로 우측으로 그려 지게 됩니다.

원점을 기준으로 좌측에 직각 삼각형을 그리게 되면 밑변의 길이가 -1의 값을 가지기 때문에 에러 입니다.

그러면 밑변을 1로 고정했으니까 식을 정리해 봅시다.

$$
\begin{align}
tan(\theta) & = 높이 / 밑변
\\
tan(\theta) & = 높이 / 1
\\
tan(\theta) & = 높이
\end{align}
$$

이제 우리가 그린 직각삼각형의 높이 값으로 그래프를 그리면 완성입니다.

<iframe src="https://1drv.ms/v/c/faa1d6b4af8fb38d/IQR9uJsige1fR441n25G-RahAfYpdJ4n8EhjgUlWf73DCHw" width="640" height="360" frameborder="0" scrolling="no" allowfullscreen></iframe>

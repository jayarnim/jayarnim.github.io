---
order: 3
title: Optimizer
date: 2024-01-21
categories: [Machine Learning Techs, Deep Learning]
tags: [Deep Learning, Optimization]
math: true
description: >-
  Based on the lecture “Intro. to Deep Learning (2023-2)” by Prof. Seong Man An, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
  path: /_post_refer_img/DeepLearning/Thumbnail.jpg
---

## What? Gadient Descent
-----

![01](/_post_refer_img/DeepLearning/03-01.png){: width="100%"}

- **정의** : 손실 함수의 도함수(경사)를 최소화하는 가중치를 추정하는 방법

    $$
    \hat{\beta}=\{\beta\,|\, \min_{\beta} \displaystyle\frac{\partial}{\partial \beta} \text{Loss}(\beta, \cdots) \}
    $$

- **최적 가중치 추정 방법**

    $$
    \beta_t
    = \beta_{t-1} - \alpha \times \displaystyle\frac{\partial}{\partial \beta_{n-1}}\text{Loss}(\beta_{t-1},\cdots)
    $$

    - $\text{Loss}(\beta,\cdots)$ : 손실 함수
    - $t$ : 극소점 탐색 횟수
    - $\alpha$ : 학습률
    - $\beta$ : 가중치

## Example: three-layer model
-----

![02](/_post_refer_img/DeepLearning/03-02.png){: width="100%"}

### 순전파 연산 과정

- **손실 $e$ 를 다음과 같이 정의하자**

    $$\begin{aligned}
    e
    &= \text{Loss}(\hat{y})\\
    &= \hat{y} - y
    \end{aligned}$$

    - $\hat{y}$ : 예측값
    - $y$ : 실제값

- **$n$ 개의 계층으로 구성된 모델의 예측값 $\hat{y}$ 은 다음과 같음**

    $$
    \hat{y}
    = f_{n} \circ g_{n} \circ f_{n-1} \circ g_{n-1} \circ \cdots \circ f_{1} \circ g_{1}(x)
    $$

    - $x$ : 입력값

    - $f_{i}(x)$ : $i$ 번째 계층의 활성화 함수

    - $g_{i}(x)=w_{i} \cdot x + b_{i}$ : $i$ 번째 계층의 순입력 함수
        - $w_{i}$ : $i$ 번째 계층의 가중치
        - $b_{i}$ : $i$ 번째 계층의 편향으로서 편의상 $0$ 이라고 가정함

- **$3$ 개의 계층으로 구성된 모델의 손실 $e$ 를 다음과 같이 서술할 수 있음**

    $$\begin{aligned}
    e
    &= h_{3} - y\\
    &= f_{3}(z_{3}) - y\\
    &= f_{3}(g_{3}(h_{2})) - y\\
    &= f_{3}(w_{3} \cdot h_{2}) - y\\
    &= f_{3}(w_{3} \cdot f_{2}(z_{2})) - y\\
    &= f_{3}(w_{3} \cdot f_{2}(g_{2}(h_{1}))) - y\\
    &= f_{3}(w_{3} \cdot f_{2}(w_{2} \cdot h_{1})) - y\\
    &= f_{3}(w_{3} \cdot f_{2}(w_{2} \cdot f_{1}(z_{1}))) - y\\
    &= f_{3}(w_{3} \cdot f_{2}(w_{2} \cdot f_{1}(g_{1}(h_{0})))) - y\\
    &= f_{3}(w_{3} \cdot f_{2}(w_{2} \cdot f_{1}(w_{1} \cdot h_{0}))) - y
    \end{aligned}$$

    - $z_{i}=g_{i}(h_{i-1})$ : $i$ 번째 계층의 순입력 함수 값
    - $h_{i}=f_{i}(z_{i})$ : $i$ 번째 계층의 활성화 함수 값
    - $h_{0} = x$ : 입력값

### 역전파 학습 과정

- **손실 $e$ 를 $1$ 번째 계층 가중치 $w_{1}$ 에 대하여 미분하면 다음과 같음**

    $$\begin{aligned}
    \frac{\partial e}{\partial w_{1}}
    &= \frac{\partial e}{\partial\not{h_{3}}}
    \cdot \frac{\partial\not{h_{3}}}{\partial\not{z_{3}}}
    \cdot \frac{\partial\not{z_{3}}}{\partial\not{h_{2}}}
    \cdot \frac{\partial\not{h_{2}}}{\partial\not{z_{2}}}
    \cdot \frac{\partial\not{z_{2}}}{\partial\not{h_{1}}}
    \cdot \frac{\partial\not{h_{1}}}{\partial\not{z_{1}}}
    \cdot \frac{\partial\not{z_{1}}}{\partial w_{1}}
    \end{aligned}$$

- **위 수식의 각 항목을 다음과 같이 일반화할 수 있음**

    $$\begin{aligned}
    \frac{\partial e}{\partial h_{n}}
    &= \frac{\partial(h_{n}-y)}{\partial h_{n}}\\
    &= 1\\\\
    \frac{\partial h_{i}}{\partial z_{i}}
    &= \frac{\partial f_{i}(z_{i})}{\partial z_{i}}\\
    &= f^{\prime}_{i}(z_{i})\\\\
    \frac{\partial z_{i}}{\partial h_{i-1}}
    &= \frac{\partial g_{i}(h_{i-1})}{\partial h_{i-1}}\\
    &= \frac{\partial (w_{i} \cdot h_{i-1})}{\partial h_{i-1}}\\
    &= w_{i}\\\\
    \frac{\partial z_{i}}{\partial w_{i}}
    &= \frac{\partial g_{i}(h_{i-1})}{\partial w_{i}}\\
    &= \frac{\partial (w_{i} \cdot h_{i-1})}{\partial w_{i}}\\
    &= h_{i-1}
    \end{aligned}$$

- **손실 $e$ 를 $k$ 번째 계층 가중치 $w_{k}$ 에 대하여 미분한 값을 다음과 같이 일반화할 수 있음**

    $$\begin{aligned}
    \frac{\partial e}{\partial w_{k}}
    &= h_{k-1} \times (w_{n} \cdot w_{n-1} \cdots w_{k+1}) \times \{f^{\prime}_{n}(z_{n}) \cdot f^{\prime}_{n-1}(z_{n-1}) \cdots f^{\prime}_{k}(z_{k})\}\\
    &= h_{k-1} \times \displaystyle\prod^{n}_{i=k+1}{w_i} \times \displaystyle\prod^{n}_{i=k}{f^{\prime}_{i}(z_{i})}
    \end{aligned}$$

    - $h_{k-1}$ : $k-1$ 번째 계층 출력값이자 $k$ 번째 계층 입력값
    - $\displaystyle\prod^{n}_{i=k+1}{w_i}$ : 출력층에서부터 $k+1$ 번째 계층까지 가중치 곱
    - $$\displaystyle\prod^{n}_{i=k}{f^{\prime}_{i}(z_{i})}$$ : 출력층에서부터 $k$ 번째 계층까지 활성화 함수 값 곱

- **경사하강법에 의해 갱신된 $k$ 번째 계층의 가중치 $(w_{k})_{new}$ 는 다음과 같음**

    $$\begin{aligned}
    (w_{k})_{new}
    &= w_{k} - \eta \times \frac{\partial e}{\partial w_{k}}\\
    &= w_{k} - \eta \times h_{k-1} \displaystyle\prod^{n}_{i=k+1}{w_i} \cdot \displaystyle\prod^{n}_{i=k}{f^{\prime}_{i}(z_{i})}
    \end{aligned}$$

## 종류
-----

![03](/_post_refer_img/DeepLearning/03-03.png){: width="100%"}

### 경사하강법 각 항목의 의미

$$
w_{t}
=w_{t-1} - \eta \times \frac{\partial e_{t-1}}{\partial w_{t-1}}
$$

- $\eta$ : 학습률(Learning Rate)로서 **갱신 크기**

    ![04](/_post_refer_img/DeepLearning/03-04.png){: width="100%"}

- $\displaystyle\frac{\partial e_{t-1}}{\partial w_{t-1}}$ : 가중치에 대한 손실의 변화율 벡터로서 **갱신 방향**

### 갱신 크기 중심

![05](/_post_refer_img/DeepLearning/03-05.png){: width="100%"}

- `Adagrad` : **갱신 크기**를 결정함에 있어 이전까지 갱신 규모를 반영함

    $$\begin{aligned}
    w_{t}
    &= w_{t-1} - \frac{\eta}{\sqrt{h_{t}}} \times \frac{\partial e_{t-1}}{\partial w_{t-1}}\\
    h_{t}
    &= h_{t-1} + \frac{\partial e_{t}}{\partial w_{t}} \odot \frac{\partial e_{t}}{\partial w_{t}}
    \end{aligned}$$

    - $h_{t-1}$ : 이전까지 갱신 규모

    - $\displaystyle\frac{\partial e_{t}}{\partial w_{t}} \odot \displaystyle\frac{\partial e_{t}}{\partial w_{t}}$ : 현 시점 갱신 규모 추정치

- `RMSProp` : **갱신 크기**를 결정함에 있어 이전까지 갱신 규모를 지수가중이동평균하여 반영함

    $$\begin{aligned}
    w_{t}
    &= w_{t-1} - \frac{\eta}{\sqrt{h_{t}}} \times \frac{\partial e_{t-1}}{\partial w_{t-1}}\\
    h_{t}
    &= \rho \cdot h_{t-1} + (1 - \rho) \cdot \frac{\partial e_{t}}{\partial w_{t}} \odot \frac{\partial e_{t}}{\partial w_{t}}
    \end{aligned}$$

    - $\rho$ : 붕괴 계수

### 갱신 방향 중심

![06](/_post_refer_img/DeepLearning/03-06.png){: width="100%"}

- **`Momentum`** : **갱신 방향**을 결정함에 있어 $m_{t-1}$ 을 $\gamma$ 만큼 반영함

    $$\begin{aligned}
    w_{t}
    &= w_{t-1} - m_{t}\\
    m_{t}
    &= \eta \cdot \frac{\partial e_{t-1}}{\partial w_{t-1}} + \gamma \cdot m_{t-1}
    \end{aligned}$$

    - $m_{t-1}$ : 직전 시점 갱신 방향
    - $\gamma$ : 관성 계수
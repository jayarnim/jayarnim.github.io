---
order: 2
title: Differentiation
date: 2023-07-08
categories: [Mathematical Techs, Calculus]
tags: [Mathematics]
math: true
description: >-
  Based on the lecture “Mathematics for Artificial Intelligence (2022-1)” by Prof. Yeo Jin Chung, Dept. of AI, Big Data & Management, College of Business Administration, Kookmin Univ.
image:
  path: /_post_refer_img/Calculus/Thumbnail.jpg
---

## What? Differentiation
-----

- **미분(Differentiation)**
    - 설명변수 $x$ 에 대한 반응변수 $y$ 의 순간변화율
    - 설명변수 $x$ 가 $\Delta x$ 만큼 변화할 때 $y$ 는 얼마만큼 변화하는가

- **평균변화율의 이해**

    ![01](/_post_refer_img/Calculus/02-01.jpg){: width="100%"}

    - 설명변수 $x \in X$ 에 대한 반응변수 $y \in Y$ 의 함수 $f:\,X\rightarrow Y$ 에 대하여
    - 다음을 구간 $[x,a]$ 에서 $x$ 에 대한 $y$ 의 평균변화율이라고 정의함

        $$\begin{aligned}
        \displaystyle\frac{\Delta y}{\Delta x}
        &=\displaystyle\frac{f(x)-f(a)}{x-a}\\
        &=\displaystyle\frac{f(x +\Delta x)-f(x)}{\Delta x}
        \end{aligned}$$

- **순간변화율의 이해**

    $$\begin{aligned}
    \displaystyle\frac{d y}{d x}
    &=\lim_{x \rightarrow a}\displaystyle\frac{f(x)-f(a)}{x-a}\\
    &=\lim_{\Delta x \rightarrow 0}\displaystyle\frac{f(x + \Delta x)-f(x)}{\Delta x}
    \end{aligned}$$

    - $x \rightarrow a$ 일 때 구간 $[x,a]$ 에서 $x$ 에 대한 $y$ 의 평균변화율
    - $\Delta x \rightarrow 0$ 일 때 $x$ 에 대한 $y$ 의 평균변화율
    - 즉, $x$ 의 변화폭이 0에 한없이 가까워질 때 $y$ 의 변화폭

- **미분 가능하다는 말의 의미**
    - 설명변수 $x \in X$ 에 대한 반응변수 $y \in Y$ 의 함수 $f:\,X\rightarrow Y$ 에 대하여
    - $x=a$ 에서 순간변화율 값이 존재하면 $f$ 는 $x=a$ 에서 미분 가능하다고 말함
    - 모든 정의역에 대하여 미분 가능하다면 $f$ 는 $x$ 에 대하여 미분 가능하다고 말함

- **성질**
    - $x$ 에 대하여 미분 가능한 함수 $f(x), g(x)$ 와 상수 $\alpha$ 에 대하여 다음이 성립함

        - $\displaystyle\frac{d}{dx}\alpha=0$
        - $\displaystyle\frac{d}{dx}(\alpha \times f(x)) = \alpha \times (\displaystyle\frac{d}{dx}f(x))$
        - $\displaystyle\frac{d}{dx}x^n=n \times x^{n-1}$
        - $\displaystyle\frac{d}{dx}(f(x)\pm g(x))=\displaystyle\frac{d}{dx}f(x) \pm \frac{d}{dx}g(x)$
        - $\displaystyle\frac{d}{dx}(f(x)\times g(x))=(\displaystyle\frac{d}{dx}f(x))\times g(x) + f(x) \times (\displaystyle\frac{d}{dx}g(x))$
        - $\displaystyle\frac{d}{dx}\displaystyle\frac{f(x)}{g(x)}=\big( (\displaystyle\frac{d}{dx}f(x))\times g(x) - f(x) \times (\displaystyle\frac{d}{dx}g(x)) \big) \times \displaystyle\frac{1}{(g(x))^2}$

### 합성함수의 미분법

- **연쇄법칙(Chain Rule)**
    - $y=f(u)$ 가 $u$ 에 대하여 미분 가능하고, $u=g(x)$ 가 $x$ 에 대하여 미분 가능한 경우 다음이 성립함

        $$\begin{aligned}
        \displaystyle\frac{dy}{dx}
        &=\displaystyle\frac{dy}{du}\times \displaystyle\frac{du}{dx} \\
        &=\displaystyle\frac{d}{du}f(u) \times \displaystyle\frac{d}{dx}g(x)
        \end{aligned}$$

- **예시**
    - $y=(3x+2)^5$

        $$\begin{aligned}
        y&=u^5,\\
        u&=3x+2 \\\\
        \therefore \displaystyle\frac{dy}{dx}
        &=\frac{d}{du}u^5 \times \displaystyle\frac{d}{dx}(3x+2) \\
        &=5u^4 \times 3 \\
        &=15(3x+2)^4
        \end{aligned}$$

## 자연로그의 밑의 미분법
-----

### 자연로그의 밑의 이해

![02](/_post_refer_img/Calculus/02-02.svg){: width="100%"}

- **자연로그함수의 정의** : 기호 $e$ 로 표기되는 특정 상수를 밑으로 하는 로그함수

    $$\begin{aligned}
    f(x)
    &=\log_e x \\
    &=\ln x\\
    &=\displaystyle\int_{1}^{x}\displaystyle\frac{1}{t}dt
    \end{aligned}$$

- **자연로그의 밑의 정의** : 자연로그함수 $f(x)$ 에 대하여 $f(x)=1$ 을 만족하는 양의 실수 $x$

    $$\begin{aligned}
    f(x)
    &=\displaystyle\int_{1}^{x}\displaystyle\frac{1}{t}dt \\
    &=\log_{e} x \\
    &=1 \\\\
    \Leftrightarrow x
    &=e \\
    &=\lim_{n \rightarrow \infty} (1+\displaystyle\frac{1}{n})^n \\
    &=2.71828\cdots,\;n\in R
    \end{aligned}$$

### 자연로그의 밑의 미분법

- **자연로그함수의 미분법**

    $$\begin{aligned}
    \displaystyle\frac{d}{dx}\ln x
    &=\displaystyle\frac{d}{dx}\displaystyle\int_{t=1}^{x}\displaystyle\frac{1}{t}dt \\
    &=\displaystyle\frac{1}{x}
    \end{aligned}$$

- **자연로그의 밑에 대한 지수함수의 미분법**

    $$\begin{aligned}
    f(x)
    &=e^x\\\\
    \displaystyle\frac{d}{dx}f(x)
    &=\displaystyle\frac{d}{dx}e^x \\
    &=e^x
    \end{aligned}$$

    - **증명**
        - 함수 정의

            $$
            f(x)=a^x
            $$

        - 미분 정의

            $$\begin{aligned}
            \displaystyle\frac{d}{dx}f(x)
            &=\lim_{\Delta x \rightarrow 0}\displaystyle\frac{f(x+\Delta x) - f(x)}{\Delta x}\\
            &=\lim_{\Delta x \rightarrow 0}\displaystyle\frac{a^{x+\Delta x} - a^{x}}{\Delta x} \\
            &=\lim_{\Delta x \rightarrow 0}\displaystyle\frac{a^{x}(a^{\Delta x} - 1)}{\Delta x} \\
            &=a^{x}
            \end{aligned}$$

        - 극한의 성질에 근거하여 좌변에서 $a^x$ 소거

            $$\begin{aligned}
            \lim_{\Delta x \rightarrow 0}a^x \times \lim_{\Delta x \rightarrow 0}\displaystyle\frac{a^{\Delta x} - 1}{\Delta x}
            &=a^x \\
            \displaystyle\frac{1}{a^x}\times a^x \times \lim_{\Delta x \rightarrow 0}\displaystyle\frac{a^{\Delta x} - 1}{\Delta x}
            &= a^x \times \displaystyle\frac{1}{a^x}\\
            \lim_{\Delta x \rightarrow 0}\displaystyle\frac{a^{\Delta x} - 1}{\Delta x}
            &= 1
            \end{aligned}$$

        - 극한의 성질에 근거하여 좌변에서 $\displaystyle\lim_{\Delta x \rightarrow 0}\displaystyle\frac{1}{\Delta x}$ 소거

            $$\begin{aligned}
            \displaystyle\frac{\displaystyle\lim_{\Delta x \rightarrow 0}(a^{\Delta x}-1)}{\displaystyle\lim_{\Delta x \rightarrow 0}\Delta x}
            &= 1 \\
            \displaystyle\lim_{\Delta x \rightarrow 0}\Delta x \times \frac{\displaystyle\lim_{\Delta x \rightarrow 0}(a^{\Delta x}-1)}{\displaystyle\lim_{\Delta x \rightarrow 0}\Delta x}
            &= 1 \times \displaystyle\lim_{\Delta x \rightarrow 0}\Delta x \\
            \displaystyle\lim_{\Delta x \rightarrow 0}(a^{\Delta x}-1)
            &=\displaystyle\lim_{\Delta x \rightarrow 0}\Delta x
            \end{aligned}$$

        - 극한의 성질에 근거하여 좌변에서 $1$ 소거

            $$\begin{aligned}
            \displaystyle\lim_{\Delta x \rightarrow 0}a^{\Delta x}-\displaystyle\lim_{\Delta x \rightarrow 0}1
            &=\displaystyle\lim_{\Delta x \rightarrow 0}\Delta x \\
            \displaystyle\lim_{\Delta x \rightarrow 0}a^{\Delta x}-\displaystyle\lim_{\Delta x \rightarrow 0}1 + \displaystyle\lim_{\Delta x \rightarrow 0}1
            &= \displaystyle\lim_{\Delta x \rightarrow 0}1 + \displaystyle\lim_{\Delta x \rightarrow 0}\Delta x \\
            \displaystyle\lim_{\Delta x \rightarrow 0}a^{\Delta x}
            &=\displaystyle\lim_{\Delta x \rightarrow 0}(1+\Delta x)
            \end{aligned}$$

        - 극한의 성질에 근거하여 양변에 $\displaystyle\frac{1}{\Delta x}$ 제곱
            
            $$\begin{aligned}
            \displaystyle\lim_{\Delta x \rightarrow 0}a^{\Delta x}
            &=\displaystyle\lim_{\Delta x \rightarrow 0}(1+\Delta x) \\
            \displaystyle\lim_{\Delta x \rightarrow 0}(a^{\Delta x})^{\frac{1}{\Delta x}}
            &=\displaystyle\lim_{\Delta x \rightarrow 0}(1+\Delta x)^{\frac{1}{\Delta x}} \\
            a
            &=\displaystyle\lim_{\Delta x \rightarrow 0}(1+\Delta x)^{\displaystyle\frac{1}{\Delta x}}
            \end{aligned}$$

        - $\Delta x$ 를 $\displaystyle\frac{1}{n}$ 로 치환

            $$\begin{aligned}
            a
            &=\displaystyle\lim_{n \rightarrow \infty}(1+\displaystyle\frac{1}{n})^n \\
            &=e
            \end{aligned}$$

## 삼각함수의 미분법
-----

### 삼각함수의 이해

- **각도에 대한 대변, 빗변, 이웃변 정의**

    ![03](/_post_refer_img/Calculus/02-03.png){: width="100%"}

    - **대변(Homologous Side)** : 각 $A$ 와 마주보는 변 $a$
    - **이웃변(Adjoint Side)** : 각 $A$ 와 이웃하는 변 $b$
    - **빗변(Hypotenuse)** : 직각 $C$ 와 마주보는 변 $c$

- **삼각함수(Trigonometric Function)** : 각도에 대한 삼각비의 함수
    - **삼각비(Trigonometric Ratio)** : 직각삼각형 두 변의 비율
    - **사인 함수(Sine Function; $\sin$)** : 각 $\theta$ 에 대하여 그 빗변 대비 대변의 비율

        $$
        \sin \theta = \frac{a}{c}
        $$

    - **코사인 함수(Cosine Function; $\cos$)** : 각 $\theta$ 에 대하여 그 빗변 대비 이웃변의 비율

        $$
        \cos \theta = \frac{b}{c}
        $$

    - **탄젠트 함수(Tangent Function; $\tan$)** : 각 $\theta$ 에 대하여 그 이웃변 대비 대변의 비율

        $$\begin{aligned}
        \tan \theta &= \frac{a}{b} \\
        &= \frac{\sin \theta}{\cos \theta}
        \end{aligned}$$

### 삼각함수의 미분법

- **사인 함수의 미분**

    $$
    \frac{d}{dx}\sin x=\cos x
    $$

- **코사인 함수의 미분**

    $$
    \frac{d}{dx}\cos x=-\sin x
    $$

- **탄젠트 함수의 미분**
    
    $$
    \frac{d}{dx}\tan x=\frac{1}{\cos^2 x}
    $$
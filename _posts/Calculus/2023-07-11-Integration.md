---
order: 5
title: Integration
date: 2023-07-11
categories: [Math, Calculus]
tags: [Math]
math: true
description: >-
  Based on the lecture “Mathematics for Artificial Intelligence (2022-1)” by Prof. Yeo Jin Chung, Dept. of AI, Big Data & Management, College of Business Administration, Kookmin Univ.
image:
  path: /_post_refer_img/Calculus/Thumbnail.jpg
---

## 적분의 이해
-----

### 적분(Integration)

- **정의** : 매우 작은 양을 쌓아가는 방법

    ![01](/_post_refer_img/Calculus/05-01.jpeg){: width="100%"}

- **미분과의 관계**
    - **미분**

        $$
        f(x)
        = F(x) \times \displaystyle\frac{1}{\Delta x}
        $$

        - $F(x)$ 의 $x$ 에 대한 순간변화율 $f(x)$ 를 구하는 방법
        - $F(x)$ 를 $\Delta x$ 로 잘게 쪼개는 방법

    - **적분**

        $$
        F(x) + C
        = \displaystyle\sum{[f(x) \times \Delta x]}
        $$

        - $x$ 축과 피적분함수 $f(x)$ 로 둘러싸인 면적의 너비 $F(x)+C$ 를 구하는 방법
        - 미분소($f(x) \times \Delta x$)를 쌓아가는 방법

### 부정적분(Indefinite Integral)

- **정의** : 어떤 함수 $f(x)$ 를 도함수로 하는 모든 함수 $F(x)+C$ 를 구하는 연산

    $$
    F(x) + C = \int{f(x)dx}
    $$

    - $f(x)$ : $F(x)+C$ 의 피적분함수, 도함수 혹은 미분계수
    - $F(x)+C$ : $f(X)$ 의 부정적분함수
    - $C$ : 적분상수

- **성질**
    - $\displaystyle\int{\alpha \cdot f(x)dx} = \alpha \cdot \displaystyle\int{f(x)dx}$
    - $\displaystyle\int{[f(x) \pm g(x)] dx} = \displaystyle\int{f(x)dx} \pm \displaystyle\int{g(x)dx}$
    - $\displaystyle\int{x^n dx} = \displaystyle\frac{x^{n+1}}{n+1} + C$
    - $\displaystyle\int{\frac{1}{x}dx} = \ln{\vert x \vert}+C$
    - $\displaystyle\int{e^{x}dx} = e^{x}+C$
    - $\displaystyle\int{\frac{f^{\prime}(x)}{f(x)}dx} = \ln{\vert f(x) \vert}+C$
    - $\displaystyle\int{\sin{x}dx} = -\cos{x}+C$
    - $\displaystyle\int{\cos{x}dx} = \sin{x}+C$

### 정적분(Definite Integral)

- **정의** : $x \in [a,b]$ 과 피적분함수 $f(x)$ 로 둘러싸인 면적의 너비를 구하는 연산

    $$\begin{aligned}
    S
    &= \int_{a}^{b}{f(x)dx} \\
    &= F(b) - F(a)
    \end{aligned}$$

    - $a$ : 적분의 아래 한계
    - $b$ : 적분의 위의 한계

- **성질**
    - $\displaystyle\frac{d}{dx}\displaystyle\int_{a}^{x}{f(t)dt} = f(x)$
    - $\displaystyle\int_{a}^{b}{\alpha f(x)dx} = \alpha \displaystyle\int_{a}^{b}{f(x)dx}$
    - $\displaystyle\int_{a}^{b}{f(x) \pm g(x)dx} = \displaystyle\int_{a}^{b}{f(x)dx} \pm \displaystyle\int_{a}^{b}{g(x)dx}$
    - $\displaystyle\int_{a}^{a}{\alpha f(x)dx} = 0$
    - $\displaystyle\int_{a}^{b}{\alpha f(x)dx} = -\displaystyle\int_{b}^{a}{\alpha f(x)dx}$
    - $\displaystyle\int_{a}^{b}{\alpha f(x)dx} + \displaystyle\int_{b}^{c}{\alpha f(x)dx} = \displaystyle\int_{a}^{c}{\alpha f(x)dx}\,(a<b<c)$

### 중적분(Multiple Integral)

- **정의** : 영역 $B$ 에서 적분 가능한 다변수함수 $y=f(x_1,x_2,\cdots,x_n)$ 에 대하여 변수 $x_1,x_2,\cdots,x_n$ 에 대한 정적분

    $$\begin{aligned}
    \int_{x_n} \cdots \int_{x_2} \int_{x_1} f(x_1,x_2,\cdots,x_n) dx_1 dx_2 \cdots dx_n
    \end{aligned}$$

- **이중적분(Double Integral)의 예시**
    - 영역 $B$ 를 다음과 같이 정의하자

        $$\begin{aligned}
        B
        &= [a,b]\times[c,d]\\
        &= \{(x,y)|a \leq x \leq b, c \leq y \leq d\}
        \end{aligned}$$

    - 2변수함수 $z=f(x,y)$ 는 영역 $B$ 에서 적분 가능한 함수임

        $$\begin{aligned}
        \lim_{x \rightarrow k-}f(x,y)=\lim_{x \rightarrow k+}f(x,y)=f(k,y)\;(a \leq k \leq b)\\
        \lim_{y \rightarrow k-}f(x,y)=\lim_{y \rightarrow k+}f(x,y)=f(x,k)\;(c \leq k \leq d)\\
        \end{aligned}$$

    - 피적분함수 $z=f(x,y)$ 를 영역 $B$ 에서 $y$ 에 대하여 적분하면 다음과 같음

        $$\begin{aligned}
        g(x)
        &= \int_{c}^{d}{z}dy\\
        &= \int_{c}^{d}{f(x,y)}dy\\
        &= F(x,d)-F(x,c)
        \end{aligned}$$

    - $x$ 에 관한 함수 $g(x)$ 를 영역 $B$ 에서 $x$ 에 대하여 적분하면 다음과 같음

        $$\begin{aligned}
        \int_{a}^{b}{g(x)}dx
        &= G(b) - G(a)
        \end{aligned}$$

    - 이상을 요약하면 다음과 같음

        $$\begin{aligned}
        \int_{a}^{b}(\int_{c}^{d}{z}dy)dx
        &= \int_{a}^{b}\int_{c}^{d}{f(x,y)}dy\,dx
        \end{aligned}$$

## 특수한 경우의 적분법
-----

### 부분적분 : 곱셈의 적분법

- $x$ 에 대하여 미분 가능한 함수 $u(x),v(x)$ 의 곱을 $x$ 에 대하여 미분하면 다음과 같음

    $$\begin{aligned}
    \frac{d}{dx}uv
    &= u\frac{dv}{dx} + v\frac{du}{dx}
    \end{aligned}$$

- 양변에 $dx$ 를 곱하면 다음과 같음

    $$\begin{aligned}
    d(uv)
    &= u \cdot dv + v \cdot du
    \end{aligned}$$

- 양변의 일부 항목을 이항하면 다음과 같음

    $$\begin{aligned}
    u \cdot dv
    &= d(uv) - v \cdot du
    \end{aligned}$$

- 양변을 적분하면 다음과 같음

    $$\begin{aligned}
    \int{u \cdot dv}
    &= uv - \int{v \cdot du}
    \end{aligned}$$

### 유리함수의 적분법

- 진분수함수 $\displaystyle\frac{f(x)}{g(x)}$ 를 다음과 같이 가정하자

    $$\begin{aligned}
    \frac{f(x)}{g(x)}
    &= \frac{x^3 - x^2 - 2}{x(x-1)}
    \end{aligned}$$

- $f(x)$ 를 $g(x)$ 로 나누면 다음과 같음

    $$\begin{aligned}
    f(x) \div g(x)
    &= \frac{x^3 - x^2 - 2}{x(x-1)} \\
    &= \frac{x^2(x - 1) - 2}{x(x-1)} \\
    &= x - \frac{2}{x(x-1)}
    \end{aligned}$$

- 나머지를 부분분수분해하면 다음과 같음

    $$\begin{aligned}
    \frac{2}{x(x-1)}
    &= 2 \times \frac{1}{(x-1)-x}(\frac{1}{x}-\frac{1}{x-1})\\
    &= -\frac{2}{x} + \frac{2}{x-1}
    \end{aligned}$$

- $\displaystyle\frac{f(x)}{g(x)}$ 를 재정의하면 다음과 같음

    $$\begin{aligned}
    \frac{f(x)}{g(x)}
    &= x + \frac{2}{x} - \frac{2}{x-1}
    \end{aligned}$$

- 양변을 적분하면 다음과 같음

    $$\begin{aligned}
    \int\frac{f(x)}{g(x)}dx
    &= \int{[x + \frac{2}{x} - \frac{2}{x-1}]dx}\\
    &= \int{x}dx + \int{\frac{2}{x}}dx - \int{\frac{2}{x-1}}dx
    \end{aligned}$$

### 이상적분 : 극한치의 적어도 한 개가 무한일 경우의 적분법

- 피적분함수 $f(x)=\displaystyle\frac{1}{x^2}$ 에 대한 정적분을 다음과 같이 가정하자

    $$
    \int_{1}^{\infty}{\frac{1}{x^2}}dx
    $$

- 적분의 위의 한계 $\infty$ 를 상수 $k$ 로 치환하면 다음과 같음

    $$
    \lim_{k\rightarrow\infty}{\int_{1}^{k}{\frac{1}{x^2}}dx}
    $$

- $f(x)$ 를 $[1,k]$ 에서 정적분하면 다음과 같음

    $$\begin{aligned}
    \int_{1}^{k}{\frac{1}{x^2}}dx
    &= [-x^{-1}]^{k}_{1}\\
    &= -\frac{1}{k}+1
    \end{aligned}$$

- $k\rightarrow\infty$ 일 때 위 식의 값은 다음과 같음

    $$\begin{aligned}
    \lim_{k\rightarrow\infty}{-\frac{1}{k}+1}
    &= 1
    \end{aligned}$$
---
order: 3
title: Taylor Series
date: 2023-07-09
categories: [Math, Calculus]
tags: [Math]
math: true
description: >-
  Based on the lecture “Mathematics for Artificial Intelligence (2022-1)” by Prof. Yeo Jin Chung, Dept. of AI, Big Data & Management, College of Business Administration, Kookmin Univ.
image:
  path: /_post_refer_img/Calculus/Thumbnail.jpg
---

## 극점과 극값
-----

![01](/_post_refer_img/Calculus/03-01.png){: width="100%"}

- **극대점과 극대값**
    - **정의** : 함수 $y=f(x)$ 에 대하여 $x=c$ 에 근접한 모든 $x$ 가 $f(c) \ge f(x)$ 인 경우
        - $y=f(x)$ 는 $x=c$ 에서 극대값을 가진다고 하고,
        - 점 $(x=c,y=f(c))$ 를 $y=f(x)$ 의 극대점이라고 하고,
            - **극대점(Local Maximum Point)** : 주위 모든 점의 함수값 이상의 함수값을 갖는 점
        - 이때의 함수값 $f(c)$ 를 $y=f(x)$ 의 극대값이라고 함    
            - **극대값(Local Maximum Value)** : 극대점이 갖는 함수값

    - **성질**
        - 함수 $y=f(x)$ 가 구간 $[a,b]$ 에서 미분 가능하고, $x=c(a<c<b)$ 에서 극대값을 가지면 다음을 만족함
            - $\displaystyle\frac{d}{dx}f(c)=f^\prime(c)=0$
            - $\displaystyle\frac{d^2}{dx^2}f(c)=f^{\prime\prime}(c)<0$

- **극소점과 극소값**
    - **정의** : 함수 $y=f(x)$ 에 대하여 $x=c$ 에 근접한 모든 $x$ 가 $f(c) \le f(x)$ 인 경우
        - $y=f(x)$ 는 $x=c$ 에서 극소값을 가진다고 하고,
        - 점 $(x=c,y=f(c))$ 를 $y=f(x)$ 의 극소점이라고 하고,
            - **극대점(Local Minimum Point)** : 주위 모든 점의 함수값 이상의 함수값을 갖는 점
        - 이때의 함수값 $f(c)$ 를 $y=f(x)$ 의 극소값이라고 함    
            - **극대값(Local Minimum Value)** : 극대점이 갖는 함수값

    - **성질**
        - 함수 $y=f(x)$ 가 구간 $[a,b]$ 에서 미분 가능하고, $x=c(a<c<b)$ 에서 극소값을 가지면 다음을 만족함
            - $\displaystyle\frac{d}{dx}f(c)=f^\prime(c)=0$
            - $\displaystyle\frac{d^2}{dx^2}f(c)=f^{\prime\prime}(c)>0$

## 테일러 급수
-----

![02](/_post_refer_img/Calculus/03-02.png){: width="100%"}

- **테일러 다항식(Taylor Polynomial)** : $x=a$ 에서 미분 가능한 함수 $y=f(x)$ 에 대하여, $y=f(x)$ 와 $x=a$ 에서 근사하는 $n$ 차 함수

    $$\begin{aligned}
    f(x)
    &\approx \sum^{k=0}_{n}{\frac{f^{k}(a)}{k!}(x-a)^{k}}\\
    &= f(a)
    + f^{\prime}(a)(x-a)
    + \frac{f^{\prime \prime}(a)}{2!}(x-a)^{2}
    + \cdots
    + \frac{f^{n}(a)}{n!}(x-a)^{n}
    \end{aligned}$$

- **선형 근사(Linear Approximation)** : $y=f(x)$ 와 $x=a$ 에서 근사하는 $1$ 차 함수 혹은 그러한 함수를 찾는 방법

    $$
    f(x) \approx f(a) + f^{\prime}(a)(x-a)
    $$

- **테일러 급수(Taylor Series)** : $n$ 이 무한대로 발산하는 경우 테일러 다항식

    $$\begin{aligned}
    f(x)
    &\approx \sum^{k=0}_{\infty}{\frac{f^{k}(a)}{k!}(x-a)^{k}}\\
    &= f(a)
    + f^{\prime}(a)(x-a)
    + \frac{f^{\prime \prime}(a)}{2!}(x-a)^{2}
    + \cdots
    + \frac{f^{n}(a)}{n!}(x-a)^{n}
    + \cdots
    \end{aligned}$$

- **매클로린 급수(Maclaurin's Series)** : $a=0$ 인 경우 테일러 급수

    $$\begin{aligned}
    f(x)
    &\approx \sum^{k=0}_{\infty}{\frac{f^{k}(0)}{k!}x^{k}}\\
    &= f(0)
    + f^{\prime}(0)x
    + \frac{f^{\prime \prime}(0)}{2!}x^{2}
    + \cdots
    + \frac{f^{n}(0)}{n!}x^{n}
    + \cdots
    \end{aligned}$$
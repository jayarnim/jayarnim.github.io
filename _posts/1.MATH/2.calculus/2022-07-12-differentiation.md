---
order: 2
title: Differentiation
date: 2022-07-12
categories: [1.MATHEMATICAL TECHS, 2.calculus]
tags: [mathematics, calculus]
math: true
description: >-
    Based on the lecture “Mathematics for Artificial Intelligence (2022-1)” by Prof. Yeo Jin Chung, Dept. of AI, Big Data & Management, College of Business Administration, Kookmin Univ.
image:
    path: /_post_refer_img/1.MATH/2.calculus/Thumbnail.jpg
---

## Differentiation
-----

- **평균변화율**: 함수 $f:X \to Y$ 의 정의역과 공역을 각각 $x \in X, y \in Y$ 라고 했을 때, 구간 $[x,a]$ 에서 $x$ 의 변화 $\Delta x$ 에 따른 $y$ 의 평균적인 변화폭 $\Delta y / \Delta x$

    $$\begin{aligned}
    \frac{\Delta y}{\Delta x}
    = \frac{f(x)-f(a)}{x-a}
    = \frac{f(x + \Delta x) - f(x)}{\Delta x}
    \end{aligned}$$

- **순간변화율**: $x \to a$ 일 때 구간 $[x,a]$ 에서 $x$ 의 변화 $\Delta x$ 에 따른 $y$ 의 평균적인 변화폭 $\Delta y / \Delta x$ 으로서, 즉, $\Delta x \to 0$ 일 때 $y$ 의 평균변화율

    $$\begin{aligned}
    \frac{\mathrm{d}y}{\mathrm{d}x}
    = \lim_{x \to a}{\frac{f(x) - f(a)}{x-a}}
    =\lim_{\Delta x \to 0}{\frac{f(x + \Delta x) - f(x)}{\Delta x}}
    \end{aligned}$$

- **미분(Differentiation)**: 함수 $f:X \to Y$ 의 정의역과 공역을 각각 $x \in X, y \in Y$ 라고 했을 때, $x \in X$ 의 변화에 따른 $y \in Y$ 의 순간변화율을 구하는 연산자

    $$\begin{aligned}
    f^{\prime}(x)
    &= \lim_{\Delta x \to 0}{\frac{f(x + \Delta x) - f(x)}{\Delta x}}
    \end{aligned}$$

- 연산 규칙:
    - $\displaystyle\frac{\mathrm{d}}{\mathrm{d}x}\alpha=0$
    - $\displaystyle\frac{\mathrm{d}}{\mathrm{d}x}\alpha f(x)=\alpha \cdot \displaystyle\frac{\mathrm{d}}{\mathrm{d}x}f(x)$
    - $\displaystyle\frac{\mathrm{d}}{\mathrm{d}x}x^{n}=n \cdot x^{n-1}$
    - $\displaystyle\frac{\mathrm{d}}{\mathrm{d}x}[f(x)+g(x)]=\displaystyle\frac{\mathrm{d}}{\mathrm{d}x}f(x)+\displaystyle\frac{\mathrm{d}}{\mathrm{d}x}g(x)$
    - $\displaystyle\frac{\mathrm{d}}{\mathrm{d}x}[f(x)g(x)]=g(x) \cdot \displaystyle\frac{\mathrm{d}}{\mathrm{d}x}f(x)+f(x)\cdot\displaystyle\frac{\mathrm{d}}{\mathrm{d}x}g(x)$

- **연쇄 법칙(Chain Rule)**: 합성함수의 미분법으로서, $y=f(u),u=g(x)$ 가 각각 $u \in U,x \in X$ 전체에 대하여 미분 가능한 경우 다음이 성립함

    $$\begin{aligned}
    \frac{\mathrm{d}y}{\mathrm{d}x}
    = \frac{\mathrm{d}y}{\mathrm{d}u} \times \frac{\mathrm{d}u}{\mathrm{d}x}
    \end{aligned}$$

## Natural Logarithm
-----

- 자연로그의 미분법:

    $$\begin{aligned}
    \ln{x}
    &=\int_{t=1}^{t=x}{\frac{1}{t}\mathrm{d}t}\\
    \therefore \frac{\mathrm{d}}{\mathrm{d}x}\ln(x)
    &= \frac{\mathrm{d}}{\mathrm{d}x}\int_{t=1}^{t=x}{\frac{1}{t}\mathrm{d}t}=\frac{1}{x}
    \end{aligned}$$

- 상수 $e$ 에 대한 지수함수의 미분법:

    $$\begin{aligned}
    \frac{\mathrm{d}}{\mathrm{d}x}e^{x}
    &= e^{x}
    \end{aligned}$$

    - 임의의 상수 $a$ 에 대하여 정의된 지수함수 $f(x)=a^{x}$ 의 순간변화율:

        $$\begin{aligned}
        \frac{\mathrm{d}}{\mathrm{d}x}a^{x}
        &= \lim_{\Delta x \to 0}{\frac{a^{x}(a^{\Delta x}-1)}{\Delta x}}\\
        &= a^{x}
        \end{aligned}$$

    - 좌변에서 $\lim_{\Delta x \to 0}{a^{x}}$ 를 소거하면:

        $$\begin{aligned}
        \lim_{\Delta x \to 0}{\frac{a^{x}(a^{\Delta x}-1)}{\Delta x}}
        &= a^{x}\\
        \lim_{\Delta x \to 0}{a^{x}} \times \lim_{\Delta x \to 0}{\frac{a^{\Delta x}-1}{\Delta x}}
        &= a^{x}\\
        a^{x} \times \lim_{\Delta x \to 0}{\frac{a^{\Delta x}-1}{\Delta x}}
        &= a^{x}\\
        \therefore \lim_{\Delta x \to 0}{\frac{a^{\Delta x}-1}{\Delta x}}
        &= 1
        \end{aligned}$$

    - 좌변에서 $\lim_{\Delta x \to 0}{1/\Delta x}$ 를 소거하면:

        $$\begin{aligned}
        \lim_{\Delta x \to 0}{\frac{a^{\Delta x}-1}{\Delta x}}
        &= 1\\
        \frac{\lim_{\Delta x \to 0}{(a^{\Delta x}-1)}}{\lim_{\Delta x \to 0}{\Delta x}}
        &= 1\\
        \lim_{\Delta x \to 0}{(a^{\Delta x}-1)}
        &= \lim_{\Delta x \to 0}{\Delta x}
        \end{aligned}$$

    - 좌변에서 $\lim_{\Delta x \to 0}{1}$ 을 소거하면:

        $$\begin{aligned}
        \lim_{\Delta x \to 0}{(a^{\Delta x}-1)}
        &= \lim_{\Delta x \to 0}{\Delta x}\\
        \lim_{\Delta x \to 0}{a^{\Delta x}}-\lim_{\Delta x \to 0}{1}
        &= \lim_{\Delta x \to 0}{\Delta x}\\
        \lim_{\Delta x \to 0}{a^{\Delta x}}
        &= \lim_{\Delta x \to 0}{1} + \lim_{\Delta x \to 0}{\Delta x}\\
        \therefore \lim_{\Delta x \to 0}{a^{\Delta x}}
        &= \lim_{\Delta x \to 0}{(1 + \Delta x)}
        \end{aligned}$$

    - 양변을 $1/\Delta x$ 제곱하면:

        $$\begin{aligned}
        \lim_{\Delta x \to 0}{a^{\Delta x}}
        &= \lim_{\Delta x \to 0}{(1 + \Delta x)}\\
        \lim_{\Delta x \to 0}{a}
        &= \lim_{\Delta x \to 0}{(1 + \Delta x)^{1/\Delta x}}\\
        \therefore a
        &= \lim_{\Delta x \to 0}{(1 + \Delta x)^{1/\Delta x}}
        \end{aligned}$$

    - $\Delta x$ 를 $1/n$ 으로 치환하면:

        $$\begin{aligned}
        a
        &= \lim_{\Delta x \to 0}{(1 + \Delta x)^{1/\Delta x}}\\
        &= \lim_{n \to \infty}{\left(1 + \frac{1}{n}\right)^{n}}\\
        &= e
        \end{aligned}$$
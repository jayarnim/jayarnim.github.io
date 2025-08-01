---
order: 1
title: Limit and Continuity
date: 2022-07-11
categories: [MATHEMATICAL TECHS, 2.calculus]
tags: [Mathematics]
math: true
description: >-
  Based on the lecture “Mathematics for Artificial Intelligence (2022-1)” by Prof. Yeo Jin Chung, Dept. of AI, Big Data & Management, College of Business Administration, Kookmin Univ.
image:
  path: /_post_refer_img/MathematicalTechs/2.Calculus/Thumbnail.jpg
---

## Limit & Continuity
-----

- **극한(Limit)**: 함수 $f:X \to Y$ 에 대하여 $x \ne a$ 이면서 $x$ 가 $a$ 에 한없이 가까워질 때 $y$ 가 일정한 값 $z$ 에 가까워지는 경우, $y$ 가 $x \to a$ 일 때 $z$ 에 수렴한다(Converge)고 하고, $L$ 을 $x \to a$ 에서 $f$ 의 극한(Limit)이라고 함

    $$\begin{aligned}
    \lim_{x  \to a}{f(x)}=z
    \Rightarrow
    \underbrace{\lim_{x  \to a-0}{f(x)}}_{\text{left-hand limit}}
    =\underbrace{\lim_{x  \to a+0}{f(x)}}_{\text{right-hand limit}}
    =z
    \end{aligned}$$

    - $\lim_{x  \to a}{\alpha f(x)}=\alpha \lim_{x  \to a}{f(x)}$
    - $\lim_{x  \to a}{[f(x)+g(x)]}=\lim_{x  \to a}{f(x)}+\lim_{x  \to a}{g(x)}$
    - $\lim_{x  \to a}{[f(x)g(x)]}=\lim_{x  \to a}{f(x)}\lim_{x  \to a}{g(x)}$
    - $\lim_{x  \to a}{[f(x)/g(x)]}=\lim_{x  \to a}{f(x)}/\lim_{x  \to a}{g(x)} \quad (\text{s.t.}\ \lim_{x  \to a}{g(x)} \ne 0)$

- **연속(Continuity)**: 함수 $f:X \to Y$ 에 대하여 $f$ 가 $x=a$ 에서 함수값 $y=f(x)$ 과 극한값 $z=\lim_{x \to a}{f(x)}$ 이 모두 존재하고 $y=z$ 일 때 $f$ 는 $x=a$ 에서 연속임

$$\begin{aligned}
f(a)=\lim_{x \to a}{f(x)}
\end{aligned}$$

- **연속 함수(Continuous Function)**: 함수 $f:X \to Y$ 가 정의역 $a \in \mathcal{X}$ 전체에서 연속이면 $f$ 는 연속 함수임

$$\begin{aligned}
f(a)=\lim_{x \to a}{f(x)}, \quad \forall a \in \mathcal{X}
\end{aligned}$$

## Natural Logarithm
-----

![02](/_post_refer_img/MathematicalTechs/2.Calculus/02-02.svg){: width="100%"}

- **자연로그(Natural Logarithm)**: 함수 $$g(x)=1/x$$ 의 면적(정적분)에 관한 함수

    $$\begin{aligned}
    f(x)
    =\ln{x}
    =\int_{t=1}^{t=x}{\frac{1}{t}\text{d}t}
    \end{aligned}$$

- **상수 $e$**: 자연로그 값이 $1$ 일 때의 $x$ 값

    $$\begin{aligned}
    e
    = \lim_{n \to \infty}{\left(1 + \frac{1}{n}\right)^{n}}
    = 2.71828\cdots, \quad n \in \mathbb{R}
    \end{aligned}$$

- `example` $\lim_{x \to 0}{(1+3x)^{1/x}}$

    $$\begin{aligned}
    \lim_{x \to 0}{(1+3x)^{n}}
    &= \lim_{x \to 0}{\left(1+\frac{3}{n}\right)^{n}}\\
    &= \lim_{x \to 0}{\left(1+\frac{3}{n/3}\right)^{n/3 \times 3}}\\
    &= e^{3}
    \end{aligned}$$

- **연속 복리(Continuous Compounding)**: 가장 짧은 시간 간격으로 취하는 복리

    - 원금 $a$ 를 연이율 $r$ 로 $n$ 년간 복리예금 시 원리금

        $$\begin{aligned}
        S
        &= a(1+r)^{n}
        \end{aligned}$$

    - $n$ 년간 이자를 $k$ 번 계산하는 경우 원리금

        $$\begin{aligned}
        S
        &= a\left[\left(1+r/k\right)^{k}\right]^{n}
        \end{aligned}$$

    - $k \to \infty$ 일 때 원리금

        $$\begin{aligned}
        \lim_{k \to \infty}{S}
        &= \lim_{k \to \infty}{a\left[\left(1+r/k\right)^{k}\right]^{n}}\\
        &= \lim_{k \to \infty}{a\left[\left(1+\frac{1}{k/r}\right)^{k/r \times r}\right]^{n}}\\
        &= a \times e^{r \times n}
        \end{aligned}$$
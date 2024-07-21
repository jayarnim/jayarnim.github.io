---
order: 1
title: Limit and Continuity
date: 2023-07-10
categories: [Mathematical Techs, Calculus]
tags: [Mathematics]
math: true
description: >-
  Based on the lecture “Mathematics for Artificial Intelligence (2022-1)” by Prof. Yeo Jin Chung, Dept. of AI, Big Data & Management, College of Business Administration, Kookmin Univ.
image:
  path: /_post_refer_img/Calculus/Thumbnail.jpg
---

## 극한
-----

- **극한(Limiting)**

    $$\begin{aligned}
    y&=f(x) \\
    \displaystyle\lim_{x  \rightarrow a}y&=L
    \end{aligned}$$

    - 설명변수 $x \in X$ 에 대한 반응변수 $y \in Y$ 의 함수 $f:\,X\rightarrow Y$ 에 대하여
    - $x \ne a$ 이면서 $x$ 가 $a$ 에 한없이 가까워질 때 $y$ 가 일정한 값 $L$ 에 가까워지는 경우
    - $y$ 는 $x  \rightarrow a$ 일 때 $L$ 에 **수렴한다(Converge)** 라고 정의함
    - 또한 $L$ 를 $x  \rightarrow a$ 인 경우 $y$ 의 **극한(Limiting)** 이라고 정의함

- **좌극한과 우극한**

    $$
    \displaystyle\lim_{x  \rightarrow a}f(x)=L \Rightarrow \displaystyle\lim_{x  \rightarrow a-0}f(x)=\displaystyle\lim_{x  \rightarrow a+0}f(x)=L
    $$

    - 설명변수 $x \in X$ 에 대한 반응변수 $y \in Y$ 의 함수 $f:\,X\rightarrow Y$ 에 대하여
    - $f$ 가 값 $a$ 에서 극한이 존재하면
    - 그 좌극한 $x  \rightarrow a-0$ 과 우극한 $x  \rightarrow a+0$ 이 존재하고, 그 값이 서로 같음

- **성질**
    - $\displaystyle\lim_{x  \rightarrow a}f(x), \displaystyle\lim_{x  \rightarrow a}g(x)$ 가 존재하는 경우 다음이 성립함

        - $\displaystyle\lim_{x  \rightarrow a}\alpha f(x)=\alpha\displaystyle\lim_{x  \rightarrow a}f(x)$
        - $\displaystyle\lim_{x  \rightarrow a}(f(x)+g(x))=\displaystyle\lim_{x  \rightarrow a}f(x)+\displaystyle\lim_{x  \rightarrow a}g(x)$
        - $\displaystyle\lim_{x  \rightarrow a}(f(x) \times g(x))=\displaystyle\lim_{x  \rightarrow a}g(x) \times \displaystyle\lim_{x  \rightarrow a}f(x)$
        - $\displaystyle\lim_{x  \rightarrow a}\frac{f(x)}{g(x)}=\frac{\displaystyle\lim_{x  \rightarrow a}f(x)}{\displaystyle\lim_{x  \rightarrow a}g(x)}\;(s.t.\displaystyle\lim_{x  \rightarrow a}g(x) \ne 0)$

## 연속
-----

- **연속성(Continuity)**

    $$
    f(a)=\displaystyle\lim_{x  \rightarrow a}f(x)
    $$

    - 설명변수 $x \in X$ 에 대한 반응변수 $y \in Y$ 의 함수 $f:\,X\rightarrow Y$ 에 대하여
    - $f$ 가 $x=a$ 에서 함수값과 극한값이 모두 존재하고 그 값이 같을 때
    - $y=f(x)$ 는 $x=a$ 에서 연속이라고 정의함

- **연속함수(Continuous Function)**

    $$
    f(a)=\displaystyle\lim_{x  \rightarrow a}f(x), \; a \in X=R
    $$

    - 설명변수 $x \in X$ 에 대한 반응변수 $y \in Y$ 의 함수 $f:\,X\rightarrow Y$ 에 대하여
    - 정의역 $X$ 를 모든 실수 $R$ 라고 정의하자
    - $f$ 가 정의역에 대하여 연속이면 $f$ 를 연속함수라고 정의함

## 자연로그의 밑
-----

- **자연로그의 밑 $e$ 의 정의**

    $$\begin{aligned}
    e&=\displaystyle\lim_{n \rightarrow \infty}(1+\frac{1}{n})^n\\
    &=2.71818\cdots,\;n \in R
    \end{aligned}$$

- **자연로그의 정의**

    $$
    \ln x=\log_e x=a \Leftrightarrow x=e^a
    $$

- **예시**
    - $f(x)=\displaystyle\lim_{x\rightarrow 0}(1+3x)^{\frac{1}{x}}$

        $$\begin{aligned}
        n=\frac{1}{x} \Rightarrow 
        f(x)
        &=\displaystyle\lim_{n\rightarrow \infty}(1+\frac{3}{n})^n\\
        &=\displaystyle\lim_{n\rightarrow \infty}(1+\frac{3}{\frac{1}{3}n})^{3 \times \frac{1}{3}n}\\
        &=e^3
        \end{aligned}$$

- **연속복리와 $e$**
    - **복리의 이해**
        - 원금 $a$ 를 연이율 $r$ 로 $n$ 년간 복리예금 시 원리금 $S$ 를 다음과 같이 정의함

            $$
            S=a(1+r)^n
            $$
    
    - **연속복리** : 가장 짧은 시간 간격으로 취하는 복리
        - 원금 $a$ 를 연이율 $r$ 로 $n$ 년간 복리예금한다고 하자
        - $n$ 년간 $m$ 번 이자를 계산하는 경우 원리금 $S$ 를 다음과 같이 정의함

            $$
            S=a[(1+\frac{r}{m})^m]^n
            $$
        
        - $m$ 이 무한대로 발산한다고 했을 때 원리금 $S$ 를 다음과 같이 정의함

            $$\begin{aligned}
            \lim_{m \rightarrow \infty} S
            &=\lim_{m \rightarrow \infty} a[(1+\frac{r}{m})^m]^n \\
            &=\lim_{m \rightarrow \infty} a[(1+\frac{1}{\frac{1}{r}m})^{r \times \frac{1}{r}m}]^{n} \\
            &=a\times e^{r \times n}
            \end{aligned}$$
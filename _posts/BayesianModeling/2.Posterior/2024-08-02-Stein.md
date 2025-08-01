---
order: 6
title: Stein's Method
date: 2024-08-02
categories: [BAYES, 2.posterior approx.]
tags: [Bayesian, Objective Function, Stein's Method, Nonparametric Estimation]
math: true
image:
    path: /_post_refer_img/BayesianModeling/2.Posterior/Thumbnail.jpg
---

## Stein's Method
-----

- 슈타인 연산자(Stein Operator):

    > 테스트 함수 $f(x)$ 를 확률 분포 $X \sim P$ 의 구조가 반영된 형태로 변환하는 연산자로서, $x$ 의 변화에 따른 $f(x)$ 의 변화율를 측정하고, 그 변화를 $x$ 가 발생할 가능성 $X \sim P$ 이 반영된 형태로 조정하는 방식으로 동작함

    $$\begin{aligned}
    \mathcal{T}_{P}f(x)
    &= \nabla_{X}f(x) + f(x)\cdot\nabla_{X}\log{p(x)}
    \end{aligned}$$

    - $$\nabla_{X}f(x)$$ : $x$ 에 대한 $f(x)$ 의 변화율
    - $$\nabla_{X}\log{p(x)}=\displaystyle\frac{p^{\prime}(x)}{p(x)}$$ : 스코어 함수(Score Function)로서 $x$ 에 대한 $\log{p(x)}$ 의 변화율

- 슈타인 클래스(Stein Class):

    > 슈타인 연산자(Stein Operator)를 통해 변화율 조정 가능한 테스트 함수 $f(x)$ 는 확률 분포 $X \sim P$ 의 정의역 경계에서 $0$ 으로 수렴해야 하고(Boundary Condition), 정의역에서 미분 가능해야 함(Differentiability Condition)

    - Boundary Condition

        $$\begin{aligned}
        \lim_{x \to \text{boundary}}{f(x)p(x)}=0
        \end{aligned}$$

    - Differentiability Condition

        $$\begin{aligned}
        \quad \exists \nabla_{X}f(x) = \lim_{h \to 0}{\frac{f(x+h)-f(x)}{h}}, \quad \forall x \in \mathbb{R}
        \end{aligned}$$

- 슈타인의 항등식(Stein's Identity):

    > $x$ 의 변화에 따른 함수 $$f(x)$$ 의 변화 양상을 $$x$$ 발생 확률 분포로써 조정했을 때(Stein Operator) 조정된 변화율의 기대값이 $0$ 이 되는 성질로서, 슈타인 연산자(Stein Operator)를 거친 슈타인 클래스(Stein Class) $$f(x)$$ 가 특정 확률 분포 $$X \sim P$$ 에서 평균적으로 변화가 없음을 보장하는 정리

    $$\begin{aligned}
    \mathbb{E}_{X \sim P}\left[\mathcal{T}_{P}f(x)\right]
    &=0
    \end{aligned}$$

## KSD
-----

- **Stein's Identity Application**

    - if $q(x)=p(x)$:

        $$\begin{aligned}
        \mathbb{E}_{x \sim q}\left[\mathcal{T}_{p}f(x)\right]
        = \begin{cases}\int{q(x) \cdot \mathcal{T}_{p}f(x)\text{d}x}\\
        \sum{q(x) \cdot \mathcal{T}_{p}f(x)}
        \end{cases}
        = 0
        \end{aligned}$$

    - else:

        $$\begin{aligned}
        \mathbb{E}_{x \sim q}\left[\mathcal{T}_{p}f(x)\right]
        = \begin{cases}\int{q(x) \cdot \mathcal{T}_{p}f(x)\text{d}x}\\
        \sum{q(x) \cdot \mathcal{T}_{p}f(x)}
        \end{cases}
        \ne 0
        \end{aligned}$$

- **KSD(`K`ernelized `S`tein `D`iscrepancy)** : `Stein's Identity` 를 활용하여 두 확률 분포 간 차이를 측정하되, 이때 테스트 함수로서 RKHS 상의 함수를 적용함

    - Stein Discrepancy:

        $$\begin{aligned}
        D_{\text{STEIN}}(q \parallel p)
        &= \sup_{f \in \mathcal{F}}{\mathbb{E}_{x \sim q}\left[\mathcal{T}_{p}f(x)\right]}
        \end{aligned}$$

    - If Test Function is defined in RKHS:

        $$\begin{aligned}
        f(x)
        = \sum_{i=1}^{n}{\alpha_{i} \cdot K(x, x_{i})},\quad f \in \mathcal{H}_{K}
        \end{aligned}$$

    - Argument of Supremum is:

        $$\begin{aligned}
        f^{*}(x)
        &= \text{arg} \sup_{f \in \mathcal{F}}{\mathbb{E}_{x \sim q}\left[\mathcal{T}_{p}f(x)\right]}\\
        &= \mathbb{E}_{x^{\prime} \sim q}[K(x, x^{\prime}) \cdot \nabla_{x^{\prime}}\log{p(x^{\prime})}+\nabla_{x^{\prime}}K(x, x^{\prime})]
        \end{aligned}$$

    - Therefore:

        $$\begin{aligned}
        D_{\text{STEIN}}(q \parallel p)
        &= \mathbb{E}_{x,x^{\prime}\sim q}\left[\nabla_{x}\log{p(x)}^{T} \cdot K(x,x^{\prime}) \cdot \nabla_{x^{\prime}}\log{p(x^{\prime})} + \nabla_{x}\nabla_{x^{\prime}}K(x,x^{\prime})\right]
        \end{aligned}$$
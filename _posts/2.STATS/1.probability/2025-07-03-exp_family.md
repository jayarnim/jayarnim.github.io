---
order: 3
title: Exponential Family
date: 2025-07-03
categories: [2.STATISTICAL TECHS, 1.probability]
tags: [statistics, uncertainty, probability, random variable, probability distribution, measure, parameter, exponential family, conjugate]
math: true
description: >-
    Based on the following lectures <br>
    (1) “Statistics (2018-1)” by Prof. Sang Ah Lee, Dept. of Economics, College of Economics & Commerce, Kookmin Univ. <br>
    (2) "Statistical Models and Application (2024-1)" by Prof. Yeo Jin Chung, Dept. of Data Science, The Grad. School, Kookmin Univ. <br>
    (3) “Bayesian Modeling (2024-1)” by Prof. Yeo Jin Chung, Dept. of AI, Big Data & Management, College of Business Administration, Kookmin Univ.
image:
    path: /_post_refer_img/2.STATS/1.probability/Thumbnail.jpg
---

## parameter
-----

- **파라미터(Parameter)**: 특정 구조로 가정된 분포 모형의 구체적 형태를 조정하는 변수
    - **위치 파라미터(Location Parameter)**: 분포의 중심 위치를 조정하는 파라미터

        $$
        X\mapsto X+\theta
        $$

    - **척도 파라미터(Scale Parameter)**: 분포의 폭을 조정하는 파라미터

        $$
        X\mapsto \theta\cdot X
        $$

    - **형상 파라미터(Shape Parameter)**: 왜도, 첨도 등 분포의 모양을 조정하는 파라미터

        $$
        X\mapsto g(X;\theta)
        $$

- **Parameteric Distribution Families**
    - location family
    - scale family
    - shape family
    - location-scale family
    - location-scale-shape family
    - mixture family
    - **exponential family**
    - conjugate family
    - non-exponential family

## exponential family
-----

- **지수족(Exponential Family)**: 확률 분포 함수를 지수 함수로 변환하였을 때, 충분통계량 $T(x)$ 과 자연매개변수 $\eta(\theta)$ 가 선형 결합으로 표현되고, 정규화 항 $A(\eta)$ 과 기저 측도 $h(x)$ 가 분리된 하나의 구조로 표현될 수 있는 확률분포들의 모임

    $$\begin{aligned}
    P_{X}(B)
    &=\int_{x\in B}{f(x)\mathrm{d}\mu(x)}\\
    &=\int_{x\in B}{\exp{\left[\eta(\theta)^{T}T(x)-A(\eta)\right]}\mathrm{d}\nu(x)}
    \end{aligned}$$

- **정규 형식(canonical form)**:

    $$
    f(x\mid\theta)
    =h(x)\exp{\left[\eta(\theta)^{T}T(x)-A(\eta)\right]}
    $$

    - $f(x\mid\theta)$: probability distribution function
    - $T(x)$: sufficient statistics
    - $\eta(\theta)$: natural parameter
    - $h(x)$: base measure

- **충분통계량(Sufficient Statistics)**: 관측 데이터 $x\in X$ 로부터 모수 $\theta$ 추정에 필요한 정보를 충분히 요약하는(정보 손실 없이 요약하는) 함수
  
    $$
    f(\theta\mid x)=f(\theta\mid T(x))
    $$
  
- **자연매개변수(Natural Parameter)**: 확률분포의 로그 우도 $\log{p(x)}$ 가 충분통계량 $T(x)$ 에 대하여 선형 형식으로 표현되도록 만드는 파라미터 변환, 혹은 그 표현

    $$
    \eta=g(\theta)
    $$

- **기저 측도(Base Measure)**: 파라미터 $\theta$ 에 대하여 독립인 항

    $$
    \mathrm{d}\nu(x):=h(x)\mathrm{d}\mu(x)
    $$

    - common representation of measures in exponential normal form:

        $$\begin{aligned}
        \int_{x\in X}{f(x)\underbrace{\mathrm{d}\mu(x)}_{\text{refer. measure}}}
        &=\int_{x\in X}{\exp{\left[\eta(\theta)^{T}T(x)-A(\eta)\right]}\underbrace{h(x)\mathrm{d}\mu(x)}_{\text{base measure}}}
        \end{aligned}$$

    - support set (domain) of the probability measure:

        $$\begin{gathered}
        f(x)>0\Leftrightarrow h(x)>0\quad(\because\exp{(\cdot)}>0)\\
        \therefore\mathrm{supp}(f):=\{x\mid h(x)>0\}
        \end{gathered}$$

- **정규화 항(Normalizer)**: 충분통계량과 자연매개변수의 선형 결합이 확률 분포의 요건을 갖출 수 있도록($P(\Omega)=1$) 정규화하는 항

    $$\begin{aligned}
    \exp{A(\eta)}
    &=\int_{x\in X}{\exp{\left[\eta(\theta)^{T}T(x)\right]}\mathrm{d}\nu(x)}
    \end{aligned}$$

    - parameter space:

        $$\begin{gathered}
        \frac{\eta(\theta)^{T}T(x)}{A(\theta)}=1\\
        \therefore\Theta:=\left\{\theta\mid A(\theta)<\infty\right\}
        \end{gathered}$$

    - moment generating structure:

        $$\begin{aligned}
        \exp{A(\eta)}
        &=\mathbb{E}_{\nu}\left[\exp{\eta(\theta)^{T}T(X)}\right]\\
        &=\sum_{k=0}^{\infty}{\frac{\eta^{k}(\theta)}{k!}\mathbb{E}_{\nu}\left[T^{k}(X)\right]}\\
        \\
        \therefore\nabla_{\eta}^{k}A(\eta)
        &=\mathbb{E}_{\nu}\left[T^{k}(X)\right]
        \end{aligned}$$

## bayes rule
-----

- prior:

    $$
    p(\eta)\propto\exp{\left[\alpha\eta(\theta)-\beta A(\eta)\right]}
    $$

- likelihood:

    $$\begin{aligned}
    p(x_{1},\cdots,x_{n}\mid\eta)
    &=\prod_{i=1}^{n}{h(x_{i})\exp{\left[\eta(\theta)^{T}T(x_{i})-A(\eta)\right]}}\quad(\because x_{i}\perp x_{j})\\
    &=\prod_{i=1}^{n}{h(x_{i})}\cdot\exp{\left[\eta(\theta)\sum_{i=1}^{n}{T(x_{i})}-nA(\eta)\right]}
    \end{aligned}$$

- posterior:

    $$\begin{aligned}
    p(\eta\mid x_{1},\cdots,x_{n})
    &\propto p(x_{1},\cdots,x_{n}\mid\eta)\cdot p(\eta)\\
    &\propto \prod_{i=1}^{n}{h(x_{i})}\cdot\exp{\left[\eta(\theta)\sum_{i=1}^{n}{T(x_{i})}-nA(\eta)\right]}\cdot\exp{\left[\alpha\eta(\theta)-\beta A(\eta)\right]}\\
    &=\prod_{i=1}^{n}{h(x_{i})}\cdot\exp{\left[\left(\alpha+\sum_{i=1}^{n}{T(x_{i})}\right)\eta(\theta)-(\beta+n)A(\eta)\right]}\\
    \\
    \alpha^{\prime}
    &:=\alpha+\sum_{i=1}^{n}{T(x_{i})}\\
    \beta^{\prime}
    &:=\beta+n\\
    \\
    \therefore p(\eta\mid x_{1},\cdots,x_{n})
    &\propto \prod_{i=1}^{n}{h(x_{i})}\cdot\exp{\left[\alpha^{\prime}\eta(\theta)-\beta^{\prime}A(\eta)\right]}
    \end{aligned}$$
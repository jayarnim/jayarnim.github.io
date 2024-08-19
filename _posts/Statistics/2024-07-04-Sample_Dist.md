---
order: 4
title: Sample Dist.
date: 2024-07-04
categories: [Statistical Techs, Statistics]
tags: [Statistics]
math: true
description: >-
  Based on the following lectures <br>
  (1) “Statistics (2018-1)” by Prof. Sang Ah Lee, Dept. of Economics, College of Economics & Commerce, Kookmin Univ. <br>
  (2) "Statistical Models and Application (2024-1)" by Prof. Yeo Jin Chung, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
  path: /_post_refer_img/Statistics/Thumbnail.png
---

## Random Sample
-----

### Statistical Inference

- **통계적 추론(Statistical Inference)**
    - **정의** : 표본을 사용하여 모집단의 성격을 추정하는 작업
        - 표본의 측정치를 모집단의 측정치에 대한 추정치로 간주함

    - **목표** : 표본오차의 크기 최소화
        - 표본은 모집단의 부분집합일 뿐이지, 모집단은 아니므로 모수와 통계량은 완전히 일치할 수 없음

- **표본오차(Sampling Error)** : 응답오차, 측정오차, 표본선택편향이 해결되었음에도 발생하는 실제값과 예측값의 차이
    - **응답오차(Response Error)** : 응답자의 응답 거부 혹은 잘못된 응답으로 인해 발생하는 오차
    - **측정오차(Measurement Error)** : 데이터의 틀린 측정이나 기입으로 인해 발생하는 오차
    - **표본선택편향(Sample Selection Bias)** : 모집단의 각 관측치들이 표본에 포함될 확률이 서로 다른 경우

### Population & Sample

> 모수는 그 값이 알려져 있지 않은 고정된 수이다. 이 값을 추정하기 위하여 표본의 통계량을 사용하므로, 통계량은 모수의 추정량이라 할 수 있다. 그런데 모집단에서 어떤 표본을 추출하느냐에 따라 통계량의 실현값이 달라진다. 따라서 모수는 **상수(Constant)**, 통계량은 **확률변수(Random Variable)**라고 볼 수 있다.

- **모집단(Population)의 모수(Parameter)**
    - **모평균** : $\mu$
    - **모분산** : $\sigma^2$

- **표본(Sample)의 통계량(Statistic)**
    - **표본평균** : $\overline{X}$

        $$\begin{aligned}
        \overline{X}
        &= \frac{1}{n}(X_{1}+X_{2}+\cdots+X_{n}) \quad \text{for}\; X_{\forall} \in \Omega\\
        &= \frac{1}{n}\sum_{i=1}^{n}{X_{i}}
        \end{aligned}$$

    - **표본분산** : $S^2$

        $$\begin{aligned}
        S^2
        &= \frac{1}{\nu}\left[\vert X_{1} - \overline{X}\vert^2 + \vert X_{2} - \overline{X}\vert^2 + \cdots + \vert X_{n} - \overline{X}\vert^2 \right]\\
        &= \frac{1}{\nu}\sum_{i=1}^{n}(X_{i}-\overline{X})^2
        \end{aligned}$$

    - `note` **자유도(Degree of Freedom; $\nu$)** : 주어진 자료 내에서 독립적으로 변할 수 있는 확률변수의 수
        - 어떠한 자료에 대하여 그 기술통계량이 주어지는 경우, 특정 관측치의 정보가 불분명하더라도 해당 관측치가 취할 수 있는 값은 제한되어 있음
        - 표본분산 $S^2$ 을 계산하기 위해서는 표본평균 $\overline{X}$ 을 먼저 계산해야 하므로, 분산 계산 시 동원되는 관측치 중 독립적으로 변할 수 있는 관측치의 수는 $n-1$ 임
        - 이 경우 관측치 수 $n$ 이 아니라 자유도 $\nu=n-1$ 로 나눈 값이 모분산 $\sigma^2$ 의 비편향 추정량임

### Random Sample

- 모집단으로부터 관측치 $X_1, X_2, X_3, \cdots, X_n$ 를 추출하여 구성한 표본에 대하여

    $$\begin{aligned}
    \{X_1, X_2, X_3, \cdots, X_N\}
    \end{aligned}$$

- 모집단의 각 개체가 표본의 원소로서 선택될 확률이 모두 같고,

    $$
    P(X_{i}=x_{i})=\frac{1}{N} \quad \text{for}\;i=1,2,\cdots,N
    $$

- 원소 $X_1, X_2, X_3, \cdots, X_n$ 이 모두 모집단의 분포를 따르는 확률변수이고,

    $$\begin{aligned}
    E\left[X_{i^{\forall}}\right]&=\mu \\
    Var\left[X_{i^{\forall}}\right]&=\sigma^2
    \end{aligned}$$

- 원소 $X_1, X_2, X_3, \cdots, X_n$ 이 모두 통계적으로 독립인 경우

    $$
    P(X_{j^{\forall}} \vert X_{i^{\forall}}) = P(X_{j^{\forall}})
    $$

## Sample Distribution
-----

### What? Sample Dist.

- **표본분석의 목적** : 모수 추정
    - 표본의 평균 $\overline{X}$ 가 모집단의 평균 $\mu$ 를 얼마나 잘 추정하는가
    - 확률변수 $\overline{X}$ 의 기대값 $E(\overline{X})$ 은 상수 $\mu$ 에 가까운가
    - 추정량 $\overline{X}$ 의 기대값 $E(\overline{X})$ 과 모수 $\mu$ 사이에는 얼마나 큰 추정오차가 존재하는가

- **추정량과 추정치의 정의**
    - **추정량(Estimator)** : 모수를 추정하는 값으로서 통계량(Statistics)
        - 모평균 $\mu$ 의 추정량 : 표본평균 $\overline{X}$
        - 모분산 $\sigma^2$ 의 추정량 : 표본분산 $S^2$
        - 모표준편차 $\sigma$ 의 추정량 : 표본표준편차 $S$

    - **추정치(Estimate)** : 특정 표본에서 얻어진 추정량의 실현값(Realized Value)

- **표본분포(Sampling Distribution)** : 모수에 대한 추정량의 확률분포
    - 모집단의 평균을 추정하기 위해 여러 표본을 뽑을 때 표본 평균의 추정치들의 분포

        $$
        \overline{X} \sim N(\mu, \displaystyle\frac{\sigma^2}{n}) \quad (\text{s.t.}\;n>30)
        $$

    - 모집단의 평균을 추정하기 위해 여러 표본을 뽑을 때 표본 비율의 추정치들의 분포

        $$
        P \sim N(\pi, \displaystyle\frac{\pi(1-\pi)}{n}) \quad (\text{s.t.}\;n>30)
        $$

### Statistics

- **$\overline{X}$ 의 기대값** : $E\left[\overline{X}\right]=\mu$

    $$\begin{aligned}
    E\left[\overline{X}\right]
    &= E\left[\frac{1}{n}(\overline{x}_1+\overline{x}_2+\cdots+\overline{x}_n)\right]\\
    &=\frac{1}{n}\bigg[E\left[\overline{x}_1+\overline{x}_2+\cdots+\overline{x}_n\right]\bigg]\\
    &=\frac{1}{n}\bigg[E\left[\overline{x}_1\right]+E\left[\overline{x}_2\right]+\cdots+E\left[\overline{x}_n\right]\bigg]\\
    &=\frac{1}{n}(\mu + \cdots + \mu)\\
    &=\mu
    \end{aligned}$$

- **$\overline{X}$ 의 분산** : $Var\left[\overline{X}\right]=\displaystyle\frac{\sigma^2}{n}$

    $$\begin{aligned}
    Var\left[\overline{X}\right]
    &= Var\left[\frac{1}{n}(\overline{x}_1+\overline{x}_2+\cdots+\overline{x}_n)\right]\\
    &=Var\left[\frac{1}{n}\overline{x}_1\right]+Var\left[\frac{1}{n}\overline{x}_2\right]+\cdots+Var\left[\frac{1}{n}\overline{x}_n\right]\\
    &(\because Cov\left[\overline{x}_i, \overline{x}_j\right]=0)\\
    &=\frac{1}{n^2}Var\left[\overline{x}_1\right]+\frac{1}{n^2}Var\left[\overline{x}_2\right]+\cdots+\frac{1}{n^2}Var\left[\overline{x}_n\right]\\
    &=\frac{1}{n^2}\sigma^2 + \frac{1}{n^2}\sigma^2 + \cdots + \frac{1}{n^2}\sigma^2\\
    &=\frac{1}{n^2}(\sigma^2 + \cdots + \sigma^2)\\
    &=\frac{\sigma^2}{n}
    \end{aligned}$$

- **표준오차(Standard Error; $SE$)** : $\overline{X}$ 의 표준편차
    
    > 표본 $sample1, sample2, \cdots$ 에 의해 얻어진 추정량 $\overline{X}$ 의 실현값 $\overline{x}_1, \overline{x}_2, \cdots$ 은 $\mu$ 를 기준으로 얼마나 널리 퍼져 있는가

    $$\begin{aligned}
    SE
    &=\sqrt{\frac{\sigma^2}{n}}\\
    &=E\left[\vert\overline{x}_{i}-\mu\vert\right]
    \end{aligned}$$

    - $\overline{X}$ 의 표준편차는 모수 $\mu$ 와 그 추정치 $\overline{x}_{i}$ 의 차이의 평균임
    - $Var(\overline{X})$ 가 작을수록 모수 $\mu$ 에 근사하는 추정량 $\overline{X}$ 가 실현될 가능성이 높음

### Central Limit Theorem

- **중심극한정리(Central Limit Theorem; $CLT$)**

    > 평균이 $\mu$ 이고, 분산이 $\sigma^2$ 인 모집단에서 크기가 $n$ 인 표본을 추출하는 경우 $n$ 이 증가할수록 표본평균 $\overline{X}$ 의 분포는 평균이 $\mu$ 이고, 분산이 $\sigma^2$ 일 때의 가우시안 분포에 근사함

    $$
    \overline{X} \sim N(\mu, \frac{\sigma^2}{n}),\quad \text{s.t.}\,n > 30
    $$

    - $n \le 30$ 인 경우에는 모집단의 분포에 의존함
    - $n > 30$ 인 경우에는 모집단의 분포와 상관 없이 성립함

## Proportion
-----

### Population Proportion

- **모비율(Population Proportion; $\pi$)** : 모집단 중 특정 성질을 가지는 관측치 비율

    $$
    \pi \times 100\%
    $$

- **모비율에 대한 확률변수 정의** : 베르누이 확률변수

    $$
    X \sim Bernoulli(\pi)
    $$

    - 관측치 $X_i$ 가 성질을 만족하면 $1$, 만족하지 않으면 $0$ 이라고 하자

        $$
        X=
        \begin{cases}
        1\quad \text{with probability}\;\pi\\
        0\quad \text{with probability}\;1-\pi
        \end{cases}
        $$

    - 확률변수 $X$ 의 기대값

        $$\begin{aligned}
        E\left[X\right]
        &=1\times\pi + 0\times(1-\pi) \\
        &=\pi
        \end{aligned}$$

    - 확률변수 $X$ 의 분산

        $$\begin{aligned}
        Var\left[X\right]
        &=(1-\pi)^2\times\pi + (0-\pi)^2\times(1-\pi) \\
        &=\pi(1-\pi)
        \end{aligned}$$

### Sample Proportion

- **표본비율(Sample Proportion; $P$)** : 모비율에 대한 표본평균
    
    > 크기가 $n$ 인 표본을 추출할 때 모비율 $\pi$ 에 대한 표본평균 $P$ 는 다음과 같음

    $$\begin{aligned}
    P
    &= \frac{1}{n}\displaystyle\sum_{i=1}^{n}{p_i}
    \end{aligned}$$

- **$P$ 의 기대값** : $E\left[P\right]=\pi$

    $$\begin{aligned}
    E\left[P\right]
    &= E\left[\frac{1}{n}(p_1+p_2+\cdots+p_n)\right]\\
    &=\frac{1}{n}\bigg[E\left[p_1+p_2+\cdots+p_n\right]\bigg]\\
    &=\frac{1}{n}\bigg[E\left[p_1\right]+E\left[p_2\right]+\cdots+E\left[p_n\right]\bigg]\\
    &=\frac{1}{n}(\pi + \cdots + \pi)\\
    &=\pi
    \end{aligned}$$

- **$P$ 의 분산** : $Var\left[P\right]=\displaystyle\frac{\pi(1-\pi)}{n}$

    $$\begin{aligned}
    Var\left[P\right]
    &= Var\left[\frac{1}{n}(p_1+p_2+\cdots+p_n)\right]\\
    &= Var\left[\frac{1}{n}p_1\right]+Var\left[\frac{1}{n}p_2\right]+\cdots+Var\left[\frac{1}{n}p_n\right]\\
    &= \frac{1}{n^2}Var\left[p_1\right]+\frac{1}{n^2}Var\left[p_2\right]+\cdots+\frac{1}{n^2}Var\left[p_n\right]\\
    &= \frac{1}{n^2}\Big[\pi(1-\pi)+\cdots+\pi(1-\pi)\Big]\\
    &= \frac{\pi(1-\pi)}{n}
    \end{aligned}$$

- **표본비율에 대한 중심극한정리**

    > 표본의 크기 $n$ 이 충분히 크면 표본비율 $P$ 는 다음과 같은 분포를 따르게 됨

    $$
    P \sim N(\pi, \frac{\pi(1-\pi)}{n})
    $$
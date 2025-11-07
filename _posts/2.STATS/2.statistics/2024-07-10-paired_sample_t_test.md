---
order: 10
title: Paired Sample t-Test
date: 2024-07-10
categories: [2.STATISTICAL TECHS, 2.statistics]
tags: [statistics, design of experiments, a/b test, t-test, two sample t-test, paired sample t-test, student’s t-distribution]
math: true
description: >-
    Based on the following lectures <br>
    (1) “Statistics (2018-1)” by Prof. Sang Ah Lee, Dept. of Economics, College of Economics & Commerce, Kookmin Univ. <br>
    (2) "Statistical Models and Application (2024-1)" by Prof. Yeo Jin Chung, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
    path: /_post_refer_img/2.STATS/2.statistics/Thumbnail.png
---

## Paired Sample t-Test
-----

- **쌍체표본 t 검정(Paired Sample t-Test)** : 쌍을 이루는 두 변수 간 차이의 평균이 기대되는 값($\mu_0$)과 통계적으로 유의한 차이가 있는지 검정하는 방법

    > 주식시장의 변동은 일부 투자자들로 하여금 주식을 팔고 그들의 자금을 더 안전한 투자로 이동시키게 만든다. 최근 주식시장의 변동이 주식 보유에 어느 정도 영향을 미쳤는지를 결정하기 위해 주식을 소유하고 있는 170 명을 대상으로 서베이를 실시하였다. 실험 대상자들의 재작년 말과 작년 말 주식 보유액을 기록하였다. 주식 보유액이 감소했다고 추론할 수 있는가?

    - **쌍체표본(Paired Sample)** : 동일한 대상에 대하여 두 번의 측정을 통해 얻은 표본, 혹은 변수 간 상관관계가 존재하는 두 대상에 대하여 측정을 통해 얻은 표본

- 모수(Parameter) 정의:

    $$\begin{aligned}
    \mu_{D}
    &= \frac{1}{N}\sum_{i=1}^{N}{\left(X^{(A)}_{i}-X^{(B)}_{i}\right)}
    \end{aligned}$$

- 점 추정량(Point Estimator) 도출:

    $$\begin{aligned}
    \overline{X}_{D}
    &= \frac{1}{n}\sum_{i=1}^{n}{\left(X^{(A)}_{i}-X^{(B)}_{i}\right)}
    \end{aligned}$$

- 가설(Hypothesis) 설정:
    - $H_{0}:\quad \mu_{D} = \mu_{0}$
    - $H_{1}:\quad \mu_{D} \ne \mu_{0}$

- 검정통계량(Test Statistic):

    $$\begin{aligned}
    T \sim t(\nu)
    \end{aligned}$$

## Test Statistic
-----

$$\begin{aligned}
T
&= \frac{\overline{X}-\mu_{0}}{s_{D} / \sqrt{n}}
\end{aligned}$$

- $$\mathbb{E}\left[\overline{X}_{D}\right]$$:

    $$\begin{aligned}
    \mathbb{E}\left[ \overline{X}_{D}\right]
    &= \mathbb{E}\left[\frac{1}{n}\sum_{i=1}^{n}{\left(X^{(A)}_{i}-X^{(B)}_{i}\right)}\right]\\
    &= \mathbb{E}\left[\frac{1}{n}\left(\sum_{i=1}^{n}{X^{(A)}_{i}}-\sum_{i=1}^{n}{X^{(B)}_{i}}\right)\right]\\
    &= \mathbb{E}\left[\frac{1}{n}\sum_{i=1}^{n}{X^{(A)}_{i}}-\frac{1}{n}\sum_{i=1}^{n}{X^{(B)}_{i}}\right]\\
    &= \mathbb{E}\left[\frac{1}{n}\sum_{i=1}^{n}{X^{(A)}_{i}}\right]-\mathbb{E}\left[\frac{1}{n}\sum_{i=1}^{n}{X^{(B)}_{i}}\right]\\
    &= \mathbb{E}\left[\overline{X}_{A}\right]-\mathbb{E}\left[\overline{X}_{B}\right]\\
    &= \mu_A - \mu_B\\
    &= \mu_{D}
    \end{aligned}$$

- $$\mathrm{Var}\left[\overline{X}\right]$$:

    $$\begin{aligned}
    \mathrm{Var}\left[\overline{X}\right]
    &= \mathrm{Var}\left[\frac{1}{n}\sum_{i=1}^{n}{\left(X^{(A)}_{i}-X^{(B)}_{i}\right)}\right]\\
    &= \mathrm{Var}\left[\frac{1}{n}\sum_{i=1}^{n}{X^{(A)}_{i}}-\frac{1}{n}\sum_{i=1}^{n}{X^{(B)}_{i}}\right]\\
    &= \mathrm{Var}\left[\overline{X}_{A}-\overline{X}_{B}\right]\\
    &= \mathrm{Var}\left[\overline{X}_{A}\right] + \mathrm{Var}\left[\overline{X}_{B}\right] - 2 \times \mathrm{Cov} \left[\overline{X}_{A}, \overline{X}_{B}\right]\\
    &=\frac{s_{A}^{2}}{n}+\frac{s_{B}^{2}}{n}-2\times\frac{r_{A,B}}{n}\\
    &=\frac{1}{n}\left(s_{A}^{2} + s_{B}^{2} - 2 \times r_{A,B}\right)\\
    &=\frac{s_{D}^2}{n}
    \end{aligned}$$

- Standardized $T$:

    $$\begin{aligned}
    T
    &= \frac{\overline{X}_{D}-\mu_{0}}{s_{D}/\sqrt{n}}\\
    &= \frac{\overline{X}_{D}-\mu_{D}}{s_{D}/\sqrt{n}} + \frac{\mu_{D}-D_{0}}{s_{D}/\sqrt{n}}\\
    &= \frac{\mu_{D}-\mu_{0}}{s_{D}/\sqrt{n}} \quad (\because \mathbb{E}\left[\overline{X}_{D}\right]=\mu_{D})
    \end{aligned}$$
---
order: 7
title: Welch’s t-Test
date: 2024-07-07
categories: [2.STATISTICAL TECHS, 2.statistics]
tags: [statistics, design of experiments, a/b test, t-test, two sample t-test, independent samples t-test, welch’s t-test, student’s t-distribution]
math: true
description: >-
    Based on the following lectures <br>
    (1) “Statistics (2018-1)” by Prof. Sang Ah Lee, Dept. of Economics, College of Economics & Commerce, Kookmin Univ. <br>
    (2) "Statistical Models and Application (2024-1)" by Prof. Yeo Jin Chung, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
    path: /_post_refer_img/2.STATS/2.statistics/Thumbnail.png
---

## Welch’s t-Test
-----

- **웰치의 t 검정(Welch’s t-Test)**: 독립표본 t 검정(Independent Samples t-Test) 중 이분산 t 검정으로서($\sigma_{1} \ne \sigma_{2}$), 등분산 가정이 성립하지 않는 두 독립표본의 평균이 통계적으로 유의한 차이가 있는지 검정하는 방법

    > 한 메이저 리그 야구경기를 마무리하는 데 걸리는 시간에 대한 우려가 팬과 구단주 사이에서 점차 더 커지고 있다. 이 문제의 심각성을 평가하기 위해서, 한 통계 전문가는 5년 전과 금년에 임의표본을 구성하는 경기들을 마무리하는데 걸린 시간을 기록하였다. 한 경기를 마무리하는 데 걸리는 시간이 5년 전보다 금년이 더 길다고 결론을 내릴 수 있는가?

- 모수(Parameter) 정의:

    $$\begin{aligned}
    \mu_{1} - \mu_{2}
    \end{aligned}$$

- 점 추정량(Point Estimator) 도출:

    $$\begin{aligned}
    \overline{X}_{1}-\overline{X}_{2}
    \end{aligned}$$

- 가설(Hypothesis) 설정:
    - $H_{0}:\quad \mu_1-\mu_2=D_{0}$
    - $H_{1}:\quad \mu_1-\mu_2 \ne D_{0}$

- 검정통계량(Test Statistic):

    $$\begin{aligned}
    T \sim t(\nu_W)
    \end{aligned}$$

- **Welch-Satterthwaite 자유도(Welch-Satterthwaite Degree of Freedom)**: $$\overline{X}_{1} - \overline{X}_{2}$$ 의 종합적인 변동성을 각 표본들이 변동성에 대하여 기여한 정도로써 가중 평균한 값

    $$\begin{aligned}
    \nu_{W}
    &= \frac{\left(s_{1}^{2}/n_{1} + s_{2}^{2}/n_{2}\right)^{2}}{(s_{1}^{2}/n_{1})/\nu_{1} + (s_{2}^{2}/n_{2})/\nu_{2}}
    \end{aligned}$$

## Test Statistic
-----

$$\begin{aligned}
T
&= \frac{(\overline{X}_1-\overline{X}_2)-D_{0}}{\sqrt{s_{1}^{2}/n_{1}+s_{2}^{2}/n_{2}}}
\end{aligned}$$

- $$\mathbb{E}\left[\overline{X}_{1}-\overline{X}_{2}\right]$$:

    $$\begin{aligned}
    \mathbb{E}\left[\overline{X}_{1}-\overline{X}_{2}\right]
    &= \mathbb{E}\left[\overline{X}_{1}\right] - \mathbb{E}\left[\overline{X}_{2}\right]\\
    &= \mu_{1} - \mu_{2}
    \end{aligned}$$

- $$\mathrm{Var}\left[\overline{X}_{1}-\overline{X}_{2}\right]$$:

    $$\begin{aligned}
    \mathrm{Var}\left[\overline{X}_{1}-\overline{X}_{2}\right]
    &= \mathrm{Var}\left[\overline{X}_{1}\right] + \mathrm{Var}\left[\overline{X}_{2}\right] - 2 \times \mathrm{Cov}\left[\overline{X}_{1}, \overline{X}_{2}\right]\\
    &= \mathrm{Var}\left[\overline{X}_{1}\right] + \mathrm{Var}\left[\overline{X}_{2}\right] \quad (\because \mathrm{Cov}\left[\overline{X}_{1}, \overline{X}_{2}\right] = 0)\\
    &= \frac{s_{1}^{2}}{n_{1}} + \frac{s_{2}^{2}}{n_{2}}
    \end{aligned}$$

- Standardized $T$:

    $$\begin{aligned}
    T
    &= \frac{(\overline{X}_{1}-\overline{X}_{2})-D_{0}}{s_{1}^{2}/n_{1} + s_{2}^{2}/n_{2}}\\
    &= \frac{(\overline{X}_{1}-\overline{X}_{2})-(\mu_{1}-\mu_{2})}{s_{1}^{2}/n_{1} + s_{2}^{2}/n_{2}} + \frac{(\mu_{1}-\mu_{2})-D_{0}}{s_{1}^{2}/n_{1} + s_{2}^{2}/n_{2}}\\
    &= \frac{(\mu_{1}-\mu_{2})-D_{0}}{s_{1}^{2}/n_{1} + s_{2}^{2}/n_{2}} \quad (\because \mathbb{E}\left[\overline{X}\right]=\mu)
    \end{aligned}$$
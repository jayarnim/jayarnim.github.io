---
order: 9
title: Levene’s Test
date: 2024-07-09
categories: [2.STATISTICAL TECHS, 2.statistics]
tags: [statistics, design of experiments, a/b test, f-test, equal-variance test, levene’s test, f distribution]
math: true
description: >-
    Based on the following lectures <br>
    (1) “Statistics (2018-1)” by Prof. Sang Ah Lee, Dept. of Economics, College of Economics & Commerce, Kookmin Univ. <br>
    (2) "Statistical Models and Application (2024-1)" by Prof. Yeo Jin Chung, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
    path: /_post_refer_img/2.STATS/2.statistics/Thumbnail.png
---

## Levene’s Test
-----

- **레벤의 검정(Levene’s Test)**: 두 개 이상의 독립표본이 등분산성(Homogeneity of Variances)을 만족하는지 검정하는 방법

- 모수(Parameter) 정의:

    $$\begin{aligned}
    \sigma_{1}^{2},\sigma_{2}^{2},\cdots,\sigma_{k}^{2}
    \end{aligned}$$

- 점 추정량(Point Estimator) 도출:

    $$\begin{aligned}
    s_{1}^{2},s_{2}^{2},\cdots,s_{k}^{2}
    \end{aligned}$$

- 가설(Hypothesis) 설정:
    - $H_{0}:\quad \forall i \quad \sigma_{i}^{2} / \sigma_{j \ne i}^{2} = 1$
    - $H_{1}:\quad \exists i \quad \sigma_{i}^{2} / \sigma_{j \ne i}^{2} \ne 1$

- 검정통계량(Test Statistic):

    $$\begin{aligned}
    F \sim \mathcal{F}(k-1, N-k)
    \end{aligned}$$

- **F 분포(F-Distribution)** : 서로 독립인 확률변수 $V_{1}\sim\chi^2(\nu_1),V_{2}\sim\chi^2(\nu_2)$ 간 비율로 구성되는 확률변수의 분포

    $$
    F=\frac{V_1/\nu_1}{V_2/\nu_2} \sim \mathcal{F}(\nu_1,\nu_2)
    $$

## Test Statistic
-----

$$\begin{aligned}
F = \frac{\text{SSB} / (k-1)}{\text{SSW} / (N-k)}
\end{aligned}$$

- SSB(`S`um of `S`quare `B`etween):

    $$
    \text{SSB}=\sum_{i=1}^{k}{N_{i}\left(\overline{Z}^{(i)}-\overline{Z}\right)^2} \sim \chi^2(k-1)
    $$

    - $\overline{Z}^{(i)}$ : $i$ 번째 집단에 대하여 그 절대편차 $$Z^{(i)}$$ 의 평균
    - $\overline{Z}$ : 모든 관측치 $X_{\forall}$ 에 대하여 그 절대편차 $$Z$$ 의 평균
    - $k$ : 표본 내 집단 갯수

- SSW(`S`um of `S`quare `W`ithin):

    $$
    \text{SSW}=\sum_{i=1}^{k}\sum_{j=1}^{N_{i}}{\left(Z^{(i)}_{j}-\overline{Z}^{(i)}\right)^2} \sim \chi^2(N-k)
    $$

    - $$Z^{(i)}_{j}=\vert X^{(i)}_{j}-\overline{X}^{(i)} \vert$$ : $$i$$ 번째 집단의 $$j$$ 번째 관측치 $$X^{(i)}_{j}$$ 의 절대편차
    - $\overline{Z}^{(i)}$ : $i$ 번째 집단에 대하여 그 절대편차 $$Z^{(i)}$$ 의 평균
    - $N$ : 표본 내 관측치 갯수
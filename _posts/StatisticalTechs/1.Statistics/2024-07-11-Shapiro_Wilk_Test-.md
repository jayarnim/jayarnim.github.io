---
order: 11
title: Shapiro-Wilk Test
date: 2024-07-11
categories: [STATISTICAL TECHS, 1.statistics]
tags: [Statistics, Design of Experiments, A/B Test, t-Test, Two Sample t-Test, Paired Sample t-Test, Student’s t-Dist.]
math: true
description: >-
    Based on the following lectures <br>
    (1) “Statistics (2018-1)” by Prof. Sang Ah Lee, Dept. of Economics, College of Economics & Commerce, Kookmin Univ. <br>
    (2) "Statistical Models and Application (2024-1)" by Prof. Yeo Jin Chung, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
    path: /_post_refer_img/StatisticalTechs/1.Statistics/Thumbnail.png
---

## Shapiro-Wilk Test
-----

- **정규성 검정(Shapiro-Wilk Test)**: 표본 순위와 표준정규분포에서 기대되는 순위 값의 선형 결합을 비교함으로써 표본이 정규 분포를 따르는지 여부를 검정하는 방법

- 귀무가설과 대립가설 설정:
    - $H_{0}:\quad X \sim N(\mu, \sigma^2)$
    - $H_{1}:\quad X \not\sim N(\mu, \sigma^2)$

- 검정통계량 정의:

    $$\begin{aligned}
    W
    &= \frac{\left(\sum_{i=1}^{n} \beta_{i} X_{i}\right)^2}{\sum_{i=1}^{n}\left(X_{i} - \overline{X}\right)^2}
    \end{aligned}$$

- 귀무가설 하 검정통계량의 분포 생성:

    $$\begin{aligned}
    W_{N} \sim f_{W_{N}}(W)
    \end{aligned}$$

- 표본의 검정통계량 $W_{\mathrm{obs}}$ 의 $\mathrm{p-value}$ 도출:

    $$\begin{aligned}
    \mathrm{p-value}
    = F_{W_{N}}(W_{\mathrm{obs}})
    = P(W \le W_{\mathrm{obs}})
    \end{aligned}$$

- 유의수준 $\alpha$ 하 결론:

    - $F_{W}(W) \le \alpha$ : $X \not\sim N(\mu, \sigma^2)$

        > 귀무가설이 참이라는 가정 하에 도출된 검정통계량보다 극단적인 실현값이 발생할 가능성이 현저히 낮다. 이는 귀무가설이 참이라는 가정 하에 표본이 실현될 가능성이 현저히 낮음을 의미한다. 따라서 유의수준 $\alpha$ 하 귀무가설을 기각한다.

    - $\alpha < F_{W}(W)$ : $X \sim N(\mu, \sigma^2)$

        > 귀무가설이 참이라는 가정 하에 도출된 검정통계량보다 극단적인 실현값이 발생할 가능성이 어느 정도 존재한다. 이는 귀무가설이 참이라는 가정 하에 표본이 실현될 가능성이 현저히 낮다고 볼 수 없음을 의미한다. 따라서 유의수준 $\alpha$ 하 귀무가설을 기각하지 않는다.

## Test Statistic
-----

$$\begin{aligned}
W
&= \frac{\left(\sum_{i=1}^{n} \beta_{i} X_{i}\right)^2}{\sum_{i=1}^{n}\left(X_{i} - \overline{X}\right)^2}
\end{aligned}$$

- $\mathbf{X}$ : 표본의 관측치 $X_{i}$ 를 크기에 따라 오름차순 정렬한 순위 통계량 벡터

    $$\begin{aligned}
    \mathbf{X}
    &= \begin{pmatrix}
    X_{1}&X_{2}&\cdots&X_{n}
    \end{pmatrix}^{T}
    \end{aligned}$$

- $\overline{X}$ : 표본평균

    $$\begin{aligned}
    \overline{X}
    &=\frac{1}{n}\sum_{i=1}^{n}{X_{i}}
    \end{aligned}$$

- $\mathbf{b}$ : 순위 통계량 벡터 $\mathbf{X}$ 의 계수 벡터

    $$\begin{aligned}
    \mathbf{b}
    &=\frac{\mathbf{m}^{T}\mathbb{V}^{-1}}{\Vert \mathbb{V}^{-1}\mathbf{m} \Vert}
    \end{aligned}$$

    - $\mathbf{m}$ : 기대 순위 통계량 벡터

        $$\begin{aligned}
        \mathbf{m}
        &=\begin{pmatrix}
        \mathbb{E}\left[X_{1}\right]&\mathbb{E}\left[X_{2}\right]&\cdots&\mathbb{E}\left[X_{n} \right]
        \end{pmatrix}^{T}
        \end{aligned}$$

    - $\mathbb{V}$ : 기대 순위 통계량의 공분산 행렬

        $$\begin{aligned}
        \mathbb{V}_{i,j}=\mathrm{Cov}\Big(\mathbb{E}\left[X_{i}\right],\mathbb{E}\left[X_{j}\right]\Big)
        \end{aligned}$$

## Generate Dist. of Test Stats
-----

1. 표준정규분포로부터 $n$ 개의 관측치로 구성된 표본을 반복적으로 생성

    $$\begin{aligned}
    \mathbf{Y}^{(k)}
    &= \begin{pmatrix} Y_{1}^{(k)}&Y_{2}^{(k)}&\cdots&Y_{n}^{(k)} \end{pmatrix}^{T} \quad \text{for} \quad Y^{(k)}_{i} \sim N(0,1)
    \end{aligned}$$

2. 표본 $\mathbf{Y}^{(1)},\mathbf{Y}^{(2)},\cdots$ 에 대하여 검정통계량 도출

    $$\begin{aligned}
    W^{(k)}
    &=\frac{\left(\sum_{i=1}^{k} \beta_{i} Y_{i}\right)^2}{\sum_{i=1}^{k}\left(Y_{i} - \overline{Y}\right)^2}
    \end{aligned}$$

3. $n$ 의 크기에 따른 $W$ 의 경험적 분포 도출

    $$\begin{aligned}
    W_{N} \sim f_{W_{N}}(W)
    \end{aligned}$$
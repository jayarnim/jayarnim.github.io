---
order: 11
title: Shapiro-Wilk Test
date: 2024-07-11
categories: [STATISTICAL TECHS, 1.statistics]
tags: [Statistics, A/B Test, t-Test, Two Sample t-Test, Paired Sample t-Test, Student’s t-Dist.]
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

- **정규성 검정(Shapiro-Wilk Test)**:

- **귀무가설과 대립가설 설정**
    - $H_{0}:\quad X \sim N(\mu, \sigma^2)$
    - $H_{1}:\quad X \not\sim N(\mu, \sigma^2)$

- **검정통계량 도출**

    $$
    W=\frac{\left(\sum_{i=1}^{n} \alpha_{i} X_{i}\right)^2}{\sum_{i=1}^{n}\left(X_{i} - \overline{X}\right)^2}
    $$

    - $\overrightarrow{X}$ : 표본의 관측치 $X_{i}$ 를 크기에 따라 오름차순 정렬한 순위 통계량 벡터

        $$\begin{aligned}
        \overrightarrow{X}
        =\begin{pmatrix} X_{1}&X_{2}&\cdots&X_{n} \end{pmatrix}^{T}
        \end{aligned}$$

        - $\overline{X}=\displaystyle\frac{1}{n}\sum_{i=1}^{n}{X_{i}}$ : 표본평균

    - $\overrightarrow{\alpha}$ : 순위 통계량 벡터 $\overrightarrow{X}$ 의 계수 벡터

        $$
        \overrightarrow{\alpha}=\displaystyle\frac{\overrightarrow{m}^{T}\mathbb{V}^{-1}}{\Vert \mathbb{V}^{-1}\overrightarrow{m} \Vert}
        $$

        - $\overrightarrow{m}$ : 기대 순위 통계량 벡터

            $$
            \overrightarrow{m}=\begin{pmatrix} E\left[X_{1}\right]&E\left[X_{2}\right]&\cdots&E\left[X_{n} \right]\end{pmatrix}^{T}
            $$

        - $\mathbb{V}$ : 기대 순위 통계량의 공분산 행렬

            $$
            \mathbb{V}_{i,j}=\text{Cov}\Big[E\left[X_{i}\right],E\left[X_{j}\right]\Big]
            $$

        - $\overrightarrow{m}^{T}\mathbb{V}^{-1}$ : $\mathbb{V}^{-1}$ 에 의해 선형 변환되어 상호 독립된 기대 순위 통계량 벡터
        - $\Vert \mathbb{V}^{-1}\overrightarrow{m} \Vert$ : 정규화 항

- **표본 $Y \sim N(0,1)$ 를 활용한 경험적 분포 생성**
    1. 표준정규분포로부터 $n$ 개의 관측치로 구성된 표본을 반복적으로 생성

        $$\begin{aligned}
        \overrightarrow{Y}^{(k)}
        =\begin{pmatrix} Y_{1}^{(k)}&Y_{2}^{(k)}&\cdots&Y_{k}^{(k)} \end{pmatrix}^{T} \quad \text{for}\; Y^{(k)}_{i} \sim N(0,1)
        \end{aligned}$$

    2. 각 표본에 대하여 검정통계량 도출

        $$
        W^{(k)}=\frac{\left(\sum_{i=1}^{k} \alpha_{i} Y_{i}\right)^2}{\sum_{i=1}^{k}\left(Y_{i} - \overline{Y}\right)^2}
        $$

    3. $n$ 의 크기에 따른 $W$ 의 경험적 분포 도출

        $$
        f_{W}:n \rightarrow W
        $$

    4. $W$ 의 경험적 분포에서 특정 $w$ 값보다 작거나 같은 값을 가질 확률 도출

        $$\begin{aligned}
        \text{p-value}
        &=F_{W}(w)\\
        &=P(W \le w)
        \end{aligned}$$

- **표본 $X$ 에 대한 검정통계량 $W$ 의 $\text{p-value}$ 와 유의수준 $\alpha$ 비교**
    - $F_{W}(W) \le \alpha$ : $X \not\sim N(\mu, \sigma^2)$

        > 귀무가설이 참이라는 가정 하에 도출된 검정통계량보다 극단적인 실현값이 발생할 가능성이 현저히 낮다. 이는 귀무가설이 참이라는 가정 하에 표본이 실현될 가능성이 현저히 낮음을 의미한다. 따라서 유의수준 $\alpha$ 하 귀무가설을 기각한다.

    - $\alpha < F_{W}(W)$ : $X \sim N(\mu, \sigma^2)$

        > 귀무가설이 참이라는 가정 하에 도출된 검정통계량보다 극단적인 실현값이 발생할 가능성이 어느 정도 존재한다. 이는 귀무가설이 참이라는 가정 하에 표본이 실현될 가능성이 현저히 낮다고 볼 수 없음을 의미한다. 따라서 유의수준 $\alpha$ 하 귀무가설을 기각하지 않는다.
---
order: 3
title: Factor Analysis
date: 2024-01-17
categories: [3.MACHINE LEARNING TECHS, 3.dimensionality reduction algorithm]
tags: [machine learning, unsupervised learning, feature engineering, dimensionality reduction, factor analysis]
math: true
description: >-
    Based on the lecture "Statistical Models and Application (2024-1)" by Prof. Yeo Jin Chung, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
    path: /_post_refer_img/3.ML/3.dimensionality_reduction/Thumbnail.jpg
---

## factor analysis
-----

- **요인 분석(Factor Analysis)**: 측정변수들은 기존에는 고나찰되지 않았으나 의미 있는 소수의 핵심 요인(Latent Factor)으로 요약하여 차원을 축소하는 방법

    - **탐색적 요인 분석(Exploratory Factor Analysis)**: 사전 가정 없이 측정변수와 잠재변수 간 관계를 탐색하는 방법
    - **확인적 요인 분석(Confirmatory Factor Analysis)**: 사전에 가정된 요인 모형에 대하여 측정변수와의 적합도를 검정하는 방법

- two tower model:

    $$\begin{gathered}
    \begin{bmatrix}
    x_{1,1}&x_{1,2}&\cdots&x_{1,P}\\
    x_{2,1}&x_{2,2}&\cdots&x_{2,P}\\
    \vdots&\vdots&\ddots&\vdots\\
    x_{N,1}&x_{N,2}&\cdots&x_{N,P}
    \end{bmatrix}
    =\begin{bmatrix}
    f_{1,1}&f_{1,2}\\
    f_{2,1}&f_{2,2}\\
    \vdots&\vdots\\
    f_{N,1}&f_{N,2}
    \end{bmatrix}
    \begin{bmatrix}
    \lambda_{1,1}&\lambda_{1,2}\\
    \lambda_{2,1}&\lambda_{2,2}\\
    \vdots&\vdots\\
    \lambda_{P,1}&\lambda_{P,2}\\
    \end{bmatrix}^{T}
    +\begin{bmatrix}
    u_{1,1}&u_{1,2}&\cdots&u_{1,P}\\
    u_{2,1}&u_{2,2}&\cdots&u_{2,P}\\
    \vdots&\vdots&\ddots&\vdots\\
    u_{N,1}&u_{N,2}&\cdots&u_{N,P}
    \end{bmatrix}\\
    \Updownarrow\\
    \mathbf{X}=\Lambda\mathbf{F}+\mathbf{U}
    \quad\mathrm{for}\quad
    f\perp u
    \end{gathered}$$

- **공통 요인(Common Factor)**:

    $$
    \mathbf{f}\sim\mathcal{N}(0,\mathbf{I})
    $$

- **특정 요인(Specific Factor)**: 공통 요인이 설명하지 못하는 측정변수의 무작위 변동

    $$
    \mathbf{u}\sim\mathcal{N}(0,\Psi\mathbf{I})
    $$

- **요인적재량(Factor Loading)**: 측정 변수와 공통 요인 간 관련도를 나타내는 값으로서, 통상 $0.3$ 이상이면 유의하다고 판단함

    $$
    \Lambda
    $$

- **공통성(Communality)**: 측정 변수 $X_{i}$ 의 분산 중 공통 요인에 의해 설명되는 분산의 비율

    $$\begin{aligned}
    \mathrm{Var}\left[X_{i}\right]
    &=\mathrm{Var}\left[\Lambda_{i}\mathbf{F}+\mathbf{U}_{i}\right]\\
    &=\Lambda_{1}^{2}+\Psi_{i}^{2}\\
    \\
    \therefore h_{i}^{2}
    &=\frac{\Lambda_{i}^{2}}{\Lambda_{i}^{2}+\Psi_{i}^{2}}
    \end{aligned}$$

## factor score estimation
-----

- **요인 점수(Factor Score)**: 개별 관측치들의 공통 요인 차원 사상값

    $$
    \hat{F}=\mathbf{W}\mathbf{X}
    $$

- definition:

    $$\begin{aligned}
    X
    &=\Lambda F+U\\
    \hat{F}
    &=\mathbb{E}\left[F\mid X\right]
    \end{aligned}$$

- multi-variate gaussian distribution application:

    $$\begin{gathered}
    \begin{bmatrix}
    F\\
    X
    \end{bmatrix}
    \sim\mathcal{N}\left(
    \begin{bmatrix}
    0\\
    0
    \end{bmatrix},
    \begin{bmatrix}
    \Sigma_{FF}&\Sigma_{FX}\\
    \Sigma_{XF}&\Sigma_{XX}
    \end{bmatrix}
    \right)\\
    \\
    \therefore \mathbb{E}\left[F\mid X\right]
    =\Sigma_{FX}\Sigma_{XX}^{-1}X
    \end{gathered}$$

- covariance:

    $$\begin{aligned}
    \mathrm{Cov}\left[F,F\right]
    &=\mathbf{I}\\
    \mathrm{Cov}\left[F,X\right]
    &=\Lambda^{T}\\
    \mathrm{Cov}\left[X,X\right]
    &=\Lambda\Lambda^{T}+\Psi\\
    \\
    \therefore \mathbb{E}\left[F\mid X\right]
    &=\underbrace{\Lambda^{T}\left(\Lambda\Lambda^{T}+\Psi\right)^{-1}}_{=W}X
    \end{aligned}$$

- woodbury-matrix identity application:

    $$\begin{aligned}
    (A+UCV)^{-1}
    &=A^{-1}-A^{-1}U\left(C^{-1}+VA^{-1}U\right)^{-1}VA^{-1}\\
    \\
    \therefore \left(\Lambda\Lambda^{T}+\Psi\right)^{-1}
    &=\Psi^{-1}-\Psi^{-1}\Lambda\left(I+\Lambda^{T}\Psi^{-1}\Lambda\right)^{-1}\Lambda^{T}\Psi^{-1}
    \end{aligned}$$

- therefore:

    $$
    W
    =\left(\Lambda^{T}\Psi^{-1}\Lambda+I\right)^{-1}\Lambda^{T}\Psi^{-1}
    $$

## factor rotation
-----

- **요인 회전(Factor Rotation)**: 요인적재량으로부터 측정 변수들이 어떤 요인에 해당하는지, 요인이 어떤 의미를 가지는지 판단하기에 애매모호한 경우, 측정변수의 공분산 구조를 훼손하지 않으면서 요인적재량을 구별하기 쉬운 직교행렬을 탐색하여 요인적재행렬을 선형변환하는 방법

    $$\begin{gathered}
    \Lambda\mapsto\Lambda M\quad\mathrm{for}\quad M^{T}M=I\\
    \\
    \begin{aligned}
    \therefore\Sigma_{XX}
    &=\Lambda\Lambda^{T}+\Psi\\
    &=\Lambda\left(MM^{T}\right)\Lambda^{T}+\Psi\\
    &=\left(\Lambda M\right)\left(M^{T}\Lambda^{T}\right)+\Psi\\
    &=\left(\Lambda M\right)\left(\Lambda M\right)^{T}+\Psi\\
    \end{aligned}
    \end{gathered}$$

    - 교차 적재 문제(Cross-Loading): 요인 해석 및 독립성 문제
    - 데이터 셋이 요인 구조가 아닌 경우
    - 요인의 설명력이 약한 경우(요인적재량이 $0$ 근처에 몰려 있는 경우)

- **직교 회전(Orthogonal Rotation)**: 회전된 요인들이 서로 상관되지 않도록(선형 변환 공간이 직교하도록) 제약하는 회전

    $$
    M^{T}M=I
    $$

    - **Varimax Rotation**: 한 공통요인에 대하여 각 측정변수가 가지는 요인적재량 크기(자승)의 분산이 최대가 되도록 변환하는 방법으로서, 요인적재행렬의 열의 분산을 최대화하는 방법

        $$
        V=\sum_{j=1}^{m}\left[\frac{1}{p}\sum_{i=1}^{p}{\left(\gamma_{i,j}\right)^{4}}-\left(\frac{1}{p}\sum_{i=1}^{p}{\left(\gamma_{i,j}\right)^{2}}\right)^{2}\right]
        $$

    - **Quartimax Rotation**: 한 측정변수에 대하여 각 측정변수가 가지는 요인적재량 크기(자승)의 분산이 최대가 되도록 변환하는 방법으로서, 요인적재행렬의 열의 분산을 최대화하는 방법

        $$
        Q=\sum_{i=1}^{p}\left[\frac{1}{m}\sum_{j=1}^{m}{\left(\gamma_{i,j}\right)^{4}}-\left(\frac{1}{m}\sum_{j=1}^{m}{\left(\gamma_{i,j}\right)^{2}}\right)^{2}\right]
        $$

- **사각 회전(Obique Rotation)**: 요인 공간의 직교 제약을 완화하여 요인 간 상관성을 허용하는 회전

    $$
    M^{T}M\ne I
    $$

    - **Oblinmin Rotation**: 측정 변수의 다요인 교차 부하(cross loading term)를 최소화하도록 변환하는 방법

        $$
        \mathcal{L}(\gamma\mid\delta)
        =\sum_{i=1}^{p}\left[\underbrace{\sum_{j=1}^{m}{\left(\gamma_{i,j}\right)^{2}}\sum_{k\ne j}{\left(\gamma_{i,k}\right)^{2}}}_{\text{cross-loading term}}+\underbrace{\delta\left(\sum_{j=1}^{m}{\left(\gamma_{i,j}\right)^{2}}\right)^{2}}_{\text{delta param term}}\right]
        $$

        - $\delta=0$: qualtimin rotation
        - $\delta<0$: more oblique
        - $\delta>0$: more orthogonal

    - **Promax Rotation**: Varimax Rotation $\gamma$ 을 그 승수 변환(Power Transform)과 유사하도록 재변환하는 방법

        $$
        \min_{M}\left\Vert\gamma M-\gamma^{k}\right\Vert^{2}
        $$
---
order: 6
title: Regression Diagnostics (3) Multicollinearity
date: 2024-07-20
categories: [2.STATISTICAL TECHS, 3.regression analysis]
tags: [statistics, regression analysis, linear regression analysis, numerical data analysis]
math: true
description: >-
    Based on the following lectures <br>
    (1) “Statistics (2018-1)” by Prof. Sang Ah Lee, Dept. of Economics, College of Economics & Commerce, Kookmin Univ. <br>
    (2) “Intro. to Machine Learning (2023-2)” by Prof. Je Hyuk Lee, Dept. of Data Science, The Grad. School, Kookmin Univ. <br>
    (3) "Statistical Models and Application (2024-1)" by Prof. Yeo Jin Chung, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
    path: /_post_refer_img/2.STATS/3.regression_analysis/Thumbnail.jpg
---

## Regression Diagnostics
-----

- `A.1` **반응변수와 설명변수 간 비선형성 문제(Non-Linearity Problem)**: 반응변수의 조건부 기대값이 설명변수들의 선형 결합 형태가 아님에 따라 계수 벡터의 최소자승추정량이 불편추정량이 될 수 없는 문제

    $$
    \cancel{\exists}\beta\in\mathbb{R}^{P}
    \quad\mathrm{s.t.}\quad
    \mathbb{E}\left[\mathbf{y}\mid\mathbf{X}\right]
    =\mathbf{X}\beta
    $$

- `A.2` **오차항의 이분산성 문제(Hetero-Scedasticity Problem)**: 오차항의 등분산 가정이 위배됨에 따라 계수 벡터의 최소자승추정량이 효율추정량이 될 수 없는 문제

    $$
    \exists i\ne j:\mathrm{Var}\left[\varepsilon_{i}\mid\mathbf{X}\right]\ne\mathrm{Var}\left[\varepsilon_{j}\mid\mathbf{X}\right]\\
    \Updownarrow\\
    \mathrm{Var}\left[\varepsilon\mid\mathbf{X}\right]
    =\mathrm{diag}(\sigma_{1}^{2},\cdots,\sigma_{N}^{2})\ne\sigma^{2}\mathbf{I}
    $$

- `A.3` **오차항의 자기상관 문제(Auto-Correlation Problem)**: 오차항의 자기상관이 존재함에 따라 계수 벡터의 최소자승추정량이 효율추정량이 될 수 없는 문제

    $$
    \exists i\ne j:\mathrm{Cov}\left[\varepsilon_{i},\varepsilon_{j}\mid \mathbf{X}\right]\ne 0
    \quad\Longleftrightarrow\quad
    \mathrm{Var}\left[\varepsilon\mid\mathbf{X}\right]\ne\sigma^{2}\mathbf{I}
    $$

- `A.5` **설명변수 간 다중공선성 문제(Multi-Col-Linearity Problem)**: 설명변수들이 선형 종속됨에 따라 계수 벡터가 유일하게 결정되지 못하는 문제
    
    $$
    \mathrm{rank}(\mathbf{X})\ne p \quad\mathrm{for}\quad\mathbf{X}\in\mathbb{R}^{N\times P}
    $$

## Unique Solution
-----

- 정규 방정식:

    $$\begin{aligned}
    \hat{\beta}=\left(\mathbf{X}^{T}\mathbf{X}\right)^{-1}\mathbf{X}\mathbf{y}\quad\mathrm{s.t.}\quad\mathrm{det}\left(\mathbf{X}^{T}\mathbf{X}\right)\ne 0
    \end{aligned}$$

- 정규 행렬의 고유값 분해:

    $$\begin{aligned}
    \mathbf{X}^{T}\mathbf{X}
    &=\mathbf{Q}\Lambda\mathbf{Q}^{T}
    \end{aligned}$$

    - $\mathbf{Q}$: 고유벡터 행렬

        $$\begin{aligned}
        \mathbf{Q}
        =\begin{pmatrix}
        |&|&|\\
        \mathbf{q}_{1}&\cdots&\mathbf{q}_{p}\\
        |&|&|
        \end{pmatrix},
        \quad\mathbf{Q}^{T}\mathbf{Q}=\mathbf{I}
        \end{aligned}$$

    - $\Lambda$: 고유값 대각행렬

        $$\begin{aligned}
        \Lambda=\mathrm{diag}(\lambda_{1},\cdots,\lambda_{p})
        \end{aligned}$$

- 행렬식 전개:

    $$\begin{aligned}
    \mathrm{det}\left(\mathbf{X}^{T}\mathbf{X}\right)
    &=\mathrm{det}\left(\mathbf{Q}\Lambda\mathbf{Q}^{T}\right)\\
    &=\mathrm{det}\left(\mathbf{Q}\right)\mathrm{det}\left(\Lambda\right)\mathrm{det}\left(\mathbf{Q}^{T}\right)\\
    &=\vert 1\vert\mathrm{det}\left(\Lambda\right)\vert 1\vert\quad(\because\text{$\mathbf{Q}$ is orthogonal})\\
    &=\prod_{i=1}^{p}{\lambda_{i}}\quad(\because\text{$\Lambda$ is diagonal})
    \end{aligned}$$

- 따라서 정규 행렬의 고유값이 모두 $0$ 이 아닐 때에만 계수 벡터의 해가 유일하게 결정됨:

    $$\begin{aligned}
    \exists! \hat{\beta}\quad\mathrm{s.t.}\quad\forall\lambda\ne 0
    \end{aligned}$$

## Multi-Col-Linearity Problem
-----

- 고유값이 $0$ 인 고유벡터가 존재한다고 하자:

    $$
    \lambda=0\quad\Longleftrightarrow\quad \left(\mathbf{X}^{T}\mathbf{X}\right)\mathbf{q}=\mathbf{0},\quad\mathbf{q}\ne\mathbf{0}
    $$

- algebraic manipulation:

    $$\begin{aligned}
    \left(\mathbf{X}^{T}\mathbf{X}\right)\mathbf{q}
    &=\mathbf{0}\\
    \mathbf{q}^{T}\left(\mathbf{X}^{T}\mathbf{X}\right)\mathbf{q}
    &=\mathbf{0}\\
    \left(\mathbf{q}^{T}\mathbf{X}^{T}\right)\mathbf{X}\mathbf{q}
    &=\mathbf{0}\\
    \left(\mathbf{X}\mathbf{q}\right)^{T}\mathbf{X}\mathbf{q}
    &=\mathbf{0}\\
    \therefore \Vert\mathbf{X}\mathbf{q}\Vert^{2}
    &=0
    \end{aligned}$$

- 유클리드 노름이 $0$ 인 벡터는 영벡터임:

    $$
    \mathbf{X}\mathbf{q}=q_{1}\mathbf{x}_{1}+\cdots+q_{p}\mathbf{x}_{p}=0
    $$

- 따라서 설명변수들이 선형 종속인 경우 계수 벡터의 해는 유일하지 않음:

    $$
    \exists\mathbf{q}\ne\mathbf{0}:\mathbf{X}\mathbf{q}=0\quad\Longrightarrow\quad\cancel{\exists!}\hat{\beta}
    $$

## Geometric Interpretation
-----

### concept

- **그람 행렬(Gram Matrix)**: 어떤 공간에서 데이터가 분산하고 있는 고유한 방향으로 벡터를 선형변환하는 행렬로서, 그 고유벡터는 분산하는 축을, 고유값은 해당 축으로의 정보량(분산)을 나타냄

    $$
    \left(\langle\mathbf{x}_{i},\mathbf{x}_{j}\rangle\right)_{(i,j)}
    $$

- **정규 행렬(Normal Matrix)**: 설명변수들의 내적으로 구성된 그람 행렬로서 변수 공간에서의 데이터 분산 구조를 나타냄

    $$
    G:=\mathbf{X}^{T}\mathbf{X} \in \mathbb{R}^{P\times P}
    $$

    - **변수 공간(Variable Space)**: 실수 성분(샘플)들을 축으로, 변수를 구성 원소로 구성되는 공간

        $$
        \mathbf{x}_{j}=(x_{1,j},\cdots,x_{n,j})\in\mathbb{R}^{N}
        $$

- **커널 행렬(Kernel Matrix)**: 샘플들의 내적으로 구성된 그람 행렬로서 샘플 공간에서의 데이터 분산 구조를 나타냄

    $$
    K:=\mathbf{X}\mathbf{X}^{T} \in \mathbb{R}^{N\times N}
    $$

    - **샘플 공간(Sample Space)**: 변수들을 축으로, 샘플을 구성 원소로 구성되는 공간

        $$
        \mathbf{x}_{i}=(x_{i,1},\cdots,x_{i,p})\in\mathbb{R}^{P}
        $$

- **설계 행렬(Design Matrix)**: $\mathbf{X}\in\mathbb{R}^{N\times P}$ 는 변수 공간의 벡터를 샘플 공간으로 사상하는 선형 변환

    $$
    \mathbf{X}:\mathbb{R}^{P}\to\mathbb{R}^{N},\quad \mathbf{v}\mapsto\mathbf{X}\mathbf{v}
    $$

### interpretation

- 정규 행렬 $G$ 의 고유벡터 $\mathbf{q}$ 의 선형 변환 $\mathbf{X}\mathbf{q}$, 즉 설명변수들의 선형 결합은 커널 행렬 $K$ 의 고유벡터로서, 샘플 공간에서 데이터가 분산하는 고유한 방향을 나타냄:

    $$\begin{aligned}
    \underbrace{\left(\mathbf{X}^{T}\mathbf{X}\right)}_{=:G}\mathbf{q}
    &=\lambda\mathbf{q}\\
    \mathbf{X}\left(\mathbf{X}^{T}\mathbf{X}\right)\mathbf{q}
    &=\lambda\mathbf{X}\mathbf{q}\\
    \underbrace{\left(\mathbf{X}\mathbf{X}^{T}\right)}_{=:K}\left(\mathbf{X}\mathbf{q}\right)
    &=\lambda\left(\mathbf{X}\mathbf{q}\right)
    \end{aligned}$$

- 설명변수들이 선형 종속임은 샘플 공간에서 데이터가 분산하는 특정 방향으로의 크기가 $0$ 임을 나타냄:

    $$
    \mathbf{X}\mathbf{q}=0\quad\Longleftrightarrow\quad\lambda=0
    $$

- 이는 변수 공간에서 데이터가 분산하는 $P$ 개의 축 중 $P-1$ 개의 축에 대해서만 계수 벡터의 성분을 특정할 수 있고 나머지 한 축에 대해서는 특정할 수 없음을 의미함:

    $$
    \exists\mathbf{q}\ne\mathbf{0}:\left(\mathbf{X}^{T}\mathbf{X}\right)\mathbf{q}=\lambda\mathbf{q}=0
    $$

- 따라서 계수 벡터를 해당 방향으로 임의 조정하더라도($\beta\to\beta+t\mathbf{q}$) 그 방향의 효과가 식별되지 않게 됨:

    $$\begin{aligned}
    \mathbf{X}\left(\beta+t\mathbf{q}\right)
    =\mathbf{X}\beta+t\mathbf{X}\mathbf{q}
    =\mathbf{X}\beta
    \end{aligned}$$

## VIF
-----

- **분산팽창계수(`V`ariance `I`nflation `F`actor)**: 변동성을 기준으로 $k$ 번째 설명변수의 다중공선성을 측정하는 지표

    $$\begin{aligned}
    \mathrm{VIF}_k
    &= \frac{1}{1-R_{k}^{2}}
    \end{aligned}$$

- $k$ 번째 설명변수에 대한 보조회귀모형:

    $$\begin{aligned}
    \mathbf{x}_{k}
    &=\mathbf{X}_{-k}^{T}\gamma,\quad\mathbf{X}_{-k}:=[\mathbf{x}_{1},\cdots,\mathbf{x}_{k-1},\mathbf{x}_{k+1},\cdots,\mathbf{x}_{p}]\in\mathbb{R}^{N\times(P-1)}
    \end{aligned}$$

- 보조회귀모형의 결정계수:

    $$\begin{aligned}
    R_{k}^{2}
    =1 - \frac{\mathrm{RSS}_{k}}{\mathrm{TSS}_{k}}
    =1 - \frac{\sum_{i=1}^{n}{\epsilon_{i}^{2}}}{\sum_{i=1}^{n}{\left(x_{i,k}-\overline{x}_{k}\right)^{2}}}
    \end{aligned}$$
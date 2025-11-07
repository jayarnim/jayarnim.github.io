---
order: 5
title: Regression Diagnostics (2) Error Terms
date: 2024-07-19
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

  $$\begin{aligned}
  \exists i\ne j:\mathrm{Var}\left[\varepsilon_{i}\mid\mathbf{X}\right]\ne\mathrm{Var}\left[\varepsilon_{j}\mid\mathbf{X}\right]\\
  \Updownarrow\\
  \mathrm{Var}\left[\varepsilon\mid\mathbf{X}\right]
  =\mathrm{diag}(\sigma_{1}^{2},\cdots,\sigma_{N}^{2})\ne\sigma^{2}\mathbf{I}
  \end{aligned}$$

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

## Normal Equation
-----

- objective function:

    $$\begin{aligned}
    \mathcal{L}_{GLS}
    &=\left(\mathbf{y}-\mathbf{X}\beta\right)^{T}\Sigma^{-1}\left(\mathbf{y}-\mathbf{X}\beta\right)\quad\mathrm{for}\quad\varepsilon\mid\mathbf{X}\sim\mathcal{N}(0,\Sigma)\\
    &=\frac{1}{\sigma^{2}}\left(\mathbf{y}-\mathbf{X}\beta\right)^{T}\left(\mathbf{y}-\mathbf{X}\beta\right)\quad\mathrm{s.t.}\quad\Sigma=\sigma^{2}\mathbf{I}\\
    &\approx\Vert\mathbf{y}-\mathbf{X}\beta\Vert^{2}
    \end{aligned}$$

- normal equation:

    $$\begin{aligned}
    \hat{\beta}_{GLS}
    &=\left(\mathbf{X}^{T}\Sigma^{-1}\mathbf{X}\right)^{-1}\mathbf{X}^{T}\Sigma^{-1}\mathbf{y}\quad\mathrm{for}\quad\varepsilon\mid\mathbf{X}\sim\mathcal{N}(0,\Sigma)\\
    &=\frac{1}{\sigma^{2}}\left(\frac{1}{\sigma^{2}}\mathbf{X}^{T}\mathbf{X}\right)^{-1}\mathbf{X}^{T}\mathbf{y}\quad\mathrm{s.t.}\quad\Sigma=\sigma^{2}\mathbf{I}\\
    &=\left(\mathbf{X}^{T}\mathbf{X}\right)^{-1}\mathbf{X}^{T}\mathbf{y}
    \end{aligned}$$

- therefore GLS is equivalent to OLS under assumptions on the covariance structure of the error term:

    $$\begin{aligned}
    \hat{\beta}_{GLS}
    &=\left(\mathbf{X}^{T}\Sigma^{-1}\mathbf{X}\right)^{-1}\mathbf{X}^{T}\Sigma^{-1}\mathbf{y}\quad\mathrm{for}\quad\varepsilon\mid\mathbf{X}\sim\mathcal{N}(0,\Sigma)\\
    &=\left(\mathbf{X}^{T}\mathbf{X}\right)^{-1}\mathbf{X}^{T}\mathbf{y}\quad\mathrm{s.t.}\quad\Sigma=\sigma^{2}\mathbf{I}\\
    &=\hat{\beta}_{OLS}
    \end{aligned}$$

### GLS

- **GLS(`G`eneralized `L`east `S`quares)**: 오차항의 마할라노비스 거리의 자승, 즉 정밀도 행렬로써 가중된 오차항의 자승을 최소화하는 계수 벡터의 해

    $$\begin{aligned}
    \hat{\beta}
    &=\mathrm{arg}\min_{\beta}{\left(\mathbf{y}-\mathbf{X}\beta\right)^{T}\Sigma^{-1}\left(\mathbf{y}-\mathbf{X}\beta\right)}\\
    &=\left(\mathbf{X}^{T}\Sigma^{-1}\mathbf{X}\right)^{-1}\mathbf{X}^{T}\Sigma^{-1}\mathbf{y}\quad\mathrm{s.t.}\quad\varepsilon\sim\mathcal{N}(0,\Sigma)
    \end{aligned}$$

- conditional expectation:

    $$\begin{aligned}
    \mathbb{E}\left[\hat{\beta}\mid\mathbf{X}\right]
    &=\left(\mathbf{X}^{T}\Sigma^{-1}\mathbf{X}\right)^{-1}\mathbf{X}^{T}\Sigma^{-1}\mathbb{E}\left[\mathbf{y}\mid\mathbf{X}\right]\\
    &=\left(\mathbf{X}^{T}\Sigma^{-1}\mathbf{X}\right)^{-1}\mathbf{X}^{T}\Sigma^{-1}\mathbf{X}\beta\\
    &=\left(\mathbf{X}^{T}\Sigma^{-1}\mathbf{X}\right)^{-1}\left(\mathbf{X}^{T}\Sigma^{-1}\mathbf{X}\right)\beta\\
    &=\beta
    \end{aligned}$$

- conditional variance:

    $$\begin{aligned}
    \mathrm{Var}\left[\hat{\beta}\mid\mathbf{X}\right]
    &=\mathrm{Var}\left[\left(\mathbf{X}^{T}\Sigma^{-1}\mathbf{X}\right)^{-1}\mathbf{X}^{T}\Sigma^{-1}\mathbf{y}\mid\mathbf{X}\right]\\
    &=\left(\mathbf{X}^{T}\Sigma^{-1}\mathbf{X}\right)^{-1}\mathbf{X}^{T}\Sigma^{-1}\mathrm{Var}\left[\mathbf{y}\mid\mathbf{X}\right]\left[\left(\mathbf{X}^{T}\Sigma^{-1}\mathbf{X}\right)^{-1}\mathbf{X}^{T}\Sigma^{-1}\right]^{T}\\
    &=\left(\mathbf{X}^{T}\Sigma^{-1}\mathbf{X}\right)^{-1}\mathbf{X}^{T}\Sigma^{-1}\Sigma\Sigma^{-1}\mathbf{X}\left(\mathbf{X}^{T}\Sigma^{-1}\mathbf{X}\right)^{-1}\quad(\because(\Sigma^{-1})^{T}=\Sigma^{-1})\\
    &=\left(\mathbf{X}^{T}\Sigma^{-1}\mathbf{X}\right)^{-1}\left(\mathbf{X}^{T}\Sigma^{-1}\mathbf{X}\right)\left(\mathbf{X}^{T}\Sigma^{-1}\mathbf{X}\right)^{-1}\\
    &=\left(\mathbf{X}^{T}\Sigma^{-1}\mathbf{X}\right)^{-1}
    \end{aligned}$$

### OLS

- **OLS(`O`rdinary `L`east `S`quares)**: 오차항의 유클리드 거리의 자승, 즉 오차항의 자승을 최소화하는 계수 벡터의 해

    $$\begin{aligned}
    \hat{\beta}
    &=\mathrm{arg}\min_{\beta}{\Vert\mathbf{y}-\mathbf{X}\beta\Vert^{2}}\\
    &=\left(\mathbf{X}^{T}\mathbf{X}\right)^{-1}\mathbf{X}^{T}\mathbf{y}\quad\mathrm{s.t.}\quad\varepsilon\sim\mathcal{N}(0,\sigma^{2}\mathbf{I})
    \end{aligned}$$

- conditional expectation:

    $$\begin{aligned}
    \mathbb{E}\left[\hat{\beta}\mid\mathbf{X}\right]
    &=\left(\mathbf{X}^{T}\mathbf{X}\right)^{-1}\mathbf{X}^{T}\mathbb{E}\left[\mathbf{y}\mid\mathbf{X}\right]\\
    &=\left(\mathbf{X}^{T}\mathbf{X}\right)^{-1}\mathbf{X}^{T}\mathbf{X}\beta\\
    &=\left(\mathbf{X}^{T}\mathbf{X}\right)^{-1}\left(\mathbf{X}^{T}\mathbf{X}\right)\beta\\
    &=\beta
    \end{aligned}$$

- conditional variance:

    $$\begin{aligned}
    \mathrm{Var}\left[\hat{\beta}\mid\mathbf{X}\right]
    &=\mathrm{Var}\left[\left(\mathbf{X}^{T}\mathbf{X}\right)^{-1}\mathbf{X}^{T}\mathbf{y}\mid\mathbf{X}\right]\\
    &=\left(\mathbf{X}^{T}\mathbf{X}\right)^{-1}\mathbf{X}^{T}\mathrm{Var}\left[\mathbf{y}\mid\mathbf{X}\right]\left[\left(\mathbf{X}^{T}\mathbf{X}\right)^{-1}\mathbf{X}^{T}\right]^{T}\\
    &=\sigma^{2}\left(\mathbf{X}^{T}\mathbf{X}\right)^{-1}\mathbf{X}^{T}\mathbf{X}\left(\mathbf{X}^{T}\mathbf{X}\right)^{-1}\\
    &=\sigma^{2}\left(\mathbf{X}^{T}\mathbf{X}\right)^{-1}
    \end{aligned}$$

## Error Term Problem
-----

- 오차항의 공분산 구조가 등분산 가정과 자기상관 없음 가정을 만족하지 못한다고 하자:

    $$
    \varepsilon\mid\mathbf{X}\sim\mathcal{N}(0,\Sigma),\quad\Sigma\ne\sigma^{2}\mathbf{I}
    $$

- OLS 는 여전히 선형불편추정량임:

    $$\begin{aligned}
    \mathbb{E}\left[\hat{\beta}\mid\mathbf{X}\right]
    &=\left(\mathbf{X}^{T}\mathbf{X}\right)^{-1}\mathbf{X}^{T}\mathbb{E}\left[\mathbf{y}\mid\mathbf{X}\right]\\
    &=\left(\mathbf{X}^{T}\mathbf{X}\right)^{-1}\mathbf{X}^{T}\mathbf{X}\beta\\
    &=\left(\mathbf{X}^{T}\mathbf{X}\right)^{-1}\left(\mathbf{X}^{T}\mathbf{X}\right)\beta\\
    &=\beta
    \end{aligned}$$

- OLS 의 조건부 분산:

    $$\begin{aligned}
    \mathrm{Var}\left[\hat{\beta}\mid\mathbf{X}\right]
    &=\mathrm{Var}\left[\left(\mathbf{X}^{T}\mathbf{X}\right)^{-1}\mathbf{X}^{T}\mathbf{y}\mid\mathbf{X}\right]\\
    &=\left(\mathbf{X}^{T}\mathbf{X}\right)^{-1}\mathbf{X}^{T}\mathrm{Var}\left[\mathbf{y}\mid\mathbf{X}\right]\left[\left(\mathbf{X}^{T}\mathbf{X}\right)^{-1}\mathbf{X}^{T}\right]^{T}\\
    &=\left(\mathbf{X}^{T}\mathbf{X}\right)^{-1}\mathbf{X}^{T}\Sigma\mathbf{X}\left(\mathbf{X}^{T}\mathbf{X}\right)^{-1}
    \end{aligned}$$

- OLS 는 최소분산성을 만족할 수 없음:

    $$
    \underbrace{\left(\mathbf{X}^{T}\Sigma^{-1}\mathbf{X}\right)^{-1}}_{\text{GLS Variance}}\le\underbrace{\left(\mathbf{X}^{T}\mathbf{X}\right)^{-1}\mathbf{X}^{T}\Sigma\mathbf{X}\left(\mathbf{X}^{T}\mathbf{X}\right)^{-1}}_{\text{OLS Variance}}
    $$
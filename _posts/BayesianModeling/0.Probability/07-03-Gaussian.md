---
order: 3
title: Gaussian Distribution and Variations
date: 2025-07-03
categories: [BAYES, 0.probability]
tags: [Distribution, Continuous Variable, Gaussian Dist., Normal Dist., Multi-Variate Gaussian Dist., Multi-Variate Normal Dist., Student t Dist., Log Gaussian Dist., Log Normal Dist.]
math: true
description: >-
    Based on the following lectures <br>
    (1) “Statistics (2018-1)” by Prof. Sang Ah Lee, Dept. of Economics, College of Economics & Commerce, Kookmin Univ. <br>
    (2) "Statistical Models and Application (2024-1)" by Prof. Yeo Jin Chung, Dept. of Data Science, The Grad. School, Kookmin Univ. <br>
    (3) “Bayesian Modeling (2024-1)” by Prof. Yeo Jin Chung, Dept. of AI, Big Data & Management, College of Business Administration, Kookmin Univ.
image:
    path: /_post_refer_img/BayesianModeling/0.Probability/Thumbnail.jpg
---

## Gaussian Dist.
-----

## Multi-Variate Gaussian Dist.
-----

### Multi-Variate Gaussian Dist.

- **다변량 가우시안 분포(`M`ulti-`V`ariate Gaussian/`N`ormal Distribution; MVN)** : 유한 차원의 상관된 가우시안 확률변수 벡터에 대해 정의되는 가우시안 분포

    ![02](/_post_refer_img/BayesianModeling/0.Probability/01-02.png){: width="100%"}

- **Definition**

    $$\begin{aligned}
    \mathbf{X} \sim \mathcal{N}\left(\mu, \Sigma\right)
    \end{aligned}$$

    - $$\mathbf{X}= \begin{pmatrix}X_{1} & X_{2} & \cdots & X_{N}\end{pmatrix}^{T}$$ : Multi-Variable

        - $$X_{i} \sim \mathcal{N}\left(\mu_{i}, \sigma_{i}^{2}\right)$$ : The elements are random variables that follow individual Gaussian dist.

    - $$\mu=\begin{pmatrix}\mu_{1} & \mu_{2} & \cdots & \mu_{N}\end{pmatrix}^{T}$$ : Mean Vector
    - $$\Sigma=\begin{pmatrix}\Sigma_{11} & \Sigma_{12} & \cdots & \Sigma_{1N}\\ \Sigma_{21} & \Sigma_{22} & \cdots & \Sigma_{2N}\\ \vdots & \vdots & \ddots & \vdots\\ \Sigma_{N1} & \Sigma_{N2} & \cdots & \Sigma_{NN} \end{pmatrix}$$ : Covariance Matrix

- **Probability Density Function**

    $$\begin{aligned}
    f(\mathbf{X})
    &= \frac{1}{(2\pi)^{n/2} \vert \Sigma \vert^{1/2}} \exp{\left[-\frac{1}{2}\underbrace{(\mathbf{X}-\mu)^{T}\Sigma^{-1}(\mathbf{X}-\mu)}_{\text{Mahalanobis Distance}}\right]}
    \end{aligned}$$

- **마할라노비스 거리(Mahalanobis Distance)** : 상관관계가 존재하는 다변량 데이터에서, 하나의 데이터 포인트가 특정 분포 혹은 군집에서 얼마나 떨어져 있는지를 측정하는 개념으로서, 단순 좌표 상의 거리뿐만 아니라 데이터 분포(분산-공분산 구조)를 반영하여 측정함

    $$\begin{aligned}
    D_{M}(x)
    &= \sqrt{(x-\mu)^{T}\Sigma^{-1}(x-\mu)}
    \end{aligned}$$

    - $\sqrt{(x-\mu)^{T}(x-\mu)}$ : 데이터 포인트와 특정 분포 중심점 간 편차로서 유클리드 거리
    - $\Sigma$ : 특정 분포의 공분산 행렬로서 데이터의 분산과 변수 간 상관관계를 포함하며, 이를 반영하여 방향성과 크기에 따라 거리를 조정함

### Conditional Probability

$$\begin{aligned}
Z_{2} \mid Z_{1} \sim \mathcal{N}\left(\mu_{2} + \Sigma_{21}\Sigma_{11}^{-1}(Z_{1}-\mu_{1}), \Sigma_{22}-\Sigma_{21}\Sigma_{11}^{-1}\Sigma_{12}\right)
\end{aligned}$$

- Multi-Variate Gaussian Dist.

    $$\begin{aligned}
    \mathbf{Z}=\begin{bmatrix}Z_{1} \\ Z_{2}\end{bmatrix} \sim \mathcal{N}\left(\begin{bmatrix}\mu_{1} \\ \mu_{2}\end{bmatrix}, \begin{bmatrix}\Sigma_{11} & \Sigma_{12}\\ \Sigma_{21} & \Sigma_{22}\end{bmatrix}\right)
    \end{aligned}$$

- Probability Density Function

    $$\begin{aligned}
    f(\mathbf{Z})
    &= \frac{1}{(2\pi)^{n/2} \vert \Sigma \vert^{1/2}} \exp{\left[-\frac{1}{2}\underbrace{(\mathbf{Z}-\mu)^{T}\Sigma^{-1}(\mathbf{Z}-\mu)}_{\text{Mahalanobis Distance}}\right]}
    \end{aligned}$$

- Inv-Covariance Matrix

    $$\begin{aligned}
    \Sigma^{-1}
    &= \begin{bmatrix}
    \Sigma_{11}^{-1}+\Sigma_{11}^{-1}\Sigma_{12} \cdot \mathbf{M} \cdot \Sigma_{12}\Sigma_{11}^{-1} & -\Sigma_{11}^{-1}\Sigma_{12}\mathbf{M}\\
    -\mathbf{M}\Sigma_{21}\Sigma_{11}^{-1} & \mathbf{M}
    \end{bmatrix}
    \end{aligned}$$

    - $$\mathbf{M}=\left(\Sigma_{22}-\Sigma_{21}\Sigma_{11}^{-1}\Sigma_{12}\right)^{-1}$$ : Schur Complement

- Exponent Formula Expansion

    $$\begin{aligned}
    (\mathbf{Z}-\mu)^{T}\Sigma^{-1}(\mathbf{Z}-\mu)
    &= \underbrace{(Z_{1}-\mu_{1})^{T}\Sigma_{11}^{-1}(Z_{1}-\mu_{1})}_{\text{Mahalanobis Distance of } Z_{1}}\\
    &\quad + \underbrace{\Bigg[Z_{2}-\bigg\{\mu_{2}+\Sigma_{21}\Sigma_{11}^{-1}(Z_{1}-\mu_{1})\bigg\}\Bigg]^{T}\mathbf{M}\Bigg[Z_{2}-\bigg\{\mu_{2}+\Sigma_{21}\Sigma_{11}^{-1}(Z_{1}-\mu_{1})\bigg\}\Bigg]}_{\text{Conditional Mahalanobis Distance of }Z_{2} \mid Z_{1}}
    \end{aligned}$$

- Therefore,

    $$\begin{aligned}
    \text{E}\left[Z_{2} \mid Z_{1}\right]
    &= \mu_{2} + \Sigma_{21}\Sigma_{11}^{-1}(Z_{1}-\mu_{1})\\
    \text{Var}\left[Z_{2} \mid Z_{1}\right]
    &= \Sigma_{22}-\Sigma_{21}\Sigma_{11}^{-1}\Sigma_{12}
    \end{aligned}$$

## Log Gaussian Dist.
-----

## Student t Dist.
-----

> **모분산 $\sigma^2$ 을 모르는 경우** 표본평균 $\overline{X}$ 에 대하여 가설검정 시 우선 표본분산 $S^2$ 을 활용하여 모분산 $\sigma^2$ 을 추정해야 함. 추정된 모분산으로 도출된 검정통계량은 자유도 $\nu$ 에 따라 그 폭이 상이한 분포를 따르게 됨. 이처럼 자유도에 따라 변화하는 분산의 변동성을 반영하기 위해 표준정규분포 $Z \sim N(0,1)$ 대신 스튜던트 t 분포 $T \sim t(\nu)$ 를 사용함.

- **스튜던트 t 분포($t(\nu)$)** : 표준정규분포를 따르는 확률변수 $Z$ 와 자유도가 $\nu$ 인 카이제곱분포를 따르는 확률변수 $V$ 로 구성되는 확률변수의 분포

    ![10](/_post_refer_img/BayesianModeling/1.Statistics/05-10.png){: width="100%"}

    $$
    T=\frac{Z}{\sqrt{\displaystyle\frac{V}{\nu}}} \quad \text{for}\;Z \sim N(0,1),\; V \sim \chi^2(\nu)
    $$

    - **카이제곱분포($\chi^2(\nu)$)** : 자유도가 $\nu$ 로 주어졌을 때 표준정규분포를 따르는 독립적인 확률변수 $Z_{i}\left(=\displaystyle\frac{X_{i}-\overline{X}}{\sigma}\right)$ 들의 자승의 합의 분포로서, 모분산을 추정하는 데 사용됨

        $$\begin{aligned}
        V
        &=\sum_{i=1}^{k}{Z_{i}^2} \quad \text{for}\; Z_{\forall} \sim N(0,1)\\
        &=\sum_{i=1}^{k}{\left(\frac{X_{i}-\overline{X}}{\sigma}\right)^2}\\
        &=\frac{1}{\sigma^2} \times \sum_{i=1}^{k}{\left(X_{i}-\overline{X}\right)^2}\\
        &=\frac{1}{\sigma^2} \times \nu \cdot \frac{1}{\nu} \sum_{i=1}^{k}{\left(X_{i}-\overline{X}\right)^2}\\
        &=\nu \times \frac{S^2}{\sigma^2} \sim \chi^2(\nu)
        \end{aligned}$$

- **스튜던트 t 분포를 활용한 표본 $X \sim N(\mu, \sigma^2)$ 의 검정통계량 $T$ 도출**

    $$\begin{aligned}
    T
    &= Z \times \frac{1}{\sqrt{\displaystyle\frac{V}{\nu}}}\\
    &= \frac{\overline{X}-\mu}{\displaystyle\frac{\sigma}{\sqrt{n}}} \times \frac{1}{\sqrt{\displaystyle\frac{\sigma^2}{S^2}}}\\
    &= \frac{\overline{X}-\mu}{\displaystyle\frac{S}{\sqrt{n}}} \sim t(\nu)
    \end{aligned}$$
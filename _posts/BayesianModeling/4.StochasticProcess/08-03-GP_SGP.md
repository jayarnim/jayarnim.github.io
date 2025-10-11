---
order: 3
title: GP (2) Sparse Gaussian Process
date: 2025-08-03
categories: [BAYES, 4.stochastic process]
tags: [Bayesian, Deep Learning, Stochastic Process, Time Series, Nonparametric Estimation, Gaussian Process, Multi-Variate Gaussian Dist., Variational Inference]
math: true
image:
    path: /_post_refer_img/BayesianModeling/4.StochasticProcess/Thumbnail.jpg
---

## SGP
-----

- **SGP(`S`parse `G`aussian `P`rocess)** : $M < N$ 개의 유도점(Inducing Points)을 도입하여 공분산 행렬을 근사하는 기법으로서, 계산량을 $\mathcal{O}(N^{3}) \to \mathcal{O}(M^{2}N)$ 으로 줄임으로써 효율성을 도모함

    ![01](/_post_refer_img/BayesianModeling/4.StochasticProcess/06-01.png){: width="100%"}

- **Methods**
    - **Nyström Approximation `BASIC`**
        - Inducing Points Sampling
        - Matrix Factorization

    - FITC(`F`ully `I`ndependent `T`raining `C`onditional)
        - Inducing Points Sampling
        - All data Points are Independent of the Inducing Points
        - Matrix Factorization

    - SKI(`S`tructured `K`ernel `I`nterpolation)
        - Grid based Inducing Points
        - Matrix Factorization

    - **SVGP(`S`parse `V`ariational `G`aussian `P`rocess)**
        - Inducing Points Optimization
        - Variational Inference

    - **DGP(`D`ecoupled `G`aussian `P`rocess)**
        - Separate the Inducing Points into Mean Function and Covariance Function
        - Mean Function and Covariance Function Optimization
        - Variational Inference

## Nyström Approximation
-----

- **Matrix Factorization**

    $$\begin{aligned}
    \mathbf{K}_{N} \approx \mathbf{Q}_{N} = \mathbf{K}_{NM} \cdot \mathbf{K}^{-1}_{MM} \cdot \mathbf{K}_{MN}
    \end{aligned}$$

    - $$\mathbf{K}_{MM}$$ : 유도점끼리의 공분산 행렬
    - $$\mathbf{K}_{NM}$$ : 전체 데이터와 유도점 간 공분산 행렬
    - $$\mathbf{K}_{MN}$$ : $$\mathbf{K}_{NM}$$ 의 전치 행렬

- **Posterior Dist.**

    $$\begin{aligned}
    \mathcal{F}^{*} \mid X, Y, X^{*} \sim \mathcal{N}(\mu^{*}, (\sigma^{*})^{2})
    \end{aligned}$$

    - Posterior Mean:

        $$\begin{aligned}
        \mu^{*}=\mu(X^{*}) + \mathbf{q}_{N}^{*}(\mathbf{Q}_{N}+\sigma^{2}_{N}\mathbf{I})^{-1}(Y-\mu(X))
        \end{aligned}$$

    - Posterior Var.:

        $$\begin{aligned}
        (\sigma^{*})^{2}
        =\mathcal{K}(X^{*},X^{*})-\mathbf{q}_{N}^{*}(\mathbf{Q}_{N}+\sigma^{2}_{N}\mathbf{I})^{-1}\left(\mathbf{q}_{N}^{*}\right)^{T}
        \end{aligned}$$

## Variational Inference based Opt.
-----

- **SVGP(`S`parse `V`ariational `G`aussian `P`rocess)**

    - Variational Inference:

        $$\begin{aligned}
        \log{p(Y \mid X)} \ge \mathbb{E}_{f \sim q}[\log{p(Y \mid f, X)}] - D_{KL}(q(f) \parallel p(f))
        \end{aligned}$$

    - $f$ 는 무한 차원의 확률 과정이므로 이를 직접 다루지 않고 유도점 $Z$ 와 이때의 함수 값 $u=f(Z)$ 를 이용하여 근사함:

        $$\begin{aligned}
        \mathbb{E}_{f \sim q}[p(f \mid y, X)]
        &= \int{q(f) \cdot p(f \mid y, X)\text{d}f}\\
        &\downarrow\\
        \mathbb{E}_{u \sim q}[p(f \mid u, Z, X)]
        &= \int{q(u) \cdot p(f \mid u, Z, X)\text{d}u}
        \end{aligned}$$

- **DGP(`D`ecoupled `G`aussian `P`rocess)**
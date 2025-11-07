---
order: 5
title: Monte Carlo Dropout
date: 2024-08-01
categories: [BAYES, 2.posterior approx.]
tags: [Bayesian, Objective Function, Variational Inference]
math: true
description: >-
    Gal, Y., & Ghahramani, Z.</br>
    (2016, June).</br>
    <a href="https://doi.org/10.48550/arXiv.1506.02142">Dropout as a bayesian approximation: Representing model uncertainty in deep learning.</a></br>
    In international conference on machine learning (pp. 1050-1059).</br>
    PMLR.
image:
    path: /_post_refer_img/BayesianModeling/2.Posterior/Thumbnail.jpg
---

## Monte Carlo Dropout
-----

![01](/_post_refer_img/BayesianModeling/2.Posterior/05-01.png){: width="100%"}

- **`MC Dropout`(`M`onte `C`arlo Dropout)** : 드롭아웃의 확률적 성질을 변분 추론 관점에서 해석하여 사후 확률 분포를 근사하는 모수 방법론으로서, 평가 과정에서도 드롭아웃을 유지하고 여러 번 샘플링한 결과값에 평균을 내어 최종 결론을 도출함

## RFF-GP
-----

- Original Gaussian Process:

    $$\begin{aligned}
    f(x) \sim \mathcal{N}(\mu(x), \mathcal{K}(x,x))
    \end{aligned}$$

- `R`andom `F`ourier `F`eatures:

    $$\begin{aligned}
    \mathcal{K}(x,x^{\prime})
    &\approx \phi(x)^{T}\phi(x^{\prime})
    \end{aligned}$$

- $\phi(x)$:

    $$\begin{gathered}
    \phi(x)
    = \sqrt{\frac{2}{N}}\begin{bmatrix}
    \phi_{1}(x)\\
    \phi_{2}(x)\\
    \vdots\\
    \phi_{N}(x)
    \end{bmatrix},\quad
    \phi_{i}(x)
    = \cos{(w_{i}^{T}x + b_{i})}
    \end{gathered}$$

- $f(x)$ be approximated linear combination:

    $$\begin{aligned}
    f(x)
    &= \sum_{i=1}^{n}{\alpha_{i} \cdot \mathcal{K}(x,x_{i})}\\
    &\approx \sum_{i=1}^{n}{\alpha_{i} \cdot \phi(x)^{T}\phi(x_{i})}\\
    &= \phi(x)^{T} \cdot \underbrace{\sum_{i=1}^{n}{\alpha_{i} \cdot \phi(x_{i})}}_{=:\Theta}
    \end{aligned}$$

    - $\phi(x)$ is chosen randomly, but fixed once drawn
    - to give probability to $f(x)$, $\theta$ must be set as a probabilistic variable

- prior of $f(x)$:

    $$\begin{aligned}
    \Theta \sim \mathcal{N}(\mathbf{0}, \mathbf{I})
    \end{aligned}$$

- posterior of $f(x)$:

    $$\begin{aligned}
    f(x) \mid \Theta \sim \mathcal{N}(\mathbf{0}, \phi(x)^{T}\phi(x^{\prime}))
    \end{aligned}$$

## Perceptron
-----

- output vector of $k$-th layer:

    $$\begin{aligned}
    \phi^{(k)}(x)
    = \begin{bmatrix}
    \phi_{1}^{(k)}(x)\\
    \phi_{2}^{(k)}(x)\\
    \vdots\\
    \phi_{N_{k}}^{(k)}(x)\\
    \end{bmatrix}, \quad
    \phi_{i}(x)
    = \sigma(w_{i}^{T}x + b_{i})
    \end{aligned}$$

    - $k=1,2,\cdots,K$: 레이어 인덱스
    - $i=1,2,\cdots,N_{k}$: $k$ 번째 레이어의 노드 인덱스
    - $j=1,2,\cdots,N_{k+1}$: $k+1$ 번째 레이어의 노드 인덱스

- the weight vector of the $j$-th node @ $k+1$-th layer:

    $$\begin{aligned}
    \Theta_{j}^{(k+1)}
    = \begin{bmatrix}
    \theta_{j,1}^{(k+1)}\\
    \theta_{j,2}^{(k+1)}\\
    \vdots\\
    \theta_{j,N_{k}}^{(k+1)}\\
    \end{bmatrix}
    \end{aligned}$$

- net-input of the $j$-th node @ $k+1$-th layer:

    $$\begin{aligned}
    f_{j}^{(k+1)}(x)
    = \phi^{(k)}(x)^{T}\Theta_{j}^{(k+1)}
    \end{aligned}$$

## Dropout
-----

- dropout mask:

    $$\begin{aligned}
    z_{i}^{(k)} \sim \mathrm{Bernoulli}(p)
    \end{aligned}$$

- net-input with dropout applied:

    $$\begin{aligned}
    f_{j}^{(k+1)}(x)
    = \left[\mathbf{z}^{(k)} \odot \phi^{(k)}(x)\right]^{T}\Theta_{j}^{(k+1)}
    \end{aligned}$$

- it is equivalent to:

    $$\begin{aligned}
    f_{j}^{(k+1)}(x)
    = \phi^{(k)}(x)^{T}\left[\mathbf{z}^{(k)} \odot \Theta_{j}^{(k+1)}\right]
    \end{aligned}$$

- approx. dist.:

    $$\begin{aligned}
    q(w)
    &= \prod_{k=1}^{K}\prod_{j=1}^{N_{k+1}}\prod_{i=1}^{N_{k}}{p(z_{i}^{(k)})} \quad \text{for} \quad w=z\cdot\theta
    \end{aligned}$$

## How to Interpret
-----

- `R`andom `F`ourier `F`eatures `G`aussian `P`rocess:

    $$\begin{gathered}
    f(x)
    = \phi (x)^{T}\Theta\\
    \phi(x)
    = \sqrt{\frac{2}{K}}\begin{bmatrix}
    \phi_{1}(x)\\
    \phi_{2}(x)\\
    \vdots\\
    \phi_{K}(x)
    \end{bmatrix},\quad
    \Theta
    = \begin{bmatrix}
    \theta_{1}\\
    \theta_{2}\\
    \vdots\\
    \theta_{K}
    \end{bmatrix}
    \end{gathered}$$

    - $f(x) = \phi (x)^{T}\Theta$: 입력값 $x$ 에 대한 출력값

        $$\begin{aligned}
        f(x) \mid \Theta 
        &\sim \mathcal{N}(0, \left<\phi(x),\phi(x^{\prime})\right>)
        \end{aligned}$$

    - $\phi(x)$: 무작위 푸리에 기저 함수 출력값 벡터

        $$\begin{aligned}
        \phi(x)
        &= \sqrt{\frac{2}{K}}
        \begin{bmatrix}
        \phi_{1}(x)\\
        \phi_{2}(x)\\
        \vdots\\
        \phi_{K}(x)
        \end{bmatrix}
        \end{aligned}$$

        - $\phi_{k}(x)=\cos{(w_{k}^{T}x + b_{k})}$: 무작위 푸리에 기저 함수 출력값
    
    - $\Theta \sim \mathcal{N}(\mathbf{0}, \mathbf{I})$: $f(x)$ 의 사전 확률 분포

        $$
        \Theta
        = \begin{bmatrix}
        \theta_{1}\\
        \theta_{2}\\
        \vdots\\
        \theta_{K}
        \end{bmatrix}
        $$

## How to Interpret
-----

- **Original ELBO**

    $$\begin{aligned}
    \text{ELBO}
    = \mathbb{E}_{W \sim Q}\left[\log{P(\mathcal{D} \mid W)}\right] - D_{KL}\big[Q(W) \parallel P(W)\big]
    \end{aligned}$$

    - $P(W)$ : Prior Dist.
    - $Q(W)$ : Approx. Dist.
    - $$\mathbb{E}_{W \sim Q}\left[\log{P(\mathcal{D} \mid W)}\right]$$ : Likelihood

- **Prior Dist.** : Normality Assumption

    $$\begin{aligned}
    \mathcal{W} \sim \mathcal{N}\left(0, \sigma^{2}_{p}\mathbf{I}\right)
    \end{aligned}$$

- **Approx. Dist.**

    - Dropout is a process of applying Bernoulli sampling to weights, <br> so each weight has stochastic properties:

        $$\begin{aligned}
        \mathcal{W} \mid \mathbf{M} &\sim Q
        \end{aligned}$$

        - $\mathcal{W} = \mathbf{W} \odot \mathbf{M}$
        - $M_{i,j} \sim \text{Bernoulli}(p)$

    - According to the CLS, <br> the mean and variance of multiple samplings converge to a normal dist.

        $$\begin{aligned}
        q(\mathcal{\omega}) \approx \mathcal{N}\left(0, \sigma^{2}_{q}\mathbf{I}\right)
        \end{aligned}$$

- **KL Divergence from Approx. to Prior**

    $$\begin{aligned}
    D_{KL}(q \parallel p)
    &= \frac{1}{2}\sum_{i}\left(\frac{\sigma_{q}^{2}}{\sigma_{p}^{2}} + \frac{\sigma_{p}^{2}}{\sigma_{q}^{2}} - 1\right)
    \end{aligned}$$

    - If $\sigma_{p}^{2} \approx \sigma_{q}^{2}$:

        $$\begin{aligned}
        D_{KL}(q \parallel p)
        &= \frac{1}{2\sigma^{2}}\Vert \mathcal{W} \Vert^{2}
        \end{aligned}$$

- **Likelihood** <br> Approximated by averaging the results of multiple samplings

    $$\begin{aligned}
    \mathbb{E}_{\omega \sim q}[\log{p(\mathcal{D} \mid \omega)}]
    \approx \frac{1}{T}\sum_{t=1}^{T}{\log{p(\mathcal{D} \mid \omega_{t})}}
    \end{aligned}$$

- **Therefore:**

    $$\begin{aligned}
    \text{ELBO}
    &= \frac{1}{T}\sum_{t=1}^{T}{\log{p(\mathcal{D} \mid \omega_{t})}} - \frac{1}{2\sigma^{2}}\Vert \mathcal{W} \Vert^{2}
    \end{aligned}$$
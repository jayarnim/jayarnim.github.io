---
order: 5
title: Monte Carlo Dropout
date: 2024-07-24
categories: [BAYES, 2.posterior approx.]
tags: [Bayesian, Objective Function, Variational Inference]
math: true
image:
    path: /_post_refer_img/BayesianModeling/Thumbnail.jpeg
---

## Monte Carlo Dropout
-----

![01](/_post_refer_img/BayesianModeling/02-05-01.png){: width="100%"}

- **MC Dropout(`M`onte `C`arlo Dropout)** : 드롭아웃의 확률적 성질을 변분추론 관점에서 해석하여 사후 확률 분포를 근사하는 모수 방법론으로서, 평가 과정에서도 드롭아웃을 유지하고 여러 번 샘플링한 결과값에 평균을 내어 최종 결론을 도출함

    - [Dropout as a Bayesian Approximation: Representing Model Uncertainty in Deep Learning(2016)](https://doi.org/10.48550/arXiv.1506.02142)

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
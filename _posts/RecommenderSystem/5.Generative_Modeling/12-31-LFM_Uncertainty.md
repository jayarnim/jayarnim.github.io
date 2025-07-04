---
order: 1
title: Latent Factor Models with Uncertainty
date: 2024-03-27
categories: [AI Application, Recommender System]
tags: [Paper Review, AI Application, Recommender System, Collaborative Filtering, Latent Factor Model, Bayesian]
math: true
description: >-
    <ul type="square">
    <li><strong>Title</strong>: <a href="https://doi.org/10.1145/1390156.1390267"><code>Bayesian Probabilistic Matrix Factorization using Markov Chain Monte Carlo</code></a></li>
    <li><strong>Published</strong>: <em>2008</em></li>
    <li><strong>Data Set</strong>: <code><a href="https://www.kaggle.com/datasets/netflix-inc/netflix-prize-data">Netflix Prize</a></code></li>
    </ul>
image:
    path: /_post_refer_img/RecommenderSystem/Thumbnail.jpg
---

## Previous Research
-----

### MF

- **행렬분해(`M`atrix `F`actorization; MF)** : 잠재요인 모형의 원형으로서, 사용자-아이템 상호작용 행렬 $\mathbf{R} \in \mathbb{R}^{M \times N}$ 을 행렬분해하여 $K$ 차원 잠재요인(Latent Factor) 공간에 사용자-잠재요인 $\mathbf{U} \in \mathbb{R}^{M \times K}$ 와 아이템-잠재요인 $\mathbf{V} \in \mathbb{R}^{N \times K}$ 을 공동으로 사상하는 방법

- **Model**

    $$\begin{aligned}
    \mathbf{R} &\approx \mathbf{U}\mathbf{V}^{T}
    \end{aligned}$$

    - $\mathbf{R}$ : User-Item Interaction Matrix

- **Hyper-Params**
    - $K$ : Dimension of Latent Factor

- **Objective Function Optimization**

    $$\begin{aligned}
    \hat{\mathbf{U}}, \hat{\mathbf{V}}
    &= \text{arg} \min_{\mathbf{U},\mathbf{V}}{\mathcal{J}\left(\mathbf{U}\mathbf{V}^{T}, \mathbf{R}\right)}
    \end{aligned}$$

    - $\hat{\mathbf{U}}, \hat{\mathbf{V}}$ : OLS(`O`rdinary `L`east `S`quares) or MLE(`M`aximum `L`ikelihood `E`stimation) Estimatior
        - $\mathbf{U}$ : User-Latent Factor Matrix
        - $\mathbf{V}$ : Item-Latent Factor Matrix

### PMF

- **확률적 행렬분해(`P`robabilistic `M`atrix `F`actorization; PMF)** : 정보 불확실성을 반영하기 위해 $\mathbf{U},\mathbf{V}$ 를 상수에서 확률변수화하고, 확률적 경사하강법(`S`tochastic `G`radient `D`escent; SGD)을 활용하여 최대 사후 확률(`M`aximum `a` `P`osteriori; MAP) 추정치를 탐색하는 방법

- **Model**

    $$
    \mathbf{R} \mid \mathbf{U},\mathbf{V} \sim \mathcal{N}\left(\mathbf{U}\mathbf{V}^{T}, \sigma^{2}\right)
    $$

    - $$\mathbf{R} \mid \mathbf{U},\mathbf{V}$$ : Liklihood Distribution of User-Item Interaction Matrix

- **Hyper-Params**
    - $K$ : Dimension of Latent Factor

    - Prior Distribution Parameters of $$\mathbf{U} \sim \mathcal{N}\left(\overrightarrow{\mu}_{U}, \lambda_{U}^{-1}\cdot\mathbf{I}\right)$$
        - $\overrightarrow{\mu}_{U}$ : Mean of User-Latent Factor
        - $\lambda_{U}^{-1}$ : Variance of User-Latent Factor

    - Prior Distribution Parameters of $$\mathbf{V} \sim \mathcal{N}\left(\overrightarrow{\mu}_{V}, \lambda_{V}^{-1}\cdot\mathbf{I}\right)$$
        - $\overrightarrow{\mu}_{V}$ : Mean of Item-Latent Factor
        - $\lambda_{V}^{-1}$ : Variance of Item-Latent Factor

    - $\sigma^{2}$ : Noise of User-Item Interaction

- **Objective Function Optimization**

    $$\begin{aligned}
    \hat{\mathbf{U}}, \hat{\mathbf{V}}
    &= \text{arg} \max_{\mathbf{U},\mathbf{V}}{\log{P\left(\mathbf{U},\mathbf{V}\mid\mathbf{R}\right)}}
    \end{aligned}$$

    - $\hat{\mathbf{U}}, \hat{\mathbf{V}}$ : MAP(`M`aximum `a` `P`osteriori) Estimator
        - $\mathbf{U}$ : User-Latent Factor Matrix
        - $\mathbf{V}$ : Item-Latent Factor Matrix

    - $\log{P\left(\mathbf{U},\mathbf{V}\mid\mathbf{R}\right)}$ : Log Joint Posterior Probability of Params

        $$
        \log{P\left(\mathbf{U},\mathbf{V}\mid\mathbf{R}\right)} \propto \log{P\left(\mathbf{R}\mid\mathbf{U},\mathbf{V}\right)} + \log{P\left(\mathbf{U}\right)} + \log{P\left(\mathbf{V}\right)}
        $$

## BPMF
-----

- **베이지안 확률적 행렬분해(`B`ayesian `P`robabilistic `M`atrix `F`actorization; BPMF)** : PMF 에서 제한적으로 적용되었던 베이지안 방법론의 적용 범위를 확장한 방법

- **PMF 의 한계점**
    - 학습파라미터의 사후 확률 분포를 추론한 후 베이즈 액션을 취하지 아니하고, 확률적 경사하강법을 통해 최대 사후 확률 추정치만을 추론함
    - 학습파라미터를 최대 사후 확률 추정치로 확정함으로써 학습파라미터의 불확실성을 반영하지 아니함

- **BPMF 의 해법**
    - MCMC(`M`arkov `C`hain `M`onte `C`arlo)를 활용하여 학습파라미터의 사후 확률 분포를 추론함
    - 학습파라미터를 특정 값으로 확정하지 아니하고 사후 확률 분포로부터 샘플링된 다양한 추정치들을 활용함으로써 학습파라미터의 불확실성을 반영함
    - $\mathbf{U}, \mathbf{V}$ 의 사전 확률 분포를 연구자에 의해 고정된 파라미터로 설정하지 아니하고 확률적 모델링을 통해 추정함

### How to Modeling

- **Model**

    $$
    \mathbf{R} \mid \overrightarrow{\mu}_{U}, \Lambda_{U}, \overrightarrow{\mu}_{V}, \Lambda_{V} \sim \mathcal{N}\left(\mathbf{U}\mathbf{V}^{T}, \sigma^{2}\right)
    $$

    - $$\mathbf{R} \mid \mathbf{U},\mathbf{V}$$ : Liklihood Distribution of User-Item Interaction Matrix

- **Hyper-Params**
    - $K$ : Dimension of Latent Factor

    - Prior Distribution Parameters of $$\overrightarrow{\mu} ; \Lambda \sim \mathcal{N}\left(\mu_{0}, (\beta_{0} \cdot \Lambda)^{-1}\right)$$
        - $\mu_{0}=0$ : Mean of User(Item)-Latent Factor Mean
        - $\beta_{0}=0$ : Scale Factor of $\Lambda$

    - Prior Distribution Parameters of $$\Lambda \sim \mathcal{W}\left(\mathbf{W}_{0}, \nu_{0}\right)$$
        - $$\mathbf{W}_{0}=\mathbf{I}_{K \times K}$$ : Scale Matrix
        - $\nu_{0}=K+1$ : Dgree of Freedom

    - $\sigma^{2}$ : Noise of User-Item Interaction

- **Objective Function**

    $$\begin{aligned}
    &\log{P\left(\overrightarrow{\mu}_{U}, \Lambda_{U}, \overrightarrow{\mu}_{V}, \Lambda_{V} \mid \mathbf{R}\right)}\\
    &\propto \log{P\left(\mathbf{R} \mid \mathbf{U},\mathbf{V}\right)}\\
    &+ \log{P\left(\mathbf{U} \mid \overrightarrow{\mu}_{U},\Lambda_{U}\right)} + \log{P\left(\overrightarrow{\mu}_{U} ; \Lambda_{U}\right)} + \log{P\left(\Lambda_{U}\right)}\\
    &+ \log{P\left(\mathbf{V} \mid \overrightarrow{\mu}_{V},\Lambda_{V}\right)} + \log{P\left(\overrightarrow{\mu}_{V} ; \Lambda_{V}\right)} + \log{P\left(\Lambda_{V}\right)}
    \end{aligned}$$

    - $$\overrightarrow{\mu}_{U}, \Lambda_{U}, \overrightarrow{\mu}_{V}, \Lambda_{V} \mid \mathbf{R}$$ : Joint Posterior Probability Distribution of Params
    - $$\mathbf{R} \mid \mathbf{U},\mathbf{V}$$ : Liklihood Distribution of User-Item Interaction Matrix
    - $$\mathbf{U} \mid \overrightarrow{\mu}_{U},\Lambda_{U}$$ : Conditional Prior Distribution of User-Latent Factor Matrix
    - $$\mathbf{V} \mid \overrightarrow{\mu}_{V},\Lambda_{V}$$ : Conditional Prior Distribution of Item-Latent Factor Matrix
    - $$\overrightarrow{\mu}, \Lambda$$ : Marginal Prior Distribution of $$\mathbf{U}, \mathbf{V} \sim \mathcal{N}\left(\overrightarrow{\mu}, \Lambda\right)$$ Params
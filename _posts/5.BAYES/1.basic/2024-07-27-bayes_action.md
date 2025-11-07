---
order: 6
title: Bayes Action
date: 2024-07-27
categories: [5.BAYES, 1.bayes basic]
tags: [bayesian, optimization, objective function]
math: true
description: >-
    Based on the lecture “Bayesian Modeling (2024-1)” by Prof. Yeo Jin Chung, Dept. of AI, Big Data & Management, College of Business Administration, Kookmin Univ.
image:
    path: /_post_refer_img/5.BAYES/1.basic/Thumbnail.jpeg
---

## Bayes Action
-----

> 사후확률 $\theta \mid X$ 을 추정하기 위해, 확률분포 $P(\theta \mid X) \propto \mathcal{L}(\theta) \cdot \pi(\theta)$ 로부터 $n$ 번의 샘플링을 통해 $n$ 개의 샘플 $\theta^{(1)},\theta^{(2)},\cdots,\theta^{(n)}$ 을 도출했다고 하자. 그렇다면 이들 중 무엇을 모수 $\theta \mid X$ 의 추정치 $\hat{\theta}$ 로 사용하는 것이 적절할까?

- **Bayes' Risk** : 사후확률분포 $P(\theta \mid X)$ 를 사용하여 계산된, 모수 $\theta$ 에 대하여 추정치 $\hat{\theta}$ 를 선택할 때의 기대 손실(Expected Loss)

    $$\begin{aligned}
    \mathcal{R}(\hat{\theta})
    &= \mathbb{E}_{\theta \mid X}\left[\text{Loss}(\theta, \hat{\theta})\right]\\
    &= \int{\text{Loss}(\theta, \hat{\theta}) \cdot P(\theta \mid X)}\text{d}\theta
    \end{aligned}$$

    - 모수 $\theta \mid X$ 를 알 수 없으므로, $n$ 번의 샘플링을 통해 도출한 $n$ 개의 샘플 $\theta^{(1)},\theta^{(2)},\cdots,\theta^{(n)} \sim P(\theta \mid X)$ 를 사용하여 근사함

        $$\begin{aligned}
        \mathcal{R}(\hat{\theta})
        &= \mathbb{E}_{\theta \mid X}\left[\text{Loss}(\theta, \hat{\theta})\right]\\
        &\approx \frac{1}{N}\sum_{i=1}^{N}{\text{Loss}(\theta^{(i)}, \hat{\theta})}
        \end{aligned}$$

- **Bayes Estimator** : 모수 $\theta$ 에 대하여, Bayes' Risk 를 최소화시키는 추정치 $\hat{\theta}$

    $$\begin{aligned}
    \hat{\theta}
    &= \text{arg} \min_{\hat{\theta}}{\mathcal{R}(\hat{\theta})}
    \end{aligned}$$

    - **Posterior Mean** : Bayes' Least Square (BLS) Estimator

        $$\begin{aligned}
        \hat{\theta}
        &= \text{arg} \min_{\hat{\theta}}{\mathbb{E}_{\theta \mid X}\left[(\theta-\hat{\theta})^2\right]}\\
        &= \mathbb{E}_{\theta \mid X}(\theta)
        \end{aligned}$$

    - **Posterior Median**

        $$\begin{aligned}
        \hat{\theta}
        &= \text{arg} \min_{\hat{\theta}}{\mathbb{E}_{\theta \mid X}\left[ \vert \theta-\hat{\theta} \vert \right]}\\
        &= \tilde{\theta}
        \end{aligned}$$

    - **Posterior mode** : Maximum a posteriori (MAP) Estimator

        $$\begin{aligned}
        \hat{\theta}
        &= \text{arg} \min_{\hat{\theta}}{\mathbb{E}_{\theta \mid X}\left[1_{\hat{\theta} \ne \theta}\right]}\\
        &= \text{arg} \max_{\theta}{P(\theta \mid X)}
        \end{aligned}$$

## Loss Function
-----

### Continuous Prob. Variable

- **Squared Error Loss**

    $$\begin{aligned}
    \text{Loss}(\theta, \hat{\theta})
    &= (\theta - \hat{\theta})^2
    \end{aligned}$$

- **Asymmetric Squared Error Loss**

    $$
    \text{Loss}(\theta, \hat{\theta})
    = \begin{cases}\begin{aligned}
    &(\theta - \hat{\theta})^2 \quad &\text{if}\;\hat{\theta} < \theta&\\
    &c \cdot (\theta - \hat{\theta})^2 \quad &\text{if}\;\hat{\theta} \ge \theta&,\;0<c<1
    \end{aligned}\end{cases}
    $$

- **Absolute Error Loss**

    $$\begin{aligned}
    \text{Loss}(\theta, \hat{\theta})
    =  \vert \theta - \hat{\theta} \vert 
    \end{aligned}$$

### Discrete Prob. Variable

- **Zero-One Loss**

    $$\begin{aligned}
    \text{Loss}(\theta, \hat{\theta})
    &= 1_{\hat{\theta} \ne \theta}\\
    &= \begin{cases}\begin{aligned}
    &0 \quad &\text{if}\;\hat{\theta} = \theta\\
    &1 \quad &\text{if}\;\hat{\theta} \ne \theta
    \end{aligned}\end{cases}
    \end{aligned}$$

- **Binary Cross Entropy Loss**

    $$\begin{aligned}
    \text{Loss}(\theta, \hat{\theta})
    = -\left[\hat{\theta} \cdot \log{\theta}+(1-\hat{\theta})\cdot\log{(1-\theta)}\right] \quad \text{for}\;&\hat{\theta}\in\{0,1\},\\&\theta\in[0,1]
    \end{aligned}$$

    - 관측치 $\hat{\theta}$ 가 $\theta$ 를 확률로 가지는 베르누이 분포로부터 생성된다고 하자

        $$\begin{aligned}
        \hat{\theta} \sim \text{Bernoulli}(\theta)
        \end{aligned}$$

    - $\hat{\theta}$ 에 대한 확률질량함수는 다음과 같음

        $$
        P(\hat{\theta};\theta)=\theta^{\hat{\theta}} \cdot (1-\theta)^{1-\hat{\theta}}
        $$

    - 이를 $\theta$ 에 대한 로그 우도 함수로 해석할 수 있음

        $$\begin{aligned}
        \log{\mathcal{L}(\theta)}
        &= \log{P(\hat{\theta} \mid \theta)}\\
        &= \hat{\theta} \cdot \log{\theta} + (1-\hat{\theta}) \cdot \log{(1-\theta)}
        \end{aligned}$$

    - $\theta$ 를 모수, $\hat{\theta}$ 를 추정치에 대응하여 손실함수를 구성하면 다음과 같음

        $$\begin{aligned}
        \text{Loss}(\theta,\hat{\theta})
        &= -\log{\mathcal{L}(\theta)}\\
        &= -\log{P(\hat{\theta} \mid \theta)}\\
        &= - \left[\hat{\theta} \cdot \log{\theta} + (1-\hat{\theta}) \cdot \log{(1-\theta)}\right]
        \end{aligned}$$

- **Categorical Cross Entropy Loss**

    $$\begin{aligned}
    \text{Loss}(\theta, \hat{\theta})
    = -\sum_{i=1}^{K}{\hat{\theta}_{i}\cdot\log{\theta_{i}}} \quad \text{for}\;&\hat{\theta}_{i}\in\{0,1\},\\&\theta_{i}\in[0,1]
    \end{aligned}$$

    - 관측치 $\hat{\theta}$ 가 $\theta$ 를 확률로 가지는 카테고리 분포로부터 생성된다고 하자

        $$\begin{aligned}
        \hat{\theta} \sim \text{Categorical}(\theta)
        \end{aligned}$$

    - $\hat{\theta}$ 에 대한 확률질량함수는 다음과 같음

        $$
        P(\hat{\theta};\theta)=\prod_{i=1}^{K}{\theta_{i}^{\hat{\theta}_{i}}}
        $$

    - 이를 $\theta$ 에 대한 로그 우도 함수로 해석할 수 있음

        $$\begin{aligned}
        \log{\mathcal{L}(\theta)}
        &= \log{P(\hat{\theta} \mid \theta)}\\
        &= \sum_{i=1}^{K}{\hat{\theta}_{i} \cdot \log{\theta_{i}}}
        \end{aligned}$$

    - $\theta$ 를 모수, $\hat{\theta}$ 를 추정치에 대응하여 손실함수를 구성하면 다음과 같음

        $$\begin{aligned}
        \text{Loss}(\theta,\hat{\theta})
        &= -\log{\mathcal{L}(\theta)}\\
        &= -\log{P(\hat{\theta} \mid \theta)}\\
        &= - \sum_{i=1}^{K}{\hat{\theta}_{i} \cdot \log{\theta_{i}}}
        \end{aligned}$$
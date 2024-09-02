---
order: 4
title: Posterior Estimation (2) Information Theory
date: 2024-07-18
categories: [Statistical Techs, Bayesian Modeling]
tags: [Statistics, Bayesian, Information Theory, Variational Inference]
math: true
description: >-
    Based on the lecture “Bayesian Modeling (2024-1)” by Prof. Yeo Jin Chung, Dept. of AI, Big Data & Management, College of Business Administration, Kookmin Univ.
image:
    path: /_post_refer_img/BayesianModeling/Thumbnail.jpeg
---

## Information Theory
-----

- **정보이론(Information Theory)** : 신호에 존재하는 정보의 양을 측정하는 이론으로서, 특정 확률분포의 특성을 알아내거나, 두 확률분포 간 유사성을 정량화하는 데 사용함

### Information Gain

- **자기정보(Self-Information)** : 확률변수 $X \sim P$ 에 대하여, 사건 $X=x$ 가 발생했을 때의 정보량

    $$\begin{aligned}
    I(X=x)
    &= \log{\frac{1}{P(X=x)}}\\
    &=-\log{P(X=x)}
    \end{aligned}$$

    - 자주 발생하지 않는 사건(Unlikely Event)일수록 높은 정보량을 가짐(Informative)
    - 독립사건은 추가적인 정보량을 가짐(Addictive Information)
        - 동전을 두 번 던져서 앞면이 두 번 나오는 사건은 동전을 한 번 던져서 앞면이 나오는 사건보다 정보량이 두 배임

- **엔트로피(Entropy)** : 자기정보의 기대값으로서, 주어진 확률분포에서 발생 가능한 사건들의 평균적인 정보량

    $$\begin{aligned}
    H(P)
    &= \mathbb{E}_{X \sim P}\left[I(X)\right]\\
    &= \mathbb{E}_{X \sim P}\left[-\log{P(X)}\right]\\
    &= -\mathbb{E}_{X \sim P}\left[\log{P(X)}\right]\\
    &= -\sum_{x}{\log{P(x)} \cdot P(x)}
    \end{aligned}$$

    - 사건의 분포가 결정적일수록(Deterministic) 엔트로피가 감소함
    - 사건의 분포가 균등할수록(Uniform) 엔트로피가 증가함

### Information Discrepancy

- **교차 엔트로피(Cross Entropy)** : 확률변수 $X$ 의 분포 $P$ 와 그 근사 분포 $Q$ 에 대하여, $Q$ 가 $P$ 에 대하여 제공하는 **정보의 불확실성을** 측정하는 지표

    $$\begin{aligned}
    H(P,Q)
    &= \mathbb{E}_{X \sim P}\left[-\log{Q(X)}\right]\\
    &= - \sum_{x}{\log{Q(x)} \cdot P(x)}
    \end{aligned}$$

- **쿨백 라이블러 발산(Kullback-Leibler Divergence)** : 확률변수 $X$ 의 분포 $P$ 와 그 근사 분포 $Q$ 에 대하여, $Q$ 를 $P$ 의 **근사 분포로 사용할 때의 비효율성을** 측정하는 지표

    $$\begin{aligned}
    D_{KL}(P \parallel Q)
    &= \mathbb{E}_{X \sim P}\left[-\log{P(X)}\right] - \mathbb{E}_{X \sim P}\left[-\log{Q(X)}\right]\\
    &= \mathbb{E}_{X \sim P}\left[-\log{\frac{Q(X)}{P(X)}}\right]\\
    &= \mathbb{E}_{X \sim P}\left[\log{\frac{P(X)}{Q(X)}}\right]\\
    &= \sum_{x}{\log{\frac{P(x)}{Q(x)}} \cdot P(x)}
    \end{aligned}$$

- **교차 엔트로피와 쿨백 라이블러 발산의 관계**

    $$\begin{aligned}
    D_{KL}(P \parallel Q)
    &= \sum_{x}{\log{\frac{P(x)}{Q(x)}} \cdot P(x)}\\
    &= -\sum_{x}{\log{\frac{Q(x)}{P(x)}} \cdot P(x)}\\
    &= -\sum_{x}{\left[\log{Q(x)}-\log{P(x)}\right] \cdot P(x)}\\
    &= \left[-\sum_{x}{\log{Q(x)} \cdot P(x)}\right] -\left[-\sum_{x}{\log{P(x)} \cdot P(x)}\right]\\
    &= H(P,Q) - H(P)
    \end{aligned}$$

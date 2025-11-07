---
order: 1
title: Stochastic Process
date: 2025-08-01
categories: [BAYES, 4.stochastic process]
tags: [Bayesian, Stochastic Process, Time Series]
math: true
image:
    path: /_post_refer_img/BayesianModeling/4.StochasticProcess/Thumbnail.jpg
---

## Stochastic Process
-----

- **확률 과정(Stochastic Process)**

    > 어떤 시점 혹은 위치 지표 $t$ 에 대하여 확률 변수들의 집합 $$\{X_{t} \mid t \in T\}$$ 이 주어졌을 때 이를 확률 과정이라고 한다. 즉, 확률 과정은 인덱스를 따라 변화하는 확률변수들의 집합으로서, 각 인덱스 $$t \in T$$ 에 대응되는 확률변수 $$X_{t}$$ 가 주어져, 인덱스 집합 $$T$$ 위에서 확률변수의 집합이 구성되는 구조이다.

## Type
-----

- Hidden Markov Model

- Gaussian Process
    - Likelihood: Multi-Variate Gaussian Dist.
    - Prior: Mean Function & Covariance Function

- Gamma-Cox Process
    - Likelihood: Poisson Process
    - Prior: Gamma Process

- Indian Buffet Process
    - Likelihood: Bernoulli Process
    - Prior: Beta Process

- Chinese Restaurant Process
    - Likelihood: Cluster
    - Prior: Dirichlet Process
---
order: 3
title: Prior Prob. Dist.
date: 2024-07-03
categories: [Statistical Techs, Bayesian Modeling]
tags: [Statistics, Bayesian]
math: true
description: >-
  Based on the lecture “Bayesian Modeling (2024-1)” by Prof. Yeo Jin Chung, Dept. of AI, Big Data & Management, College of Business Administration, Kookmin Univ.
image:
  path: /_post_refer_img/BayesianModeling/Thumbnail.jpeg
---

## 사전확률분포의 결정
-----

- 사전확률분포의 결정은 모델링의 일부임

    >모형이 적합한 이후에는 사후확률분포를 살펴보아야 하고, 이치에 맞는지 확인해야 한다. 만일 사후확률분포가 이치에 맞지 않는다면 모형에 포함되지 않은 사전 정보가 추가로 필요하다는 것을 의미한다. 그리고 이전에 사용한 사전확률분포의 가정에 위배된다는 것을 의미한다. 그래서 이전으로 돌아가 사전확률분포가 외부 정보와 조화되도록 변경하는 것이 적절하다. (Andrew Gelman)

- 사전확률분포의 결정은 해결하려는 문제에 따라 달라지며, 어느 것이 항상 최선의 대안이라고 볼 수 없음
    - 과학 연구의 경우, 결과에 대한 편향을 제거하기 위하여 객관적인 사전확률분포(Objective Prior Dist.)를 선택하는 것이 적절함

- 관측치 갯수($N$)가 많아질수록 사전확률분포의 영향력이 약화됨

    ![01](/_post_refer_img/BayesianModeling/03-01.png){: width="100%"}

## 사전확률분포의 종류
-----

![02](/_post_refer_img/BayesianModeling/03-02.png){: width="100%"}

- **객관적인 확률분포(Objective/Non-Informative Dist.)**
    - **Principle of Indifference** : 가능한 모수 공간에서 특별히 어떤 값을 선호하지 않는 원칙에 따라, 관측치가 사후분포에 미치는 영향력을 최대화하는 방법

    - 주로 Flat Prior Dist.를 사용함

        $$\begin{aligned}
        X \vert \theta &\sim \text{Binomial}(n,\theta)\\
        \theta &\sim \text{Uniform}(0,1)
        \end{aligned}$$

    - 큰 범위의 균등 분포(Uniform Dist.)는 객관적인 사전확률분포(Objective Prior Dist.)로서 좋은 선택지이지만, 실제로 발생할 가능성이 낮은 파라미터를 할당할 수 있다는 점에서 한계점이 있음
        - `대안.1` $\sigma$ 가 매우 큰 정규 분포 $N(0, \sigma^2)$
        - `대안.2` 양의 영역에서 꼬리가 두터운 지수 분포 $\text{Exp}(\lambda)$

- **주관적인 확률분포(Subjective/Informative Dist.)**
    - **Principle of Subjectivity** : 주관적 판단을 반영하여 특정한 영역을 선호하는 원칙에 따라, 사전 지식이나 경험, 믿음 등의 영향력을 개입시킴으로써 특정 영역에 편향된 추론 결과를 도출하는 방법

## Empirical Bayes Method
-----

- **정의** : 사전확률분포에 설정되는 하이퍼파라미터를 빈도주의적으로 접근하여 추정하는 방법
- **장점** : 사전 정보가 많지 않지만 관측치가 풍부한 경우 유용한 방법임
- **단점** : 관측치를 관측하기 이전에 사전분포가 정의되어야 한다는 베이지안 추론 원칙에 위배되는 방법임

### `example` General Model

$$\begin{aligned}
X_{i} \vert \theta &\sim N(\theta, 5^2)\\
\theta &\sim N(\mu, \sigma^2)
\end{aligned}$$

- **객관적 사전확률분포 설정을 통한 접근**

    $$
    \theta \sim N(0, 100^2)
    $$

- **주관적 사전확률분포 설정을 통한 접근**

    $$
    \theta \sim N(\mu_{0}, \sigma_{0}^{2})
    $$

    - $\mu=\mu_{0}$ : 연구자가 보유하고 있는 사전 정보를 활용하여 설정
    - $\sigma=\sigma_{0}$ : 연구자가 보유하고 있는 불확실성을 수량화하여 설정

- **Empirical Bayes**

    $$
    \theta \sim N\left(\frac{1}{N}\sum_{i=1}^{N}{X_i}, \frac{1}{N-1}\sum_{i=1}^{N}{(X_i-\mu)^2}\right)
    $$

## Conjugate Priors
-----

- **정의** : 관측치 $X$ 와 그 확률분포 $$\mathcal{L}_{\alpha}$$ 에 대하여, 다음의 조건을 만족하는 사전확률분포 $$\pi_{\beta}$$ 가 존재하는 경우, $$\pi_{\beta}$$ 를 $$\mathcal{L}_{\alpha}$$ 의 켤레사전분포(Conjugate Prior Prob. Dist.)라고 함

    $$\begin{aligned}
    \pi_{\beta^{\prime}}(\theta \vert X) \propto \mathcal{L}_{\alpha}(\theta) \cdot \pi_{\beta}(\theta)
    \end{aligned}$$

    - $\mathcal{L}_{\alpha}(\theta)$ : 모수 $\theta$ 의 우도 함수
    - $\pi_{\beta}(\theta)$ : 모수 $\theta$ 의 사전 확률
    - $\pi_{\beta^{\prime}}(\theta \vert X)$ : 모수 $\theta$ 의 사후 확률
    - $\alpha,\beta,\beta^{\prime}$ : 모수들의 집합

- **예시**

    | Likelihood | Prior | Posterior |
    |---|---|---|
    | $\text{Bernoulli}(\theta)$ | $\text{Beta}(\alpha, \beta)$ | $\text{Beta}\Big(\alpha + n \cdot \bar{x}, \beta + n\cdot(1-\bar{x})\Big)$ |
    | $\text{Poisson}(\lambda)$ | $\text{Gamma}(\alpha, \beta)$ | $\text{Gamma}(\alpha+ n \cdot \bar{x}, \beta+n)$ |
    | $\text{Multinomial}(\theta)$ | $\text{Dirichlet}(\alpha)$ | $\text{Dirichlet}(\alpha+n \cdot \bar{x})$ |
    | $N(\mu, \sigma^2) \\ (\text{known} \; \sigma^2$) | $N(\mu_0, \sigma_0^2)$ | $N\Bigg( \displaystyle\frac{\displaystyle\frac{\mu_0}{\sigma_0^2} + \frac{n \cdot \bar{x}}{\sigma^2}}{\displaystyle\frac{1}{\sigma_0^2} + \displaystyle\frac{n}{\sigma^2}}, \displaystyle\frac{1}{\displaystyle\frac{1}{\sigma_0^2} + \frac{n}{\sigma^2}} \Bigg)$ |
    |$N(\mu, \sigma^2) \\ (\text{known} \; \mu)$ | $\text{Inv-Gamma}(\alpha, \beta)$ | $\text{Inv-Gamma}\Bigg(\alpha + \displaystyle\frac{n}{2}, \beta + \displaystyle\frac{n \cdot (\bar{x} -\mu)^2}{2}\Bigg)$ |
    | $N(\mu, \Sigma) \\ (\text{known} \; \mu)$ | $\text{Inv-Wishart}(\nu_{0}, S_{0})$ | $\text{Inv-Wishart}(\nu_{0}+n, S_{0} + n \cdot \bar{S})$ |

## Jeffreys Priors

### Transformation Variant

- 모수 $\theta$ 가 균등 분포 $\text{Uniform}(0,1)$ 를 따르는 객관적인 사전확률이라고 하자

    $$
    \theta \sim \text{Uniform}(0,1)
    $$

- 모수 $\theta$ 를 $\log{\frac{\theta}{1-\theta}}$ 로 변수 변환한 $\psi$ 는 로지스틱 분포 $\text{Logistic}(0,1)$ 을 따르게 됨

    $$\begin{aligned}
    \psi
    &= g(\theta)\\
    &= \log{\frac{\theta}{1-\theta}}\\ \\

    \theta
    &= g^{-1}(\psi)\\
    &= \frac{\text{exp}(\psi)}{1+\text{exp}(\psi)}\\ \\

    f_{\psi}(\psi)
    &= f_{\theta}(g^{-1}(\psi)) \times \Big \vert \frac{\text{d}}{\text{d} \psi}g^{-1}(\psi)\Big \vert \\
    &= 1 \times \Big \vert \frac{\text{d}}{\text{d} \psi}g^{-1}(\psi)\Big \vert  \quad (\because \theta \sim \text{Uniform}(0,1))\\
    &= \frac{\text{exp}(\psi)}{(1+\text{exp}(\psi))^{2}} \\ \\

    \therefore \psi &\sim \text{Logistic}(0,1)
    \end{aligned}$$

- 즉, 모수 $\theta$ 의 변수 변환에 의하여 사전분포의 객관성이 상실되었음

    - 변환 전 : $\theta \sim \text{Uniform}(0,1)$

        ![03](/_post_refer_img/BayesianModeling/03-03.png){: width="100%"}

    - 변환 후 : $\psi \sim \text{Logistic}(0,1)$

        ![04](/_post_refer_img/BayesianModeling/03-04.png){: width="100%"}

### Jeffreys Priors

- **정의** : 모수 공간에 대해 불변성을 보장함으로써 변수 변환 후에도 객관성을 보존하는 사전분포

    $$
    \pi_{J}(\theta) \propto \sqrt{\mathbf{I}(\theta)}
    $$

    - $\sqrt{\mathbf{I}(\theta)}$ : Fisher Information

        $$\begin{aligned}
        \mathbf{I}(\theta)
        &= - \mathbb{E}\bigg[\frac{\text{d}^{2}}{\text{d}\theta^{2}}\log{\mathcal{L}(\theta)}\bigg]
        \end{aligned}$$
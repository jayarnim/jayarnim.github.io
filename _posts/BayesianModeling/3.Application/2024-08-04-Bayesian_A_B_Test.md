---
order: 1
title: Bayesian A/B Test
date: 2024-08-04
categories: [BAYES, 3.bayes applications]
tags: [Bayesian, Design of Experiments, A/B Test]
math: true
description: >-
    Based on the lecture “Bayesian Modeling (2024-1)” by Prof. Yeo Jin Chung, Dept. of AI, Big Data & Management, College of Business Administration, Kookmin Univ.
image:
    path: /_post_refer_img/BayesianModeling/3.Application/Thumbnail.jpg
---

![01](/_post_refer_img/BayesianModeling/3.Application/01-01.png){: width="100%"}

> #### Question
> 프론트엔드 웹 개발자는 전환율(Conversion Rate)을 개선하기 위해 웹사이트 디자인을 기존 $A$ 안에서 $B$ 안으로 개편하고자 한다. 변경 전, 개발자는 개편이 성공적이었는지 확인하기 위해 A/B Test 를 실시하였다. 구체적으로 방문객 일부에게는 $A$ 를, 나머지는 $B$ 를 제공한 후, 전환 수를 아래와 같이 기록하였다. $A,B$ 전환율 간에 유의한 차이가 있다고 볼 수 있는가? (단, $$\sigma^2_{A}=\sigma^2_{B}$$ 임이 알려져 있다고 가정한다.)

| 디자인 | 방문자 수 | 전환 수 |
|---|---|---|
| A | 1,300 | 120 |
| B | 1,275 | 125 |

## Frequentist A/B Test
-----

- **Point Estimator**
    - **Interest Parameter** : $\pi_A-\pi_B$
    - **Point Estimator** : $p_A-p_B$

- **Hypothesis**
    - $H_{0}:\quad p_A-p_B = D_{0}$
    - $H_{1}:\quad p_A-p_B \ne D_{0}$

- **Parametric Test Assumptions**

    $$\begin{aligned}
    n_A \cdot p_A &\ge 5\\
    n_A \cdot (1-p_A) &\ge 5\\
    n_B \cdot p_B &\ge 5\\
    n_B \cdot (1-p_B) &\ge 5
    \end{aligned}$$

- **Test Statistic**

    $$\begin{aligned}
    Z
    &= \frac{(p_A-p_B) - D_0}{\sqrt{s^2_p(1-s^2_p)\left(\displaystyle\frac{1}{n_A}+\displaystyle\frac{1}{n_B}\right)}}
    \sim N(0,1)
    \end{aligned}$$

    - $s^{2}_p$ : Pooled Estimator

        $$
        s^{2}_p = \frac{n_A \cdot p_A + n_B \cdot p_B }{n_A + n_B}
        $$

## Bayesian A/B Test
-----

- **Prior of $\pi$ Determination**

    - 전환율 $\pi$ 은 $n$ 번의 실험에 따른 성공 횟수 $X \mid \pi$ 에 대한 성공 확률임

        $$
        X \mid \pi \sim \text{Bin}(n,\pi)
        $$

    - `Binomial Dist.` 의 성공 확률 $\pi$ 에 대한 `Conjugate Prior Dist.` 로서 `Beta Dist.` 가 적합함

        $$
        \pi \sim \text{Beta}(\alpha_0,\beta_0)
        $$

- **Posterior of $\pi \mid X$ Estimation**

    $$
    \pi \mid X \sim \text{Beta}(\alpha_0 + X, \beta_0 + n - X)
    $$

- **Beyes Action**

    $$
    \hat{p} = \text{arg}\min{\mathcal{R}(p)}
    $$

    - $\mathcal{R}(p)$ : Bayes Risk

        $$\begin{aligned}
        \mathcal{R}(p)
        &= \mathbb{E}_{\pi \mid X}\left[\text{Loss}(\pi, p)\right]\\
        &\approx \frac{1}{k}\sum_{i=1}^{k}{\text{Loss}(p^{(i)}, p)}
        \end{aligned}$$

- **Compare $\hat{p}_A$ and $\hat{p}_B$**
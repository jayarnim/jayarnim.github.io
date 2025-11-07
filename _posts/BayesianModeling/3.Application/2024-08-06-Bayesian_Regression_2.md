---
order: 6
title: Bayesian Regression (2) Subjective Prior
date: 2024-08-06
categories: [BAYES, 3.bayes applications]
tags: [Bayesian, Regression]
math: true
description: >-
    Based on the lecture “Bayesian Modeling (2024-1)” by Prof. Yeo Jin Chung, Dept. of AI, Big Data & Management, College of Business Administration, Kookmin Univ.
image:
    path: /_post_refer_img/BayesianModeling/3.Application/Thumbnail.jpg
---

<div style="text-align: center;">
    <img src="/_post_refer_img/BayesianModeling/3.Application/06-01.png" alt="01" width="100%">
    <p><em>Bayesian Regression Model</em></p>
</div>

## Liklihood Function
-----

- 다중선형회귀모형의 우도 함수:

    $$\begin{aligned}
    \mathcal{L}(\mathbf{b}, \sigma^2)
    &= (2\pi\sigma^{2})^{-n/2} \cdot \exp{\left[-\frac{1}{2\sigma^{2}}\cdot(\mathbf{y}-\mathbf{X}\mathbf{b})^{T}(\mathbf{y}-\mathbf{X}\mathbf{b})\right]} \quad (\because \mathbf{y} \sim \mathcal{N}(\mathbf{X}\mathbf{b}, \sigma^{2}\mathbf{I}))\\
    &\propto (\sigma^2)^{-n/2} \cdot \exp{\left[-\frac{1}{2\sigma^{2}}\cdot(\mathbf{y}-\mathbf{X}\mathbf{b})^{T}(\mathbf{y}-\mathbf{X}\mathbf{b})\right]}
    \end{aligned}$$

## Setting Conjugate Prior
-----

$$
p(\mathbf{b}, \sigma^{2}) = p(\mathbf{b} \mid \sigma^{2}) \cdot p(\sigma^{2})
$$

- Conjugate Prior of $\sigma^{2}$ is Scaled Inverse Chi-Squared Distribution

    $$\begin{gathered}
    p(\sigma^{2})
    \propto (\sigma^{2})^{-\nu_{0}/2-1} \cdot \exp{\left[-\frac{1}{2\sigma^{2}}\cdot \nu_{0} s_{0}^{2}\right]}\\
    \therefore \sigma^{2} \sim \text{Scaled Inv-}\chi^2(\nu_{0}, s_{0}^{2})
    \end{gathered}$$

    - $\nu_{0}$ : 사전 자유도
    - $s_{0}^{2}$ : 사전 잔차 분산

- Conjugate Prior of $\beta$ given $\sigma^{2}$ is Normal Distribution

    $$\begin{gathered}
    p(\mathbf{b} \mid \sigma^{2})
    \propto (\sigma^{2})^{-(n-\nu_{0})/2} \cdot \exp{\left[-\frac{1}{2\sigma^{2}}\cdot(\mathbf{b}-\mu_{0})^{T}\Lambda_{0}(\mathbf{b}-\mu_{0})\right]}\\
    \therefore \mathbf{b} \mid \sigma^{2} \sim \mathcal{N}(\mu_{0}, \sigma^{2}\Lambda_{0}^{-1})
    \end{gathered}$$

    - $\mu_{0}$ : $\mathbf{b}$ 의 사전 평균
    - $\sigma^{2}\Lambda_{0}^{-1}$ : $\mathbf{b}$ 의 사전 공분산 행렬

## Posterior Estimation
-----

$$\begin{aligned}
p(\mathbf{b}, \sigma^{2} \mid \mathcal{D})
&\propto \mathcal{L}(\mathbf{b}, \sigma^{2}) \cdot p(\mathbf{b}, \sigma^{2})\\
&\propto (\sigma^{2})^{-n/2} \cdot \exp{\left[-\frac{1}{2\sigma^{2}}\cdot(\mathbf{y}-\mathbf{X}\mathbf{b})^{T}(\mathbf{y}-\mathbf{X}\mathbf{b})\right]} \times (\sigma^{2})^{-\nu_{n}/2-1} \cdot \exp{\left[-\frac{1}{2\sigma^{2}}\cdot \nu_{n} s_{n}^{2}\right]} \times (\sigma^{2})^{-(n-\nu_{n})/2} \cdot \exp{\left[-\frac{1}{2\sigma^{2}}\cdot(\mathbf{b}-\mu_{n})^{T}\Lambda_{n}(\mathbf{b}-\mu_{n})\right]}\\
&= (\sigma^2)^{-(n+\nu_{n})/2-1} \cdot \exp{\left[-\frac{1}{2\sigma^{2}}\left(\nu_{n} s_{n}^{2} + (\mathbf{y}-\mathbf{X}\mathbf{b})^{T}(\mathbf{y}-\mathbf{X}\mathbf{b})\right)\right]} \times (\sigma^{2})^{-(n-\nu_{n})/2} \cdot \exp{\left[-\frac{1}{2\sigma^{2}}\cdot(\mathbf{b}-\mu_{n})^{T}\Lambda_{n}(\mathbf{b}-\mu_{n})\right]}
\end{aligned}$$

- Posterior of $\sigma^2$ is Inverse-Gamma Distribution

    $$\begin{gathered}
    p(\sigma^{2} \mid \mathcal{D})
    \propto (\sigma^2)^{-(n+\nu_{n})/2-1} \cdot \exp{\left[-\frac{1}{2\sigma^{2}}\left(\nu_n s_{n}^{2} + (\mathbf{y}-\mathbf{X}\mathbf{b})^{T}(\mathbf{y}-\mathbf{X}\mathbf{b})\right)\right]}\\
    \therefore \sigma^{2} \mid \mathcal{D}
    \sim \text{Inv-Gamma}\left(\frac{n + \nu_{n}}{2}, \frac{1}{2} \left[\nu_{n} s_{n}^{2} + (\mathbf{y} - \mathbf{X}\mathbf{b})^{T}(\mathbf{y} - \mathbf{X}\mathbf{b})\right]\right)
    \end{gathered}$$

    - $\nu_{n}$ : 사후 자유도
    - $s_{n}^{2}$ : 사후 잔차 분산

- Posterior of $\beta$ given $\sigma^2$ is Normal Distribution

    $$\begin{gathered}
    p(\mathbf{b}\mid\sigma^{2},\mathcal{D})
    \propto (\sigma^{2})^{-(n-\nu_{n})/2} \cdot \exp{\left[-\frac{1}{2\sigma^{2}}\cdot(\mathbf{b}-\mu_{n})^{T}\Lambda_{n}(\mathbf{b}-\mu_{n})\right]}\\
    \therefore \mathbf{b}\mid\sigma^{2},\mathcal{D}
    \sim \mathcal{N}(\mu_{n}, \sigma^{2}\Lambda_{n}^{-1})
    \end{gathered}$$

    - $\mu_{n}$ : $\mathbf{b}$ 의 사후 평균
    - $\sigma^{2}\Lambda_{n}^{-1}$ : $\mathbf{b}$ 의 사후 공분산 행렬
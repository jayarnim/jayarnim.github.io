---
order: 5
title: Bayesian Regression (1) Objective Prior
date: 2024-08-08
categories: [BAYES, 3.bayes applications]
tags: [Bayesian, Regression]
math: true
description: >-
    Based on the lecture “Bayesian Modeling (2024-1)” by Prof. Yeo Jin Chung, Dept. of AI, Big Data & Management, College of Business Administration, Kookmin Univ.
image:
    path: /_post_refer_img/BayesianModeling/3.Application/Thumbnail.jpg
---

<div style="text-align: center;">
    <img src="/_post_refer_img/BayesianModeling/3.Application/05-01.png" alt="01" width="100%">
    <p><em>Bayesian Regression Model</em></p>
</div>

## Liklihood Function Transformation
-----

- 다중선형회귀모형의 우도 함수:

    $$\begin{aligned}
    \mathcal{L}(\mathbf{b}, \sigma^2)
    &= (2\pi\sigma^2)^{-n/2} \cdot \exp{\left[-\frac{1}{2\sigma^2}\cdot(\mathbf{y}-\mathbf{X}\mathbf{b})^{T}(\mathbf{y}-\mathbf{X}\mathbf{b})\right]} \quad (\because \mathbf{y} \sim \mathcal{N}(\mathbf{X}\mathbf{b}, \sigma^2\mathbf{I}))\\
    &\propto (\sigma^2)^{-n/2} \cdot \exp{\left[-\frac{1}{2\sigma^2}\cdot(\mathbf{y}-\mathbf{X}\mathbf{b})^{T}(\mathbf{y}-\mathbf{X}\mathbf{b})\right]}
    \end{aligned}$$

- $(\mathbf{y}-\mathbf{X}\mathbf{b})^{T}(\mathbf{y}-\mathbf{X}\mathbf{b})$ 변형:

    $$\begin{aligned}
    (\mathbf{y}-\mathbf{X}\mathbf{b})^{T}(\mathbf{y}-\mathbf{X}\mathbf{b})
    &= \left[(\mathbf{y}-\mathbf{X}\hat{\mathbf{b}}) + (\mathbf{X}\hat{\mathbf{b}}-\mathbf{X}\mathbf{b})\right]^{T}\left[(\mathbf{y}-\mathbf{X}\hat{\mathbf{b}}) + (\mathbf{X}\hat{\mathbf{b}}-\mathbf{X}\mathbf{b})\right]\\
    &= (\mathbf{y}-\mathbf{X}\hat{\mathbf{b}})^{T}(\mathbf{y}-\mathbf{X}\hat{\mathbf{b}}) + (\mathbf{X}\hat{\mathbf{b}}-\mathbf{X}\mathbf{b})^{T}(\mathbf{X}\hat{\mathbf{b}}-\mathbf{X}\mathbf{b}) + 2 \cdot (\mathbf{y}-\mathbf{X}\hat{\mathbf{b}})^{T}(\mathbf{X}\hat{\mathbf{b}}-\mathbf{X}\mathbf{b})\\
    \\
    (\mathbf{X}\hat{\mathbf{b}}-\mathbf{X}\mathbf{b})^{T}(\mathbf{X}\hat{\mathbf{b}}-\mathbf{X}\mathbf{b})
    &= (\mathbf{b} - \hat{\mathbf{b}})^{T}(\mathbf{X}^{T}\mathbf{X})(\mathbf{b} - \hat{\mathbf{b}})\\
    2 \cdot (\mathbf{y}-\mathbf{X}\hat{\mathbf{b}})^{T}(\mathbf{X}\hat{\mathbf{b}}-\mathbf{X}\mathbf{b})
    &=0\\
    \\
    \therefore (\mathbf{y}-\mathbf{X}\mathbf{b})^{T}(\mathbf{y}-\mathbf{X}\mathbf{b})
    &= (\mathbf{y}-\mathbf{X}\hat{\mathbf{b}})^{T}(\mathbf{y}-\mathbf{X}\hat{\mathbf{b}}) + (\mathbf{b} - \hat{\mathbf{b}})^{T}(\mathbf{X}^{T}\mathbf{X})(\mathbf{b} - \hat{\mathbf{b}})\\
    \end{aligned}$$

- 우도 함수에 대입:

    $$\begin{aligned}
    \mathcal{L}(\mathbf{b}, \sigma^2)
    &\propto (\sigma^2)^{-n/2} \cdot \exp{\left[-\frac{1}{2\sigma^2}(\mathbf{y}-\mathbf{X}\hat{\mathbf{b}})^{T}(\mathbf{y}-\mathbf{X}\hat{\mathbf{b}})\right]} \cdot \exp{\left[-\frac{1}{2\sigma^2}(\mathbf{b} - \hat{\mathbf{b}})^{T}(\mathbf{X}^{T}\mathbf{X})(\mathbf{b} - \hat{\mathbf{b}})\right]}\\
    \end{aligned}$$

- 잔차 분산 및 자유도 정의:

    $$\begin{aligned}
    s^{2}
    &= \frac{1}{\nu} \cdot RSS\\
    &= \frac{1}{\nu} \cdot (\mathbf{y}-\mathbf{X}\hat{\mathbf{b}})^{T}(\mathbf{y}-\mathbf{X}\hat{\mathbf{b}})\\
    \nu
    &= n-k
    \end{aligned}$$

- 우도 함수에 대입:

    $$\begin{aligned}
    \therefore \mathcal{L}(\mathbf{b}, \sigma^{2})
    &\propto (\sigma^{2})^{-\nu/2} \cdot \exp{\left[-\frac{1}{2\sigma^{2}}\cdot \nu s^{2}\right]} \times (\sigma^{2})^{-(n-\nu)/2} \cdot \exp{\left[-\frac{1}{2\sigma^{2}}\cdot (\mathbf{b} - \hat{\mathbf{b}})^{T}(\mathbf{X}^{T}\mathbf{X})(\mathbf{b} - \hat{\mathbf{b}})\right]}
    \end{aligned}$$

## Prior Determination
-----

$$\begin{aligned}
p(\mathbf{b}, \sigma^{2})
&= p(\mathbf{b} \mid \sigma^{2}) \cdot p(\sigma^{2})\\
&= p(\mathbf{b}) \cdot p(\sigma^{2}) \quad (\because \text{i.i.d})\\
&= 1 \times \frac{1}{\sigma^{2}}
\end{aligned}$$

- Jacobian Change of $\sigma^2$ for Relaxing Range Constraints

    $$\begin{aligned}
    \psi
    &= \log{\sigma^{2}}\\
    \therefore p(\sigma^{2})
    &= p(\psi) \cdot \frac{1}{\sigma^{2}}
    \end{aligned}$$

- Non-informative Prior Determination of $\beta, \psi$

    $$
    \mathbf{b}, \psi \sim \text{Uniform}(0,1)
    $$

- Jeffreys Prior of $\sigma^{2}$

    $$\begin{aligned}
    p(\sigma^{2})
    = p(\psi) \cdot \frac{1}{\sigma^{2}}
    = \frac{1}{\sigma^{2}}
    \end{aligned}$$

## Posterior Estimation
-----

$$\begin{aligned}
p(\mathbf{b}, \sigma^{2} \mid \mathcal{D})
&\propto \mathcal{L}(\mathbf{b}, \sigma^{2}) \cdot p(\mathbf{b}, \sigma^{2})\\
\
&\propto (\sigma^{2})^{-\nu/2} \cdot \exp{\left[-\frac{1}{2\sigma^{2}}\cdot \nu s^{2}\right]} \times (\sigma^{2})^{-(n-\nu)/2} \cdot \exp{\left[-\frac{1}{2\sigma^{2}} \cdot (\mathbf{b} - \hat{\mathbf{b}})^{T}(\mathbf{X}^{T}\mathbf{X})(\mathbf{b} - \hat{\mathbf{b}})\right]} \times \frac{1}{\sigma^{2}}\\
&= (\sigma^{2})^{-\nu/2-1} \cdot \exp{\left[-\frac{1}{2\sigma^{2}}\cdot \nu s^{2}\right]} \times (\sigma^{2})^{-(n-\nu)/2} \cdot \exp{\left[-\frac{1}{2\sigma^{2}} \cdot (\mathbf{b} - \hat{\mathbf{b}})^{T}(\mathbf{X}^{T}\mathbf{X})(\mathbf{b} - \hat{\mathbf{b}})\right]}
\end{aligned}$$

- Marginal Posterior of $\sigma^2$ is Inverse Chi-Squared Distribution

    $$\begin{gathered}
    f(\sigma^2 \mid \nu,s^2)
    =(\sigma^2)^{-\nu/2-1} \cdot \exp{\left[-\frac{1}{2\sigma^2}\cdot \nu s^2\right]}\\
    \therefore \sigma^2 \mid \mathcal{D}
    \sim \text{Inv-}\chi^2(\nu,s^2)
    \end{gathered}$$

- Conditional Posterior of $\beta$ given $\sigma^2$ is Normal Distribution

    $$\begin{gathered}
    f(\mathbf{b} \mid \hat{\mathbf{b}}, \mathbf{V}_{\beta})
    = (\sigma^2)^{-(n-\nu)/2} \cdot \exp{\left[-\frac{1}{2\sigma^2}\cdot (\mathbf{b} - \hat{\mathbf{b}})^{T}(\mathbf{X}^{T}\mathbf{X})(\mathbf{b} - \hat{\mathbf{b}})\right]}\\
    \therefore \mathbf{b} \mid \sigma^{2}, \mathcal{D}
    \sim \mathcal{N}(\hat{\mathbf{b}}, \sigma^2\mathbf{V}_{\beta})
    \end{gathered}$$

    - $\hat{\mathbf{b}}=(\mathbf{X}^{T}\mathbf{X})^{-1}\mathbf{X}^{T}\mathbf{y}$ : $\mathbf{b}$ 의 최우추정량
    - $\sigma^2\mathbf{V}_{\beta}=\sigma^2(\mathbf{X}^{T}\mathbf{X})^{-1}$ : $\mathbf{b}$ 의 공분산 행렬
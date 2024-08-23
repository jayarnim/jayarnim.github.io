---
order: 7
title: Bayesian Regression
date: 2024-07-21
categories: [Statistical Techs, Bayesian Modeling]
tags: [Statistics, Bayesian, Regression]
math: true
description: >-
    Based on the lecture “Bayesian Modeling (2024-1)” by Prof. Yeo Jin Chung, Dept. of AI, Big Data & Management, College of Business Administration, Kookmin Univ.
image:
    path: /_post_refer_img/BayesianModeling/Thumbnail.jpeg
---

<div style="text-align: center;">
    <img src="/_post_refer_img/BayesianModeling/07-01.png" alt="01" width="100%">
    <p><em>Bayesian Regression Model</em></p>
</div>

## Frequentist Estimation
-----

- **다중선형회귀모형(Multiple Linear Regression Model)**

    $$\begin{aligned}
    \overrightarrow{y}
    &= \mathbf{X}\overrightarrow{\beta} + \overrightarrow{\varepsilon}
    \quad \text{for} \quad \overrightarrow{\varepsilon} \sim N(0, \sigma^2\mathbf{I})\\
    \therefore \overrightarrow{y}
    &= \mathbf{X}\overrightarrow{\hat{\beta}}
    \end{aligned}$$

### MLE

- **최우추정법(Maximum Liklihood Estimation; MLE)** : 우도를 최대화하는 회귀계수를 탐색하는 방법

    $$\begin{aligned}
    \overrightarrow{\hat{\beta}}_{MLE}
    &= \text{arg}\max{\mathcal{L}(\overrightarrow{\beta}, \sigma^2)}
    \end{aligned}$$

- **우도(Liklihood)** : 파라미터 $\theta$ 가 주어졌을 때, 관측치 $y$ 가 발생할 확률

    $$\begin{aligned}
    \overrightarrow{y}
    &\sim N(\mathbf{X}\overrightarrow{\beta}, \sigma^2\mathbf{I}) \quad (\because \overrightarrow{\varepsilon} \sim N(0, \sigma^2\mathbf{I}))\\
    \\
    \therefore \mathcal{L}(\overrightarrow{\beta}, \sigma^2)
    &= P(\overrightarrow{y} \,\mid\, \overrightarrow{\beta}, \sigma^2)\\
    &= \frac{1}{(2\pi\sigma^2)^{n/2}} \cdot \exp{\left[-\frac{1}{2\sigma^2}\cdot(\overrightarrow{y}-\mathbf{X}\overrightarrow{\hat{\beta}})^{T}(\overrightarrow{y}-\mathbf{X}\overrightarrow{\hat{\beta}})\right]}
    \end{aligned}$$

### OLS

- **최소자승법(Least Square Estimation; OLS)** : 잔차 자승의 합을 최소화하는 회귀계수를 탐색하는 방법

    $$\begin{aligned}
    \overrightarrow{\hat{\beta}}_{OLS}
    &= \text{arg}\min_{\beta}{RSS}\\
    &= (\mathbf{X}^{T}\mathbf{X})^{-1}\mathbf{X}^{T}\overrightarrow{y}
    \end{aligned}$$

- **Residual Sum of Square(RSS)** : 잔차 자승의 합

    $$\begin{aligned}
    RSS
    &= \sum_{i}{(y_{i}-\hat{y}_{i})^2}\\
    &= \mid \overrightarrow{y} - \overrightarrow{\hat{y}} \mid^{2}\\
    &= (\overrightarrow{y}-\mathbf{X}\overrightarrow{\hat{\beta}})^{T}(\overrightarrow{y}-\mathbf{X}\overrightarrow{\hat{\beta}})
    \end{aligned}$$

### $$\hat{\beta}_{MLE}=\hat{\beta}_{OLS}$$

- **우도 $\mathcal{L}(\overrightarrow{\beta}, \sigma^2)$ 는 잔차 $RSS$ 에 반비례함**

    $$\begin{aligned}
    \mathcal{L}(\overrightarrow{\beta}, \sigma^2)
    &\propto \log{\mathcal{L}(\overrightarrow{\beta}, \sigma^2)}\\
    &= -\frac{n}{2}\cdot\log{2\pi\sigma^2}-\frac{1}{2\sigma^2}\cdot(\overrightarrow{y}-\mathbf{X}\overrightarrow{\beta})^{T}(\overrightarrow{y}-\mathbf{X}\overrightarrow{\beta})\\
    &\propto -\frac{1}{2\sigma^2}\cdot(\overrightarrow{y}-\mathbf{X}\overrightarrow{\beta})^{T}(\overrightarrow{y}-\mathbf{X}\overrightarrow{\beta})\\
    &\propto -(\overrightarrow{y}-\mathbf{X}\overrightarrow{\beta})^{T}(\overrightarrow{y}-\mathbf{X}\overrightarrow{\beta})\\
    &= -RSS
    \end{aligned}$$

- **따라서 최우추정량(우도를 최대화하는 모수) $\hat{\beta}_{MLE}$ 과 최소자승추정량(잔차를 최소화하는 모수) $\hat{\beta}_{OLS}$ 는 동일함**

    $$\begin{aligned}
    \therefore \text{arg}\max_{\beta}{\mathcal{L}(\overrightarrow{\beta}, \sigma^2)}
    &= \text{arg}\max_{\beta}{\log{\mathcal{L}(\overrightarrow{\beta}, \sigma^2)}}\\
    &= \text{arg}\max_{\beta}{-(\overrightarrow{y}-\mathbf{X}\overrightarrow{\beta})^{T}(\overrightarrow{y}-\mathbf{X}\overrightarrow{\beta})}\\
    &= \text{arg}\min_{\beta}{(\overrightarrow{y}-\mathbf{X}\overrightarrow{\beta})^{T}(\overrightarrow{y}-\mathbf{X}\overrightarrow{\beta})}\\
    &= \text{arg}\min_{\beta}{RSS}
    \end{aligned}$$

## Non-informative Prior Determination
-----

### Liklihood Function Transformation

- **다중선형회귀모형의 우도 함수**

    $$\begin{aligned}
    \mathcal{L}(\beta, \sigma^2)
    &= (2\pi\sigma^2)^{-n/2} \cdot \exp{\left[-\frac{1}{2\sigma^2}\cdot(\overrightarrow{y}-\mathbf{X}\overrightarrow{\beta})^{T}(\overrightarrow{y}-\mathbf{X}\overrightarrow{\beta})\right]} \quad (\because \overrightarrow{y} \sim N(\mathbf{X}\overrightarrow{\beta}, \sigma^2\mathbf{I}))\\
    &\propto (\sigma^2)^{-n/2} \cdot \exp{\left[-\frac{1}{2\sigma^2}\cdot(\overrightarrow{y}-\mathbf{X}\overrightarrow{\beta})^{T}(\overrightarrow{y}-\mathbf{X}\overrightarrow{\beta})\right]}
    \end{aligned}$$

- **$(\overrightarrow{y}-\mathbf{X}\overrightarrow{\beta})^{T}(\overrightarrow{y}-\mathbf{X}\overrightarrow{\beta})$ 변형**

    $$\begin{aligned}
    (\overrightarrow{y}-\mathbf{X}\overrightarrow{\beta})^{T}(\overrightarrow{y}-\mathbf{X}\overrightarrow{\beta})
    &= \left[(\overrightarrow{y}-\mathbf{X}\overrightarrow{\hat{\beta}}) + (\mathbf{X}\overrightarrow{\hat{\beta}}-\mathbf{X}\overrightarrow{\beta})\right]^{T}\left[(\overrightarrow{y}-\mathbf{X}\overrightarrow{\hat{\beta}}) + (\mathbf{X}\overrightarrow{\hat{\beta}}-\mathbf{X}\overrightarrow{\beta})\right]\\
    &= (\overrightarrow{y}-\mathbf{X}\overrightarrow{\hat{\beta}})^{T}(\overrightarrow{y}-\mathbf{X}\overrightarrow{\hat{\beta}})\\
    &\quad + (\mathbf{X}\overrightarrow{\hat{\beta}}-\mathbf{X}\overrightarrow{\beta})^{T}(\mathbf{X}\overrightarrow{\hat{\beta}}-\mathbf{X}\overrightarrow{\beta})\\
    &\quad + 2 \cdot (\overrightarrow{y}-\mathbf{X}\overrightarrow{\hat{\beta}})^{T}(\mathbf{X}\overrightarrow{\hat{\beta}}-\mathbf{X}\overrightarrow{\beta})\\
    \\
    (\mathbf{X}\overrightarrow{\hat{\beta}}-\mathbf{X}\overrightarrow{\beta})^{T}(\mathbf{X}\overrightarrow{\hat{\beta}}-\mathbf{X}\overrightarrow{\beta})
    &= (\overrightarrow{\beta} - \overrightarrow{\hat{\beta}})^{T}(\mathbf{X}^{T}\mathbf{X})(\overrightarrow{\beta} - \overrightarrow{\hat{\beta}})\\
    2 \cdot (\overrightarrow{y}-\mathbf{X}\overrightarrow{\hat{\beta}})^{T}(\mathbf{X}\overrightarrow{\hat{\beta}}-\mathbf{X}\overrightarrow{\beta})
    &=0\\
    \\
    \therefore (\overrightarrow{y}-\mathbf{X}\overrightarrow{\beta})^{T}(\overrightarrow{y}-\mathbf{X}\overrightarrow{\beta})
    &= (\overrightarrow{y}-\mathbf{X}\overrightarrow{\hat{\beta}})^{T}(\overrightarrow{y}-\mathbf{X}\overrightarrow{\hat{\beta}}) + (\overrightarrow{\beta} - \overrightarrow{\hat{\beta}})^{T}(\mathbf{X}^{T}\mathbf{X})(\overrightarrow{\beta} - \overrightarrow{\hat{\beta}})\\
    \end{aligned}$$

- **우도 함수에 대입**

    $$\begin{aligned}
    \mathcal{L}(\beta, \sigma^2)
    &\propto (\sigma^2)^{-n/2}\\
    &\quad \cdot \exp{\left[-\frac{1}{2\sigma^2}(\overrightarrow{y}-\mathbf{X}\overrightarrow{\hat{\beta}})^{T}(\overrightarrow{y}-\mathbf{X}\overrightarrow{\hat{\beta}})\right]}\\
    &\quad \cdot \exp{\left[-\frac{1}{2\sigma^2}(\overrightarrow{\beta} - \overrightarrow{\hat{\beta}})^{T}(\mathbf{X}^{T}\mathbf{X})(\overrightarrow{\beta} - \overrightarrow{\hat{\beta}})\right]}\\
    \end{aligned}$$

- **잔차 분산 및 자유도 정의**

    $$\begin{aligned}
    s^{2}
    &= \frac{1}{\nu} \cdot RSS\\
    &= \frac{1}{\nu} \cdot (\overrightarrow{y}-\mathbf{X}\overrightarrow{\hat{\beta}})^{T}(\overrightarrow{y}-\mathbf{X}\overrightarrow{\hat{\beta}})\\
    \nu
    &= n-k
    \end{aligned}$$

- **우도 함수에 대입**

    $$\begin{aligned}
    \therefore \mathcal{L}(\beta, \sigma^2)
    &\propto (\sigma^2)^{-\nu/2} \cdot \exp{\left[-\frac{1}{2\sigma^2}\cdot \nu s^2\right]}\\
    &\quad \times (\sigma^2)^{-(n-\nu)/2} \cdot \exp{\left[-\frac{1}{2\sigma^2}\cdot (\overrightarrow{\beta} - \overrightarrow{\hat{\beta}})^{T}(\mathbf{X}^{T}\mathbf{X})(\overrightarrow{\beta} - \overrightarrow{\hat{\beta}})\right]}
    \end{aligned}$$

### Prior Determination of $\beta, \sigma^2$

$$\begin{aligned}
P(\beta, \sigma^2)
&= P(\beta ; \sigma^2) \cdot P(\sigma^2)\\
&= P(\beta) \cdot P(\sigma^2) \quad (\because \text{i.i.d})\\
&= 1 \times \frac{1}{\sigma^2}
\end{aligned}$$

- **Jacobian Change of $\sigma^2$ for Relaxing Range Constraints**

    $$\begin{aligned}
    \psi
    &= \log{\sigma^2}\\
    \therefore P(\sigma^2)
    &= P(\psi) \cdot \frac{1}{\sigma^2}
    \end{aligned}$$

- **Non-informative Prior Determination of $\beta, \psi$**

    $$
    \beta, \psi \sim \text{Uniform}(0,1)
    $$

- **Jeffreys Prior of $\sigma^2$**

    $$\begin{aligned}
    P(\sigma^2)
    &= P(\psi) \cdot \frac{1}{\sigma^2}\\
    &= \frac{1}{\sigma^2}
    \end{aligned}$$

### Posterior Estimation of $\beta, \sigma^2$

$$\begin{aligned}
P(\beta, \sigma^2 \mid \mathcal{D})
&\propto P(\mathcal{D} \mid \beta, \sigma^2) \cdot P(\beta, \sigma^2)\\
\\
&\propto (\sigma^2)^{-\nu/2} \cdot \exp{\left[-\frac{1}{2\sigma^2}\cdot \nu s^2\right]}\\
&\quad \times (\sigma^2)^{-(n-\nu)/2} \cdot \exp{\left[-\frac{1}{2\sigma^2} \cdot (\overrightarrow{\beta} - \overrightarrow{\hat{\beta}})^{T}(\mathbf{X}^{T}\mathbf{X})(\overrightarrow{\beta} - \overrightarrow{\hat{\beta}})\right]}\\
&\quad \times \frac{1}{\sigma^2}\\
\\
&= (\sigma^2)^{-\nu/2-1} \cdot \exp{\left[-\frac{1}{2\sigma^2}\cdot \nu s^2\right]}\\
&\quad \times (\sigma^2)^{-(n-\nu)/2} \cdot \exp{\left[-\frac{1}{2\sigma^2} \cdot (\overrightarrow{\beta} - \overrightarrow{\hat{\beta}})^{T}(\mathbf{X}^{T}\mathbf{X})(\overrightarrow{\beta} - \overrightarrow{\hat{\beta}})\right]}
\end{aligned}$$

- **Marginal Posterior of $\sigma^2$ is Inverse Chi-Squared Distribution**

    $$\begin{aligned}
    f(\sigma^2 \mid \nu,s^2)
    &=(\sigma^2)^{-\nu/2-1} \cdot \exp{\left[-\frac{1}{2\sigma^2}\cdot \nu s^2\right]}\\
    \therefore \sigma^2 \mid \mathcal{D}
    &\sim \text{Inv-}\chi^2(\nu,s^2)
    \end{aligned}$$

- **Conditional Posterior of $\beta$ given $\sigma^2$ is Normal Distribution**

    $$\begin{aligned}
    f(\beta \mid \hat{\beta}, \mathbf{V}_{\beta})
    &= (\sigma^2)^{-(n-\nu)/2} \cdot \exp{\left[-\frac{1}{2\sigma^2}\cdot (\overrightarrow{\beta} - \overrightarrow{\hat{\beta}})^{T}(\mathbf{X}^{T}\mathbf{X})(\overrightarrow{\beta} - \overrightarrow{\hat{\beta}})\right]}\\
    \therefore \beta ; \sigma^2 \mid \mathcal{D}
    &\sim N(\overrightarrow{\hat{\beta}}, \sigma^2\mathbf{V}_{\beta})
    \end{aligned}$$

    - $\overrightarrow{\hat{\beta}}=(\mathbf{X}^{T}\mathbf{X})^{-1}\mathbf{X}^{T}\overrightarrow{y}$ : $\overrightarrow{\beta}$ 의 최우추정량
    - $\sigma^2\mathbf{V}_{\beta}=\sigma^2(\mathbf{X}^{T}\mathbf{X})^{-1}$ : $\overrightarrow{\beta}$ 의 공분산 행렬

## Informative Prior Determination
-----

### Liklihood Function

$$\begin{aligned}
\mathcal{L}(\beta, \sigma^2)
&= (2\pi\sigma^2)^{-n/2} \cdot \exp{\left[-\frac{1}{2\sigma^2}\cdot(\overrightarrow{y}-\mathbf{X}\overrightarrow{\beta})^{T}(\overrightarrow{y}-\mathbf{X}\overrightarrow{\beta})\right]} \quad (\because \overrightarrow{y} \sim N(\mathbf{X}\overrightarrow{\beta}, \sigma^2\mathbf{I}))\\
&\propto (\sigma^2)^{-n/2} \cdot \exp{\left[-\frac{1}{2\sigma^2}\cdot(\overrightarrow{y}-\mathbf{X}\overrightarrow{\beta})^{T}(\overrightarrow{y}-\mathbf{X}\overrightarrow{\beta})\right]}
\end{aligned}$$

### Setting Conjugate Prior of $\beta, \sigma^2$

$$
P(\beta, \sigma^2) = P(\beta ; \sigma^2) \cdot P(\sigma^2)
$$

- **Conjugate Prior of $\sigma^2$ is Scaled Inverse Chi-Squared Distribution**

    $$\begin{aligned}
    P(\sigma^2)
    &\propto (\sigma^2)^{-\nu_{0}/2-1} \cdot \exp{\left[-\frac{1}{2\sigma^2}\cdot \nu_{0} s_{0}^{2}\right]}\\
    &\propto \text{Scaled Inv-}\chi^2(\nu_{0}, s_{0}^{2})
    \end{aligned}$$

    - $\nu_{0}$ : 사전 자유도
    - $s_{0}^{2}$ : 사전 잔차 분산

- **Conjugate Prior of $\beta$ given $\sigma^2$ is Normal Distribution**

    $$\begin{aligned}
    P(\beta;\sigma^2)
    &\propto (\sigma^2)^{-(n-\nu_0)/2} \cdot \exp{\left[-\frac{1}{2\sigma^2}\cdot(\overrightarrow{\beta}-\overrightarrow{\mu}_0)^{T}\Lambda_{0}(\overrightarrow{\beta}-\overrightarrow{\mu}_0)\right]}\\
    &\propto N(\overrightarrow{\mu}_0, \sigma^2\Lambda_{0}^{-1})
    \end{aligned}$$

    - $\overrightarrow{\mu}_0$ : $\overrightarrow{\beta}$ 의 사전 평균
    - $\sigma^2\Lambda_{0}^{-1}$ : $\overrightarrow{\beta}$ 의 사전 공분산 행렬

### Posterior Estimation of $\beta, \sigma^2$

$$\begin{aligned}
P(\beta, \sigma^2 \mid \mathcal{D})
&\propto P(\mathcal{D} \mid \beta, \sigma^2) \cdot P(\beta, \sigma^2)\\
\\
&\propto (\sigma^2)^{-n/2} \cdot \exp{\left[-\frac{1}{2\sigma^2}\cdot(\overrightarrow{y}-\mathbf{X}\overrightarrow{\beta})^{T}(\overrightarrow{y}-\mathbf{X}\overrightarrow{\beta})\right]}\\
&\quad \times (\sigma^2)^{-\nu_{n}/2-1} \cdot \exp{\left[-\frac{1}{2\sigma^2}\cdot \nu_{n} s_{n}^{2}\right]}\\
&\quad \times (\sigma^2)^{-\frac{n-\nu_n}{2}} \cdot \exp{\left[-\frac{1}{2\sigma^2}\cdot(\overrightarrow{\beta}-\overrightarrow{\mu}_n)^{T}\Lambda_{n}(\overrightarrow{\beta}-\overrightarrow{\mu}_n)\right]}\\
\\
&= (\sigma^2)^{-\frac{n+\nu_n}{2}-1} \cdot \exp{\left[-\frac{1}{2\sigma^2}\left(\nu_n s^{2}_{n} + (\overrightarrow{y}-\mathbf{X}\overrightarrow{\beta})^{T}(\overrightarrow{y}-\mathbf{X}\overrightarrow{\beta})\right)\right]}\\
&\quad \times (\sigma^2)^{-\frac{n-\nu_n}{2}} \cdot \exp{\left[-\frac{1}{2\sigma^2}\cdot(\overrightarrow{\beta}-\overrightarrow{\mu}_n)^{T}\Lambda_{n}(\overrightarrow{\beta}-\overrightarrow{\mu}_n)\right]}
\end{aligned}$$

- **Posterior of $\sigma^2$ is Inverse-Gamma Distribution**

    $$\begin{aligned}
    P(\sigma^2 \mid \mathcal{D})
    &\propto (\sigma^2)^{-\frac{n+\nu_n}{2}-1} \cdot \exp{\left[-\frac{1}{2\sigma^2}\left(\nu_n s^{2}_{n} + (\overrightarrow{y}-\mathbf{X}\overrightarrow{\beta})^{T}(\overrightarrow{y}-\mathbf{X}\overrightarrow{\beta})\right)\right]}\\
    &\propto \text{Inv-Gamma}\left(\frac{n + \nu_n}{2}, \frac{1}{2} \left[\nu_n s_n^2 + (\overrightarrow{y} - \mathbf{X}\overrightarrow{\beta})^{T}(\overrightarrow{y} - \mathbf{X}\overrightarrow{\beta})\right]\right)
    \end{aligned}$$

    - $\nu_{n}$ : 사후 자유도
    - $s_{n}^{2}$ : 사후 잔차 분산

- **Posterior of $\beta$ given $\sigma^2$ is Normal Distribution**

    $$\begin{aligned}
    P(\beta;\sigma^2)
    &\propto (\sigma^2)^{-\frac{n-\nu_n}{2}} \cdot \exp{\left[-\frac{1}{2\sigma^2}\cdot(\overrightarrow{\beta}-\overrightarrow{\mu}_n)^{T}\Lambda_{n}(\overrightarrow{\beta}-\overrightarrow{\mu}_n)\right]}\\
    &\propto N(\overrightarrow{\mu}_n, \sigma^2\Lambda_{n}^{-1})
    \end{aligned}$$

    - $\overrightarrow{\mu}_n$ : $\overrightarrow{\beta}$ 의 사후 평균
    - $\sigma^2\Lambda_{n}^{-1}$ : $\overrightarrow{\beta}$ 의 사후 공분산 행렬
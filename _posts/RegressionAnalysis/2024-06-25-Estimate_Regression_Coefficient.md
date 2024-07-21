---
order: 2
title: Estimate Regression Coefficient
date: 2024-06-25
categories: [Statistical Techs, Regression Analysis]
tags: [Statistics, Regression, OLS]
math: true
description: >-
  Based on the lecture "Statistical Models and Application (2024-1)" by Prof. Yeo Jin Chung, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
  path: /_post_refer_img/RegressionAnalysis/Thumbnail.jpg
---

## Ordinary Least Squares
-----

![01](/_post_refer_img/RegressionAnalysis/02-01.png){: width="100%"}

- **최소자승법(Ordinary Least Squares; OLS)** : 잔차 자승의 합을 최소화하는 회귀계수를 추정하는 방법

    $$\begin{aligned}
    \hat{\beta}_{0}, \hat{\beta}_{1}
    &= \text{arg} \min_{\theta}{\sum_{i=1}^{n}{\varepsilon_{i}^{2}}}\\
    &= \text{arg} \min_{\theta}{\sum_{i=1}^{n}{\left(y_{i} - \hat{y}_{i} \right)^{2}}}\\
    &= \text{arg} \min_{\theta}{\sum_{i=1}^{n}{\left[ y_{i} - \left(\beta_{0} + \beta_{1} x_{i} \right) \right]^2}}
    \end{aligned}$$

- **최소자승추정량(OLS Estimator)**
    - 편향 $$\beta_{0}$$ 의 최소자승추정량 $$\hat{\beta}_{0} = \overline{Y} - \hat{\beta}_{1} \overline{X}$$
    - 가중치 $$\beta_{1}$$ 의 최소자승추정량 $$\hat{\beta}_{1} = \displaystyle\frac{Cov(X,Y)}{Var(X)}$$

### OLS Estimator

- $Loss(\beta_0, \beta_1)=\displaystyle\sum_{i=1}^{n}{\varepsilon_{i}^{2}}$ 을 $\beta_0$ 으로 편미분

    $$\begin{aligned}
    &\frac{\partial}{\partial \beta_0}Loss(\beta_0, \beta_1)\\
    &= -2 \times \sum_{i=1}^{n}{\left[y_{i}-\left(\beta_0 + \beta_1 x_{i}\right)\right]} \\
    &= -2 \times \left[\sum_{i=1}^{n}{y_{i}} - n \beta_{0}-\beta_{1} \sum_{i=1}^{n}{x_{i}} \right] \cdots ①\\
    &= -2n \times (\overline{Y} - \beta_0 - \beta_1 \overline{X}) \\
    &= 0
    \end{aligned}$$

- 편향 $\beta_0$ 의 최소자승추정량 $\hat{\beta}_{0}$ 도출

    $$
    \therefore
    \hat{\beta_0}
    = \overline{Y} - \hat{\beta_1}\overline{X} \quad (\text{s.t.} \; n \ne 0)
    $$

- $Loss(\beta_0, \beta_1)=\displaystyle\sum_{i=1}^{n}{e_{i}^{2}}$ 을 $\beta_0$ 으로 편미분

    $$\begin{aligned}
    &\frac{\partial}{\partial \beta_1} Loss(\beta_0, \beta_1)\\
    &= -2\times\sum_{i=1}^{n}{\left[y_{i}-\left(\beta_0+\beta_1 x_{i}\right)\right] \times x_{i}}\\
    &= -2\times\left[\sum_{i=1}^{n}{y_{i}x_{i}}-\beta_0\sum_{i=1}^{n}{x_{i}}-\beta_1\sum_{i=1}^{n}{x_{i}^2}\right] \cdots ② \\
    &= 0
    \end{aligned}$$

- 식 $①$ 변형

    $$\begin{aligned}
    & -\frac{1}{2} \times ① \times \sum_{i=1}^{n}{x_{i}}\\
    &= \sum_{i=1}^{n}{x_{i}} \sum_{i=1}^{n}{x_{i}} - n \beta_{0} \sum_{i=1}^{n}{x_{i}} - \beta_{1} \sum_{i=1}^{n}{x_{i}} \sum_{i=1}^{n}{x_{i}}\\
    &= n^{2}\overline{Y}\overline{X} - n^{2}\beta_{0}\overline{X}-n^{2}\beta_{1}\left(\overline{X}\right)^{2}\\
    &= 0
    \end{aligned}$$

- 식 $②$ 변형

    $$\begin{aligned}
    & -\frac{1}{2} \times ② \times n \\
    &= n \sum_{i=1}^{n}{y_{i}x_{i}} - n \beta_0 \sum_{i=1}^{n}{x_{i}} - n \beta_1 \sum_{i=1}^{n}{(x_{i})^2}\\
    &= n \sum_{i=1}^{n}{y_{i}x_{i}} - n^{2} \beta_0 \overline{X} - n \beta_1 \sum_{i=1}^{n}{x_{i}^2}\\
    &= 0
    \end{aligned}$$

- 식 ①, ② 의 변형을 뺄셈

    $$\begin{aligned}
    & -\frac{1}{2} \left(① \times \displaystyle\sum_{i=1}^{n}X_i - ② \times n \right)\\
    &= \left[n^{2}\overline{Y}\overline{X} - n^{2}\beta_{1}\left(\overline{X}\right)^{2}\right] -  \left[n \sum_{i=1}^{n}{y_{i}x_{i}} - n \beta_1 \sum_{i=1}^{n}{(x_{i})^2}\right]\\
    &= \beta_1 \times n^{2}\left[\frac{1}{n}\sum_{i=1}^{n}{x_{i}^2}-\left(\overline{X}\right)^{2}\right] - n^{2}\left[\frac{1}{n}\sum_{i=1}^{n}{y_{i}x_{i}}-\overline{Y}\overline{X}\right]\\
    &= \beta_1 \times n^{2} Var\left[X\right] - n^{2} Cov\left[Y,X\right]\\
    &= 0
    \end{aligned}$$

- 가중치 $\beta_1$ 의 최소자승추정량 $\hat{\beta}_{1}$ 도출

    $$
    \hat{\beta}_{1}
    = \frac{Cov\left[Y,X\right]}{Var\left[X\right]}
    $$

## Gauss-Markov Theorem
-----

> 고전적 선형 회귀 가정(Classical Linear Regression Assumptions) 하 최소자승추정량은 선형 불편 추정량 중 분산이 가장 작은 추정량(Best Linear Unbiased Estimator; BLUE)이다.

- **가중치 $\beta_{1}$ 의 최소자승추정량 $\hat{\beta}_{1}$ 의 확률분포**

    $$
    \hat{\beta}_{1} \sim N\left(\beta_{1}, \sigma^2\left[\displaystyle\frac{1}{\sum_{i=1}^{n}{(x_{i}-\overline{x})^2}}\right]\right)
    $$

- **편향 $\beta_{0}$ 의 최소자승추정량 $\hat{\beta}_{0}$ 의 확률분포**

    $$
    \hat{\beta}_{0} \sim N\left(\beta_{0}, \sigma^{2} \left[\displaystyle\frac{1}{n} + \displaystyle\frac{\overline{x}^{2}}{\sum_{i=1}^{n}{(x_{i}-\overline{x})^2}}\right]\right)
    $$

- **오차항 $\varepsilon$ 의 모분산 $\sigma^2$ 을 그 표본분산으로 추정함**

    $$
    \sigma^2 \xrightarrow{\text{P}} \displaystyle\frac{\text{RSS}}{n-2}
    $$

## OLS Estimator is Unbiasedness Estimator
-----

$$
\mathbb{Bias}\left[\hat{\beta}\right]=\mathbb{E}\left[\hat{\beta}-\beta\right]=0
$$

### $\hat{\beta}_{1}$

$$\begin{aligned}
\hat{\beta}_{1}
&= \frac{\sum_{i=1}^{n}{(x_{i}-\overline{x})(y_{i}-\overline{y})}}{\sum_{i=1}^{n}{(x_{i}-\overline{x})^{2}}}\\
\\
y_{i}
&= \beta_{0}+\beta_{1}x_{i}+\varepsilon_{i}\\
\overline{y}
&= \beta_{0}+\beta_{1}\overline{x}+\varoverline{\epsilon}\\
\\
\therefore
(y_{i}-\overline{y})
&= \beta_{1}(x_{i}-\overline{x}) + (\varepsilon_{i}-\overline{\epsilon})\\
\\
\therefore
(x_{i}-\overline{x})(y_{i}-\overline{y})
&= \beta_{1}(x_{i}-\overline{x})^{2} + \varepsilon_{i}(x_{i}-\overline{x}) = \overline{\epsilon}(x_{i}-\overline{x})\\
\\
\therefore
\hat{\beta}_{1}
&= \beta_{1}+\frac{\sum_{i=1}^{n}{(x_{i}-\overline{x})\epsilon_{i}}}{\sum_{i=1}^{n}{(x_{i-\overline{x}})^2}}+\overline{\epsilon} \cdot \frac{\sum_{i=1}^{n}{(x_{i}-\overline{x})}}{\sum_{i=1}^{n}{(x_{i}-\overline{x})^2}}\\
&= \beta_{1}+\frac{\sum_{i=1}^{n}{(x_{i}-\overline{x})\varepsilon_{i}}}{\sum_{i=1}^{n}{(x_{i-\overline{x}})^2}} \quad \text{s.t.}\;\epsilon \sim N(0,\sigma^2)\\
\\
\mathbb{E}\left[\hat{\beta}_{1}\right]
&= \beta_{1} + \mathbb{E}\left[\frac{\sum_{i=1}^{n}{(x_{i}-\overline{x})\varepsilon_{i}}}{\sum_{i=1}^{n}{(x_{i}-\overline{x})^2}}\right]\\
&= \beta_{1} + \frac{\sum_{i=1}^{n}{(x_{i}-\overline{x}) \mathbb{E}\left[\varepsilon_{i}\right]}}{\sum_{i=1}^{n}{(x_{i}-\overline{x})^2}} \quad \text{s.t.}\;\mathbb{E}\left[\epsilon_{i}\vert x_{i}\right]=\mathbb{E}\left[\varepsilon_{i}\right]\\
&= \beta_{1} \quad \text{s.t.}\;\epsilon \sim N(0,\sigma^2)
\end{aligned}$$

### $\hat{\beta}_{0}$

$$\begin{aligned}
\hat{\beta}_{0}
&= \overline{y} - \hat{\beta}_{1}\overline{x}\\
\\
\overline{y}
&= \beta_{0} + \beta_{1}\overline{x}\\
\\
\therefore
\hat{\beta}_{0}
&= \beta_{0} + \beta_{1}\overline{x} - \hat{\beta}_{1}\overline{x}\\
\\
\mathbb{E}\left[\hat{\beta}_{0}\right]
&= \beta_{0} + \mathbb{E}\left[\beta_{1}\overline{x}\right] - \mathbb{E}\left[\hat{\beta}_{1}\overline{x}\right]\\
&= \beta_{0} + \overline{x}\cdot\mathbb{E}\left[\beta_{1}\right] - \overline{x}\cdot\mathbb{E}\left[\hat{\beta}_{1}\right]\\
&= \beta_{0} + \overline{x} \cdot \beta_{1} - \overline{x} \cdot \beta_{1} \quad \left(\because \mathbb{E}\left[\hat{\beta}_{1}\right] = \beta_{1} \right)\\
&= \beta_{0}
\end{aligned}$$

## OLS Estimator is Efficiency Estimator
-----

$$
\hat{\beta}_{OLS}=\text{arg} \min{\mathbb{Var}\left[\hat{\beta}\right]}
$$

### $\hat{\beta}_{1}$

$$\begin{aligned}
\hat{\beta}_{1}
&= \frac{\sum_{i=1}^{n}{(x_{i}-\overline{x})(y_{i}-\overline{y})}}{\sum_{i=1}^{n}{(x_{i}-\overline{x})^{2}}}\\
&= \beta_{1}+\frac{\sum_{i=1}^{n}{(x_{i}-\overline{x})\varepsilon_{i}}}{\sum_{i=1}^{n}{(x_{i}-\overline{x})^{2}}} \quad \text{s.t.}\;\epsilon \sim N(0,\sigma^2)\\
\\
\mathbb{Var}\left[\hat{\beta}_{1}\right]
&= \mathbb{Var}\left[\beta_{1}+\frac{\sum_{i=1}^{n}{(x_{i}-\overline{x})\varepsilon_{i}}}{\sum_{i=1}^{n}{(x_{i}-\overline{x})^{2}}}\right]\\
&= \mathbb{Var}\left[\frac{\sum_{i=1}^{n}{(x_{i}-\overline{x})\varepsilon_{i}}}{\sum_{i=1}^{n}{(x_{i}-\overline{x})^{2}}}\right]\\
&= \left(\frac{1}{\sum_{i=1}^{n}{(x_{i}-\overline{x})^{2}}}\right)^{2} \cdot \mathbb{Var}\left[\sum_{i=1}^{n}{(x_{i}-\overline{x})\varepsilon_{i}}\right] \quad \text{s.t.}\;\mathbb{E}\left[\varepsilon_{i} \vert x_{i}\right] = \mathbb{E}\left[\varepsilon_{i}\right]\\
\\
\mathbb{Var}\left[\sum_{i=1}^{n}{(x_{i}-\overline{x})\epsilon_{i}}\right]
&= \sum_{i=1}^{n}{\mathbb{Var}\left[(x_{i}-\overline{x})\varepsilon_{i}\right]} \quad \text{s.t.} \; \mathbb{Cov}\left[\varepsilon_{i},\varepsilon_{j}\right]=0\\
&= \sum_{i=1}^{n}{(x_{i}-\overline{x})^{2}\mathbb{Var}\left[\varepsilon_{i}\right]} \quad \text{s.t.} \; \mathbb{E}\left[\varepsilon_{i} \vert x_{i}\right]=\mathbb{E}\left[\varepsilon_{i}\right]\\
&= \sigma^{2}\sum_{i=1}^{n}{(x_{i}-\overline{x})^{2}} \quad \text{s.t.}\;\epsilon \sim N(0, \sigma^2)\\
\\
\therefore
\mathbb{Var}\left[\hat{\beta}_{1}\right]
&= \left(\frac{1}{\sum_{i=1}^{n}{(x_{i}-\overline{x})^{2}}}\right)^{2} \cdot \sigma^{2}\sum_{i=1}^{n}{(x_{i}-\overline{x})^{2}}\\
&= \sigma^2 \cdot \left[\frac{1}{\sum_{i=1}^{n}{(x_{i}-\overline{x})^2}} \right]
\end{aligned}$$

### $\hat{\beta}_{0}$

$$\begin{aligned}
\hat{\beta}_{0}
&= \overline{y} - \hat{\beta}_{1}\overline{x}\\
\\
\mathbb{Var}\left[\hat{\beta}_{0}\right]
&= \mathbb{Var}\left[\overline{y} - \hat{\beta}_{1}\overline{x}\right]\\
&= \mathbb{Var}\left[\overline{y}\right] + \mathbb{Var}\left[\hat{\beta}_{1}\overline{x}\right] - \mathbb{Cov}\left[\overline{y}, \hat{\beta}_{1}\overline{x}\right]
\end{aligned}$$

- $\mathbb{Var}\left[\overline{y}\right]$

    $$\begin{aligned}
    \mathbb{Var}\left[\overline{y}\right]
    &= \mathbb{Var}\left[\frac{1}{n}\sum_{i=1}^{n}{y_{i}}\right]\\
    &= \left(\frac{1}{n}\right)^{2} \cdot \mathbb{Var}\left[\sum_{i=1}^{n}{y_{i}}\right]\\
    &= \left(\frac{1}{n}\right)^{2} \cdot \sum_{i=1}^{n}{\mathbb{Var}\left[y_{i}\right]} \quad \text{s.t.}\;\mathbb{Cov}\left[\varepsilon_{i},\varepsilon_{j}\right]=0\\
    &= \left(\frac{1}{n}\right)^{2} \cdot \sum_{i=1}^{n}{\mathbb{Var}\left[\varepsilon_{i}\right]} \quad \left(\because y_{i}=\beta_{0} + \beta_{1}x_{i} + \varepsilon_{i} \right)\\
    &= \frac{\sigma^2}{n} \quad \text{s.t.}\;\epsilon \sim N(0, \sigma^2)
    \end{aligned}$$

- $\mathbb{Var}\left[\hat{\beta}_{1}\overline{x}\right]$

    $$\begin{aligned}
    \mathbb{Var}\left[\hat{\beta}_{1}\overline{x}\right]
    &= \overline{x}^{2} \cdot \mathbb{Var}\left[\hat{\beta}_{1}\right]\\
    &= \overline{x}^{2} \cdot \frac{\sigma^2}{\sum_{i=1}^{n}{(x_{i}-\overline{x})^2}}
    \end{aligned}$$

- $\mathbb{Cov}\left[\overline{y}, \hat{\beta}_{1}\overline{x}\right]$

    $$\begin{aligned}
    \mathbb{Cov}\left[\overline{y}, \hat{\beta}_{1}\overline{x}\right]
    &= \mathbb{Cov}\left[\beta_{0}+\beta_{1}\overline{x}+\overline{\epsilon}, \hat{\beta}_{1}\overline{x}\right]\\
    &= \overline{x} \cdot \mathbb{Cov}\left[\overline{\epsilon},\hat{\beta}_{1}\right]\\
    &= \overline{x} \cdot \mathbb{E}\left[\left(\hat{\beta}_{1}-\mathbb{E}\left[\hat{\beta}_{1}\right]\right)\cdot\left(\overline{\epsilon}-\mathbb{E}\left[\overline{\epsilon}\right]\right)\right]\\
    &= \overline{x} \cdot \mathbb{E}\left[\left(\hat{\beta}_{1}-\beta_{1}\right)\cdot\left(\overline{\epsilon}-\mathbb{E}\left[\overline{\epsilon}\right]\right)\right] \quad (\because \mathbb{E}\left[\hat{\beta}_{1}\right] = \beta_{1})\\
    &= \overline{x} \cdot \mathbb{E}\left[\left(\hat{\beta}_{1}-\beta_{1}\right)\cdot\left(0-0\right)\right] \quad \text{s.t.} \; \epsilon \sim N(0, \sigma^2)\\
    &= 0
    \end{aligned}$$

- $\mathbb{Var}\left[\hat{\beta}_{0}\right]$

    $$\begin{aligned}
    \mathbb{Var}\left[\hat{\beta}_{0}\right]
    &= \mathbb{Var}\left[\overline{y}\right] + \mathbb{Var}\left[\hat{\beta}_{1}\overline{x}\right] - \mathbb{Cov}\left[\overline{y}, \hat{\beta}_{1}\overline{x}\right]\\
    &= \frac{\sigma^2}{n} + \overline{x}^{2} \cdot \frac{\sigma^2}{\sum_{i=1}^{n}{(x_{i}-\overline{x})^2}} + 0\\
    &= \sigma^2 \cdot \left[\frac{1}{n} + \frac{\overline{x}^{2}}{\sum_{i=1}^{n}{(x_{i}-\overline{x})^2}}\right]
    \end{aligned}$$

-----

### 이미지 출처

- https://medium.com/@luvvaggarwal2002/linear-regression-in-machine-learning-9e8af948d3eb
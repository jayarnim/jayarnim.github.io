---
order: 4
title: Regression Diagnostics
date: 2024-07-11
categories: [Statistical Techs, Regression Analysis]
tags: [Statistics, Regression]
math: true
description: >-
    Based on the following lectures <br>
    (1) “Statistics (2018-1)” by Prof. Sang Ah Lee, Dept. of Economics, College of Economics & Commerce, Kookmin Univ. <br>
    (2) “Intro. to Machine Learning (2023-2)” by Prof. Je Hyuk Lee, Dept. of Data Science, The Grad. School, Kookmin Univ. <br>
    (3) "Statistical Models and Application (2024-1)" by Prof. Yeo Jin Chung, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
    path: /_post_refer_img/RegressionAnalysis/Thumbnail.jpg
---

## Regression Diagnostics
-----

- **회귀 진단(Regression Diagnostics)** : 고전적 선형 회귀 가정이 위배되는지 진단하는 절차

- **고전적 선형 회귀 가정이 위배됨에 따라 발생하는 문제점**
    - `A.1` 반응변수와 설명변수 간 비선형성 문제(Non-linearity Problem)
    - `A.2` 오차항 간 상관성 문제(Auto-correlation Problem)
    - `A.3` 이상치 및 영향점 문제(Outlier & Influential Points Problem)
    - `A.4` 오차항의 이분산성 문제(Hetero-scedasticity Problem)
    - `A.5` 설명변수 간 다중공선성 문제(Multi-col-linearity Problem)

## Non-linearity Problem
-----

- $Y$ 가 $X$ 의 선형 결합이 아니라고 하자

    $$\begin{aligned}
    y_i= f(x_i)+\varepsilon_i
    \end{aligned}$$

- 최소자승추정량 $$\hat{\beta}_{1}$$ 을 다음과 같이 이해할 수 있음

    $$\begin{aligned}
    \hat{\beta}_{1}
    &= \frac{\sum_{i=1}^{n}{(x_i - \overline{x})(y_i - \overline{y})}}{\sum_{i=1}^{n}{(x_i - \overline{x})^2}}\\
    &= \frac{\sum_{i=1}^{n}{(x_i - \overline{x})(f(x_i)+\varepsilon_i - \overline{f(x)} - \overline{\varepsilon})}}{\sum_{i=1}^{n}{(x_i - \overline{x})^2}}\\
    &= \frac{\sum_{i=1}^{n}{(x_i-\overline{x})(f(x_i)-\overline{f(x)})}}{\sum_{i=1}^{n}{(x_i - \overline{x})^2}} + \frac{\sum_{i=1}^{n}{(x_i-\overline{x})(\varepsilon_i-\overline{\varepsilon})}}{\sum_{i=1}^{n}{(x_i - \overline{x})^2}}\\
    &= \frac{\sum_{i=1}^{n}{(x_i-\overline{x})(f(x_i)-\overline{f(x)})}}{\sum_{i=1}^{n}{(x_i - \overline{x})^2}} + \frac{\sum_{i=1}^{n}{(x_i-\overline{x}) \cdot \varepsilon_i}}{\sum_{i=1}^{n}{(x_i - \overline{x})^2}} - \frac{\sum_{i=1}^{n}{(x_i-\overline{x}) \cdot \overline{\varepsilon}}}{\sum_{i=1}^{n}{(x_i - \overline{x})^2}}\\
    &= \frac{\sum_{i=1}^{n}{(x_i-\overline{x})(f(x_i)-\overline{f(x)})}}{\sum_{i=1}^{n}{(x_i - \overline{x})^2}} + \sum_{i=1}^{n}{w_i \cdot \varepsilon_i}
    \end{aligned}$$

- $$\hat{\beta}_{1}$$ 의 기대값은 다음과 같음

    $$\begin{aligned}
    \mathbb{E}\left[\hat{\beta}_{1}\right]
    &= \mathbb{E}\left[\frac{\sum_{i=1}^{n}{(x_i-\overline{x})(f(x_i)-\overline{f(x)})}}{\sum_{i=1}^{n}{(x_i - \overline{x})^2}} + \sum_{i=1}^{n}{w_i \cdot \varepsilon_i}\right]\\
    &= \mathbb{E}\left[\frac{\sum_{i=1}^{n}{(x_i-\overline{x})(f(x_i)-\overline{f(x)})}}{\sum_{i=1}^{n}{(x_i - \overline{x})^2}}\right] + \mathbb{E}\left[\sum_{i=1}^{n}{w_i \cdot \varepsilon_i}\right]\\
    &= \mathbb{E}\left[\frac{\sum_{i=1}^{n}{(x_i-\overline{x})(f(x_i)-\overline{f(x)})}}{\sum_{i=1}^{n}{(x_i - \overline{x})^2}}\right] + \sum_{i=1}^{n}{\mathbb{E}\left[w_i\right] \cdot \mathbb{E}\left[\varepsilon_i\right]} \quad \text{s.t.} \quad X \perp \varepsilon\\
    &= \mathbb{E}\left[\frac{\sum_{i=1}^{n}{(x_i-\overline{x})(f(x_i)-\overline{f(x)})}}{\sum_{i=1}^{n}{(x_i - \overline{x})^2}}\right] + \sum_{i=1}^{n}{\mathbb{E}\left[w_i\right] \cdot 0} \quad (\because \varepsilon \sim N(0,\sigma^2))\\
    &= \mathbb{E}\left[\frac{\sum_{i=1}^{n}{(x_i-\overline{x})(f(x_i)-\overline{f(x)})}}{\sum_{i=1}^{n}{(x_i - \overline{x})^2}}\right]
    \end{aligned}$$

- 따라서 $$\hat{\beta}_{1}$$ 은 $$\beta_{1}$$ 의 불편추정량이 될 수 없음

    $$\begin{aligned}
    \mathbb{Bias}\left[\hat{\beta}_{1}\right]
    &= \mathbb{E}\left[\hat{\beta}_{1}\right] - \beta_1\\
    &= \mathbb{E}\left[\frac{\sum_{i=1}^{n}{(x_i-\overline{x})(f(x_i)-\overline{f(x)})}}{\sum_{i=1}^{n}{(x_i - \overline{x})^2}}\right] - \beta_1\\
    &\ne 0
    \end{aligned}$$

## Auto-correlation Problem
-----

- 최소자승추정량 $$\hat{\beta}_{1}$$ 의 분산은 다음과 같음

    $$\begin{aligned}
    \mathbb{Var}\left[\hat{\beta}_{1}\right]
    &= \mathbb{Var}\left[\beta_1 + \sum_{i=1}^{n}{w_i \cdot \varepsilon_i}\right]\\
    &= \mathbb{Var}\left[\sum_{i=1}^{n}{w_i \cdot \varepsilon_i}\right]\\
    &= \sum_{i=1}^{n}{w_{i}^{2} \cdot \sigma_{i}^{2}} + \sum_{i}\sum_{j \ne i}{w_{i} \cdot w_{j} \cdot \mathbb{Cov}\left[\varepsilon_{i}, \varepsilon_{j}\right]}\\
    &= \sigma^{2}\sum_{i=1}^{n}{w_{i}^{2}} + \sum_{i}\sum_{j \ne i}{w_{i} \cdot w_{j} \cdot \mathbb{Cov}\left[\varepsilon_{i}, \varepsilon_{j}\right]} \quad (\because \sigma_{i^{\forall}}^{2}=\sigma^{2})
    \end{aligned}$$

- $\mathbb{Cov}\left[\varepsilon_{i}, \varepsilon_{j}\right] \ne 0$ 이므로 최소분산성을 보장할 수 없음

    $$\begin{aligned}
    \sigma^{2}\sum_{i=1}^{n}{w_{i}^{2}} \le \sigma^{2}\sum_{i=1}^{n}{w_{i}^{2}} + \sum_{i}\sum_{j \ne i}{w_{i} \cdot w_{j} \cdot \mathbb{Cov}\left[\varepsilon_{i}, \varepsilon_{j}\right]}
    \end{aligned}$$

## Hetero-scedasticity Problem
-----

- 최소자승추정량 $$\hat{\beta}_{1}$$ 의 분산은 다음과 같음

    $$\begin{aligned}
    \mathbb{Var}\left[\hat{\beta}_{1}\right]
    &= \mathbb{Var}\left[\beta_1 + \sum_{i=1}^{n}{w_i \cdot \varepsilon_i}\right]\\
    &= \mathbb{Var}\left[\sum_{i=1}^{n}{w_i \cdot \varepsilon_i}\right]\\
    &= \sum_{i=1}^{n}{w_{i}^{2} \cdot \sigma_{i}^{2}} + \sum_{i}\sum_{j \ne i}{w_{i} \cdot w_{j} \cdot \mathbb{Cov}\left[\varepsilon_{i}, \varepsilon_{j}\right]}\\
    &= \sum_{i=1}^{n}{w_{i}^{2} \cdot \sigma_{i}^{2}} \quad (\because \mathbb{Cov}\left[\varepsilon_{i}, \varepsilon_{j}\right] = 0)
    \end{aligned}$$

- $\sigma_{i}^{2} \ne \sigma_{j \ne i}^{2}$ 이므로 최소분산성을 보장할 수 없음

    $$\begin{aligned}
    \sigma^{2}\cdot\sum_{i=1}^{n}{w_{i}^{2}} \le \sum_{i=1}^{n}{w_{i}^{2} \cdot \sigma_{i}^{2}}
    \end{aligned}$$

## Multi-col-linearity Problem
-----

- 반응변수 $Y$ 가 설명변수 $X_1, X_2$ 의 선형 결합이라고 하자

    $$\begin{aligned}
    Y = \beta_0 + \beta_1 \cdot X_1 + \beta_2 \cdot X_2 + \varepsilon
    \end{aligned}$$

- 설명변수 $X_1$ 에 대한 가중치 $\beta_1$ 의 의미

    $$\begin{aligned}
    \beta_1
    &= \frac{\partial Y}{\partial X_1}
    \end{aligned}$$

- 설명변수 $X_1$ 에 대한 가중치 $\beta_1$ 의 최소자승추정량 $\hat{\beta}_{1}$

    $$\begin{aligned}
    \hat{\beta}_{1}
    &= \frac{\sum_{i=1}^{n}{(x^{(i)}_{1}-\overline{x}_{1})(y^{(i)}-\overline{y})}}{\sum_{i=1}^{n}{(x^{(i)}_{1}-\overline{x}_{1})^{2}}} - \frac{\sum_{i=1}^{n}{(x^{(i)}_{1}-\overline{x}_{1})(x^{(i)}_{2}-\overline{x}_{2})}}{\sum_{i=1}^{n}{(x^{(i)}_{1}-\overline{x}_{1})^{2}}} \cdot \hat{\beta}_{2}\\
    &= \frac{\mathbb{Cov}\left[X_1, Y\right]}{\mathbb{Var}\left[X_1\right]} - \frac{\mathbb{Cov}\left[X_1, X_2\right]}{\mathbb{Var}\left[X_1\right]} \cdot \hat{\beta}_{2}
    \end{aligned}$$

- $X_2$ 가 $X_1$ 의 선형 결합으로 표현될 수 있다고 하자

    $$\begin{aligned}
    X_2 = \delta + \alpha \cdot X_1 + \epsilon
    \end{aligned}$$

- $$\mathbb{Cov}\left[X_1, X_2\right] \ne 0$$ 이므로 $$\hat{\beta}_{1}$$ 은 $$\hat{\beta}_{2}$$ 를 포함하게 되어 $$Y$$ 에 대한 $$X_1$$ 만의 순수한 설명력을 의미한다고 해석할 수 없음

    $$\begin{aligned}
    Y
    &= \beta_0 + \beta_1 \cdot X_1 + \beta_2 \cdot X_2 + \varepsilon\\
    &= \beta_0 + \beta_1 \cdot X_1 + \beta_2 \cdot \left(\delta + \alpha \cdot X_1\right) + \varepsilon\\
    &= \left(\beta_0 + \delta \cdot \beta_2 \right) + \left(\beta_1 + \alpha \cdot \beta_2\right) \cdot X_1 + \varepsilon
    \end{aligned}$$
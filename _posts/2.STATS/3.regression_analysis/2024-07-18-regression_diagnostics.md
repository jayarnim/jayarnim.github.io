---
order: 4
title: Regression Diagnostics
date: 2024-07-18
categories: [2.STATISTICAL TECHS, 3.regression analysis]
tags: [statistics, regression analysis, linear regression analysis, numerical data analysis]
math: true
description: >-
    Based on the following lectures <br>
    (1) “Statistics (2018-1)” by Prof. Sang Ah Lee, Dept. of Economics, College of Economics & Commerce, Kookmin Univ. <br>
    (2) “Intro. to Machine Learning (2023-2)” by Prof. Je Hyuk Lee, Dept. of Data Science, The Grad. School, Kookmin Univ. <br>
    (3) "Statistical Models and Application (2024-1)" by Prof. Yeo Jin Chung, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
    path: /_post_refer_img/2.STATS/3.regression_analysis/Thumbnail.jpg
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

### Durbin-Watson Statistic

- **더빈-왓슨 통계량(Durbin-Watson Statistic)** : 잔차의 1차 자기상관성을 측정하는 지표

    $$\begin{aligned}
    DW
    &= \frac{\sum_{t=2}^{n}{(\varepsilon_{t}-\varepsilon_{t-1})^{2}}}{\sum_{t=1}^{n}{(\varepsilon_{t})^{2}}}
    \end{aligned}$$

    - $DW \approx 0$ : 양의 자기상관이 매우 강함
    - $DW \approx 2$ : 자기상관 없음
    - $DW \approx 4$ : 음의 자기상관이 매우 강함

- $0\le DW \le 4 \quad (\because -1 \le \rho \le 1)$

    - $DW$ 의 분자를 다음과 같이 세분화할 수 있음

        $$\begin{aligned}
        \sum_{t=2}^{n}{(\varepsilon_{t}-\varepsilon_{t-1})^{2}}
        &= \sum_{t=2}^{n}{\varepsilon_{t}^2} + \sum_{t=2}^{n}{\varepsilon_{t-1}^2} - 2 \cdot \sum_{t=2}^{n}{\varepsilon_{t} \cdot \varepsilon_{t-1}}\\
        \end{aligned}$$

    - $n$ 이 매우 클 경우 다음이 성립함

        $$\begin{aligned}
        \sum_{t=2}^{n}{\varepsilon_{t}^2}
        &\approx \sum_{t=2}^{n}{\varepsilon_{t-1}^2}\\

        \therefore \sum_{t=2}^{n}{\varepsilon_{t}^2} + \sum_{t=2}^{n}{\varepsilon_{t-1}^2}
        &\approx 2 \cdot \sum_{t=2}^{n}{\varepsilon_{t}^2}
        \end{aligned}$$

    - 자기상관계수 $\rho$ 의 정의에 의해 다음이 성립함

        $$\begin{aligned}
        \rho
        &= \frac{\sum_{t=2}^{n}{(\varepsilon_{t}-\overline{\varepsilon})(\varepsilon_{t-1}-\overline{\varepsilon})}}{\sum_{t=1}^{n}{(\varepsilon_{t}-\overline{\varepsilon})^{2}}}\\
        &= \frac{\sum_{t=2}^{n}{\varepsilon_{t} \cdot \varepsilon_{t-1}}}{\sum_{t=1}^{n}{(\varepsilon_{t})^{2}}} \quad(\because \varepsilon \sim N(0, \sigma^2))\\
        \therefore \sum_{t=2}^{n}{\varepsilon_{t} \cdot \varepsilon_{t-1}}
        &= \rho \cdot \sum_{t=1}^{n}{(\varepsilon_{t})^{2}}
        \end{aligned}$$

    - 따라서 분자를 다음과 같이 이해할 수 있음

        $$\begin{aligned}
        \therefore \sum_{t=2}^{n}{(\varepsilon_{t}-\varepsilon_{t-1})^{2}}
        &= \sum_{t=2}^{n}{\varepsilon_{t}^2} + \sum_{t=2}^{n}{\varepsilon_{t-1}^2} - 2 \cdot \sum_{t=2}^{n}{\varepsilon_{t} \cdot \varepsilon_{t-1}}\\
        &\approx 2 \cdot \sum_{t=2}^{n}{\varepsilon_{t}^2} - 2 \cdot \rho \cdot \sum_{t=1}^{n}{\varepsilon_{t}^{2}}\\
        &\approx 2(1-\rho) \cdot \sum_{t=1}^{n}{\varepsilon_{t}^{2}}
        \end{aligned}$$

    - 따라서 $DW$ 는 $\rho$ 와 다음의 관계가 성립함

        $$\begin{aligned}
        \therefore DW
        &= \frac{\sum_{t=2}^{n}{(\varepsilon_{t}-\varepsilon_{t-1})^{2}}}{\sum_{t=1}^{n}{(\varepsilon_{t})^{2}}}\\
        &\approx 2(1-\rho) \cdot \frac{\sum_{t=1}^{n}{\varepsilon_{t}^{2}}}{\sum_{t=1}^{n}{\varepsilon_{t}^{2}}}\\
        &= 2(1-\rho)
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

### Breusch-Pagan Test

- **브레쉬-파건 검정(Breusch-Pagan Test)** : 잔차의 등분산성에 관한 검정

- **관심 모수 $\sigma^2$ 의 점 추정량 도출**

    - 다중선형회귀모형에서 $i$ 번째 관측치의 잔차 $\varepsilon^{(i)}$ 는 다음과 같이 정의됨

        $$\begin{aligned}
        y^{(i)}
        &= \hat{\beta}_{0} + \hat{\beta}_{1} \cdot x^{(i)}_{1} + \cdots + \hat{\beta}_{p} \cdot x^{(i)}_{p} + \varepsilon^{(i)}\\
        \varepsilon^{(i)}
        &= y^{(i)} - \left(\hat{\beta}_{0} + \hat{\beta}_{1} \cdot x^{(i)}_{1} + \cdots + \hat{\beta}_{p} \cdot x^{(i)}_{k} \right)
        \end{aligned}$$

    - 잔차 자승 $\varepsilon^{2}$ 은 오차 분산 $\sigma^2$ 의 간접적인 추정치임

        $$\begin{aligned}
        \hat{\sigma}^{2}
        &= \frac{1}{n-(p+1)} \cdot \sum_{i=1}^{n}{(\varepsilon_{i} - \overline{\varepsilon})^{2}}\\
        &= \frac{1}{n-(p+1)} \cdot \sum_{i=1}^{n}{\varepsilon_{i}^{2}} \quad (\because \varepsilon \sim N(0,\sigma^2))
        \end{aligned}$$

- **귀무가설과 대립가설 설정**
    - $H_0:\quad \sigma_{i}^2 = \sigma_{j\ne i}^2$
    - $H_1:\quad \sigma_{i}^2 \ne \sigma_{j\ne i}^2$

- **검정통계량 도출**

    $$
    BP \sim \chi^{2}(p)
    $$

    - 잔차 자승 $\varepsilon_{i}^{2}$ 에 대한 보조회귀모형 정의

        $$\begin{aligned}
        \varepsilon_{i}^{2}
        &= \gamma_{0} + \gamma_{1} \cdot x^{(i)}_{1} + \cdots + \gamma_{k} \cdot x^{(i)}_{p} + \epsilon^{(i)}
        \end{aligned}$$

    - 보조회귀모형의 결정계수 $R^2$ 도출

        $$\begin{aligned}
        R^{2}
        &= 1 - \frac{RSS}{TSS}\\
        &= 1 - \frac{\sum_{i=1}^{n}{\epsilon_{i}^{2}}}{\sum_{i=1}^{n}{\left(\varepsilon_{i}^{2}-\overline{\varepsilon^{2}}\right)^{2}}}
        \end{aligned}$$

    - 검정통계량 도출

        $$
        BP = n \cdot R^2 \sim \chi^{2}(p)
        $$

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

### VIF

- **분산팽창계수(`V`ariance `I`nflation `F`actor; VIF)** : 변동성을 기준으로 다중공선성을 측정하는 지표로서, 통상 10을 초과하는 경우 다중공선성이 높다고 판단함

    $$\begin{aligned}
    VIF_k
    &= \frac{1}{1-R_{k}^{2}}
    \end{aligned}$$

    - $VIF_i$ : $i$ 번째 설명변수의 분산팽창계수
    - $R_i^2$ : $i$ 번째 설명변수에 대한 결정계수

- $R_k^2$

    - 다중선형회귀모형은 다음과 같이 정의됨

        $$\begin{aligned}
        y^{(i)}
        &= \hat{\beta}_{0} + \hat{\beta}_{1} \cdot x^{(i)}_{1} + \cdots + \hat{\beta}_{k} \cdot x^{(i)}_{p} + \varepsilon^{(i)}
        \end{aligned}$$

    - $k$ 번째 설명변수에 대한 보조회귀모형 도출

        $$\begin{aligned}
        x_{k}^{(i)}
        &= \gamma_{0} + \gamma_{1} \cdot x^{(i)}_{1} + \cdots + \gamma_{k-1} \cdot x^{(i)}_{k-1} + \gamma_{k+1} \cdot x^{(i)}_{k+1} + \cdots +\gamma_{p} \cdot x^{(i)}_{p} + \epsilon^{(i)}
        \end{aligned}$$

    - 보조회귀모형의 결정계수 $R_k^2$ 도출

        $$\begin{aligned}
        R_{k}^{2}
        &= 1 - \frac{RSS_k}{TSS_k}\\
        &= 1 - \frac{\sum_{i=1}^{n}{\epsilon_{i}^{2}}}{\sum_{i=1}^{n}{\left(x_{k}^{(i)}-\overline{x}_{k}\right)^{2}}}
        \end{aligned}$$
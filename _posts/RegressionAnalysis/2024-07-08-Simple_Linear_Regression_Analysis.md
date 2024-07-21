---
order: 1
title: Simple Linear Regression Analysis
date: 2024-07-08
categories: [Statistical Techs, Regression Analysis]
tags: [Statistics, Regression, t Test, Goodness of Fit Test, R2]
math: true
description: >-
  Based on the lecture "Statistical Models and Application (2024-1)" by Prof. Yeo Jin Chung, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
  path: /_post_refer_img/RegressionAnalysis/Thumbnail.jpg
---

## What? Linear Regression Analysis
-----

- **선형 회귀 분석(Linear Regression Analysis)** : 관찰된 연속형 변수들에 대하여 한 변수($Y$)를 다른 변수들($X$)의 선형 결합으로써 설명하는 모형을 탐색하는 방법
    - 광고지출비용이 증가할 때 매출액은 어떻게 변하는가?
    - 소득이 높은 국가의 국민들이 더 행복한가?
    - 소득이 증가할 때 소비는 얼마나 증가하는가?
    - 교육수준이 높을수록 임금이 증가하는가?

- **변수(Variable)**
    - **예측 대상이 되는 변수($Y$)**
        - 반응변수(Response Variable)
        - 종속변수(Dependent Variable)
        - 내생변수(Endogenous Variable)

    - **예측에 활용되는 변수($X$)**
        - 설명변수(Explanatory Variable)
        - 독립변수(Independent Variable)
        - 외생변수(Exogenous Variable)

### Simple Linear Regression Model

![01](/_post_refer_img/RegressionAnalysis/01-01.png){: width="100%"}

- **단순 선형 회귀 모형(Simple Linear Regression Model)** : 반응변수와 **단일 설명변수** 간 선형 상관관계를 모델링하는 모형

    $$\begin{aligned}
    Y
    &=\beta_0+\beta_1X+\varepsilon\\
    y_{i}
    &=\beta_0+\beta_1 x_{i}+\varepsilon_{i}
    \end{aligned}$$

- **회귀계수(Regression Coefficient)** : 모형이 추론하고자 하는 모수(Parameter)로서 상수
    - **편향(Bias; $\beta_0$)** : 설명변수의 값이 $0$ 일 때 종속변수의 값
    - **가중치(Weight; $\beta_1$)** : 설명변수가 종속변수에 미치는 영향력의 방향과 강도

- **오차항(Error Term; $\varepsilon$)** : 확률변수

    $$\begin{aligned}
    \varepsilon = y-\left(\beta_{0} + \beta_{1} x \right) \sim N(0, \sigma^2)
    \end{aligned}$$

    - **잔차(Residual; $\epsilon$)** : 최적 회귀계수 하 오차항의 추정치

        $$
        \epsilon=y-\left(\hat{\beta}_{0} + \hat{\beta}_{1} x \right)
        $$

## 회귀계수의 유의성 검정: T-검정
-----

> 반응변수와 설명변수가 **통계적으로 유의한(Statistically Significant)** 관계를 가지는가에 관한 가설검정임. 단, 검정 결과 두 변수 간 관계가 통계적으로 유의하다는 결론이 도출되더라도, 이 결론은 두 변수 간 상관관계(Correlation)의 유의성을 보장할 뿐, 두 변수 간 선형관계(Linear Relationship) 혹은 인과관계(Causation)의 유의성을 보장하지는 않음.

- **관심 모수에 대한 점 추정량 도출**
    - **관심 모수** : $\beta_{1}$
    - **최소자승추정량** : $$\hat{\beta}_{1} \sim N(\mathbb{E}\left[\hat{\beta}_{1}\right], \mathbb{SE}\left[\hat{\beta}_{1}\right]^2) \quad \text{s.t.}\;n>30$$
        
        $$\begin{aligned}
        \mathbb{E}\left[\hat{\beta}_{1}\right]
        &= \beta_{1}\\
        \mathbb{SE}\left[\hat{\beta}_{1}\right]^2
        &= \sigma^2\left[\displaystyle\frac{1}{\sum_{i=1}^{n}{(x_{i}-\overline{x})^2}}\right] \quad \text{s.t.}\;\varepsilon \sim N(0,\sigma^2)
        \end{aligned}$$

- **귀무가설과 대립가설 설정**
    - $H_{0}: \quad \beta_{1} = 0$
    - $H_{1}: \quad \beta_{1} \ne 0$

- **검정통계량 도출**

    $$\begin{aligned}
    T = \frac{\hat{\beta}_{1}-0}{\mathbb{SE}\left[\hat{\beta}_{1}\right]} \sim t(n-2)
    \end{aligned}$$

## Goodness of Fit
-----

- **적합도(Goodness of Fit)** : 모형이 반응변수의 변동을 얼마나 잘 설명하고 있는가

- **반응변수(Response Variable)**
    - $y_{i}=\beta_{0}+\beta_{1}x_{i}+\varepsilon_{i}$
    - $\hat{y}=\beta_{0}+\beta_{1}x$
    - $\overline{y}=\beta_{0}+\beta_{1}\overline{x} \quad \text{s.t.}\; \varepsilon \sim N(0, \sigma^2)$

### Variation of the Response Variable

$$\begin{aligned}
\sum_{i=1}^{n}{\left(y_{i}-\overline{y}\right)^2}
&= \sum_{i=1}^{n}{\left[\left(\hat{y}_{i} + \varepsilon_{i}\right) -\overline{y}\right]^{2}} \\
&= \sum_{i=1}^{n}{\left[\left(\hat{y}_{i} -\overline{y}\right) + \varepsilon_i \right]^{2}} \\
&= \sum_{i=1}^{n}{\left[\left(\hat{y}_{i} -\overline{y}\right)^2 + \varepsilon_{i}^{2} + 2 \times \varepsilon_{i} \times \left(\hat{y}_{i}-\overline{y}\right)\right]} \\
&= \sum_{i=1}^{n}{\left(\hat{y}_{i} -\overline{y}\right)^{2}} + \sum_{i=1}^{n}{\varepsilon_{i}^2} + 2\times\sum_{i=1}^{n}{\varepsilon_{i}\left(\hat{y}_{i}-\overline{y}\right)} \\
&= \sum_{i=1}^{n}{\left(\hat{y}_{i} -\overline{y}\right)^2} + \sum_{i=1}^{n}{\varepsilon_{i}^{2}}\quad(\because \sum_{i=1}^{n}{\hat{y}_{i}-\overline{y}} = 0)
\end{aligned}$$

- **총변동(Total Sum of Square; TSS)** : 반응변수의 총 변동성

    $$
    TSS=\sum_{i=1}^{n}{\left(y_{i}-\overline{y}\right)^2}
    $$

- **회귀변동(Explained Sum of Square; ESS)** : 모형에 의해 설명되는 반응변수의 변동성

    $$
    ESS=\sum_{i=1}^{n}{\left(\hat{y}_{i}-\overline{y}\right)^2}
    $$

- **잔차변동(Residual Sum of Square; RSS)** : 모형에 의해 설명되지 않는 반응변수의 변동성

    $$\begin{aligned}
    RSS
    &=\sum_{i=1}^{n}{\left(y_{i}-\hat{y}_{i}\right)^{2}}\\
    &=\sum_{i=1}^{n}{\varepsilon_{i}^{2}}
    \end{aligned}$$

### Coefficient of Determination

- **결정계수(Coefficient of Determination; $R^2$)** : 총변동 대비 회귀변동의 비율로 측정된 적합도

    $$\begin{aligned}
    R^2
    &= \frac{ESS}{TSS} \\
    &= \frac{ESS}{ESS + RSS} \\
    &= 1 - \frac{RSS}{TSS}
    \end{aligned}$$

- **Adjusted Coefficient of Determination($\text{Adj.}R^2$)** : 설명변수의 갯수 $p$ 가 많을수록 적합도가 높게 측정되는 경향을 조정한 결정계수

    $$
    \text{Adj.}R^2 = \frac{(n-1)R^2-p}{n-p-1}
    $$
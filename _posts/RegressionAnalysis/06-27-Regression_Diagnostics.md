---
order: 4
title: Regression Diagnostics
date: 2024-06-27
categories: [Statistical Techs, Regression Analysis]
tags: [Statistics, Regression]
math: true
description: >-
  Based on the lecture "Statistical Models and Application (2024-1)" by Prof. Yeo Jin Chung, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
  path: /_post_refer_img/RegressionAnalysis/Thumbnail.jpg
---

## 선형회귀모형의 고전적 가정

- `A.1` **반응변수와 설명변수의 선형성 가정**

    >The Linear Model is Correctly Specified.

- `A.2` **설명변수의 비확률성 가정 혹은 설명변수 간 통계적 독립성 가정**

    >$X_i$ is Non-Random For Every $i=1,\cdots,n$

- `A.3` **오차항의 기대값에 관한 가정**

    >$E(\varepsilon_i)=0$ For Every $i=1,\cdots,n$

- `A.4` **오차항의 등분산성(Homoskedasticity) 가정**

    >$Var(\varepsilon_i)=\sigma^2$ For Every $i=1,\cdots,n$

- `A.5` **관측치 간 오차항의 자기상관 없음(No Autocorrelation) 가정**

    >$Cov(\varepsilon_i, \varepsilon_j)=0$ If $i \ne j$

- `A.6` **오차의 정규성 가정(Normality Assumption)**
    - 최소자승추정량에 대하여 가설검정하기 위해서는 고전적 가정에 더하여 오차항의 분포에 관한 가정이 필요함

        >$\varepsilon_i$ is Normally Distributed For Every $i=1,\cdots,n$

    - 고전적 가정과 오차의 정규성 가정을 종합하면 다음이 성립함

        $$
        \varepsilon_{i^\forall} \sim N(0, \sigma^2)
        $$

</br>

## 반응변수와 설명변수 간 선형관계의 이해

- **가중치 $\beta_1$ 에 관한 최소자승추정량 $\hat{\beta_1}$ 은 다음과 같음**

    $$\begin{aligned}
    \hat{\beta_1}
    &= \displaystyle\frac{Cov(X,Y)}{Var(X)} \\
    &= \displaystyle\frac{\displaystyle\sum_{i=1}^{n}(X_i-\overline{X})(Y_i-\overline{Y})}{\displaystyle\sum_{i=1}^{n}(X_i-\overline{X})^2}
    \end{aligned}$$

- **분자를 다음과 같이 이해할 수 있음**

    $$\begin{aligned}
    \displaystyle\sum_{i=1}^{n}(X_i-\overline{X})(Y_i-\overline{Y})
    &= \displaystyle\sum_{i=1}^{n}(X_i-\overline{X})Y_i-\displaystyle\sum_{i=1}^{n}(X_i-\overline{X})\overline{Y} \\
    &= \displaystyle\sum_{i=1}^{n}(X_i-\overline{X})Y_i - \overline{Y} \times \displaystyle\sum_{i=1}^{n}(X_i-\overline{X}) \\
    &= \displaystyle\sum_{i=1}^{n}(X_i-\overline{X})Y_i\;(\because \displaystyle\sum_{i=1}^{n}(X_i-\overline{X}) = 0)
    \end{aligned}$$

- 즉, $\hat{\beta_1}$ 은 $Y_i$ 들의 **선형조합(Linear Combination)**

    $$\begin{aligned}
    \hat{\beta_1}
    &= \displaystyle\frac{\displaystyle\sum_{i=1}^{n}(X_i-\overline{X})Y_i}{\displaystyle\sum_{i=1}^{n}(X_i-\overline{X})^2} \\
    &= w_1Y_1 + w_2Y_2 + \cdots + w_nY_n \\
    \\
    (w_i
    &= \displaystyle\frac{(X_i-\overline{X})}{\displaystyle\sum_{j=1}^{n}(X_j-\overline{X})^2},\;i=1,2,\cdots,n)
    \end{aligned}$$

- **$\hat{\beta_1}$ 에 대하여 다음이 성립함** (증명 생략)
    - $\displaystyle\sum_{i=1}^{n}w_i=0$
    - $\displaystyle\sum_{i=1}^{n}w_iX_i=1$
    - $\displaystyle\sum_{i=1}^{n}w_i^2=\displaystyle\frac{1}{\displaystyle\sum_{i=1}^{n}(X_i-\overline{X})^2}$

- **따라서 최소자승추정량 $\hat{\beta_1}$ 과 그 모수 $\beta_1$ 사이에는 다음이 성립함**

    $$\begin{aligned}
    \hat{\beta_1}
    &= \displaystyle\sum_{i=1}^{n}w_iY_i \\
    &= \displaystyle\sum_{i=1}^{n}w_i(\beta_0+\beta_1X_i+\varepsilon_i) \\
    &= \beta_1 + \displaystyle\sum_{i=1}^{n}w_i\varepsilon_i
    \end{aligned}$$

- **최소자승추정량은 다음을 만족함**
    - $\overline{Y}=\hat{\beta_0}+\hat{\beta_1}\overline{X}$
    - $\overline{e}=\displaystyle\frac{1}{n}\displaystyle\sum_{i=1}^{n}e_i=0$
    - $\displaystyle\sum_{i=1}^{n}e_iX_i=0$
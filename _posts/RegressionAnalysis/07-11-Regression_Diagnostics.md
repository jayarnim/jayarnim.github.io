---
order: 4
title: Regression Diagnostics
date: 2024-07-11
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

## 선형성 가정과 비선형 문제

### 반응변수와 설명변수 간 선형관계의 이해

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

</br>

## 독립성 가정과 다중공선성 문제

### 💡 고전적 가정 `A.2` 의 수학적 이해

- **선형 결합(Linear Combination)** : 차원이 $n$ 으로 동일한 임의의 벡터와 스칼라에 대하여, 각 항에 스칼라를 곱하거나 상호 더함으로써 일련의 항으로 구성하는 작업

    $$
    \alpha_{1}\overrightarrow{a_{1}} + \alpha_{2}\overrightarrow{a_{2}} + \cdots + \alpha_{p}\overrightarrow{a_{p}}
    $$

- **선형 종속(Linearly Dependent)** : 어떤 벡터가 다른 벡터들의 선형 결합으로 표현 가능한 경우
        
    $$
    \alpha_{1}\overrightarrow{a_{1}} + \alpha_{2}\overrightarrow{a_{2}} + \cdots + \alpha_{p}\overrightarrow{a_{p}} = 0, \alpha^{\forall} \ne 0
    $$

- **선형 독립(Linearly Independent)** : 어떤 벡터가 다른 벡터들의 선형 결합으로 표현될 수 없는 경우

    $$
    \alpha_{1}\overrightarrow{a_{1}} + \alpha_{2}\overrightarrow{a_{2}} + \cdots + \alpha_{p}\overrightarrow{a_{p}} = 0 \Rightarrow \alpha^{\forall} = 0
    $$

- **고전적 가정 `A.2` 의 수학적 이해**

    $$\begin{aligned}
    X_i
    &\ne \lambda X_j \; (i \ne j, \lambda \ne 0)
    \end{aligned}$$

    - 설명변수벡터 $\overrightarrow{X_i}$ 가 $\overrightarrow{X_j}(i \ne j)$ 에 선형 종속이어서는 안 됨

### 다중공선성 문제

#### 💡 가중치 최소자승추정량의 이해

- **가중치 $\beta_i$**

    $$\begin{aligned}
    \beta_{i}
    &= \displaystyle\frac{\partial Y}{\partial X_i}
    \end{aligned}$$

    - $i$ 번째 설명변수 $X_i$ 의 가중치 $\beta_i$ 는 $X_i$ 가 반응변수 $Y$ 에 순수하게 미치는 영향력으로서, $X_{j^{\forall}} (j^{\forall} \ne i)$ 의 값이 일정할 때 $X_i$ 변동 시 $Y$ 의 변동 양상을 나타냄

- **가중치 $\beta_i$ 의 최소자승추정량**

    $$\begin{aligned}
    \hat{\beta}_{i}
    &= \displaystyle\frac{\sigma_{X_i,Y}}{\sigma_{X_i}^2}
    \end{aligned}$$

    - 고전적 가정 하 $X_i$ 의 가중치 $\beta_i$ 의 최소자승추정량은 $X_i$ 의 분산 대비 $X_i$ 와 $Y$ 의 공분산의 비율임

#### 💡 다중공선성

- **완전공선성(Perfect Multi-Col-Linearity)** : 고전적 가정 `A.2` 가 위배되는 상황

    $$\begin{aligned}
    X_i
    &= \lambda X_j \; (i \ne j, \lambda \ne 0)
    \end{aligned}$$

    - $X_j(j^{\forall} \ne i)$ 의 변동이 $X_i$ 의 변동에 영향을 미친다고 하자
    - $X_{i}$ 와 $Y$ 의 공분산 $\sigma_{X_{i},Y}$ 는 제3의 요인인 $X_{j}$ 의 변동에 영향을 받은 $X_{i}$ 의 변동에 의한 $Y$ 의 변동을 내포함
    - 즉, $X_i$ 와 $X_j$ 가 선형 독립이 아닐 경우, $X_i$ 의 가중치 $\hat{\beta}_i$ 가 $Y$ 에 대한 $X_i$ 의 순수한 설명력이라고 볼 수 없음

- **다중공선성(Multicollinearity)** : 설명변수 간 상관관계가 선형관계라고 확정할 수는 없으나, 선형관계에 가까운 형태를 보이는 경우

    $$
    \rho (X_i, X_j) \approx \pm 1
    $$

#### 💡 분산팽창계수

- **$Y$ 변동의 이해**

    - **총 변동(Sum of Squared Total; $SST$)**

        $$\begin{aligned}
        SST
        &= \displaystyle\sum_{i=1}^{n}(Y_i-\overline{Y})^2\\
        &= SSR+SSE
        \end{aligned}$$

    - **회귀변동(Sum of Squared Regression; $SSR$)** : $X_{\forall}$ 의 선형조합으로 설명 가능한 변동

        $$
        SSR=\displaystyle\sum_{i=1}^{n}(\hat{Y_i} -\overline{Y})^2
        $$

    - **오차변동(Sum of Squared Regression; $SSE$)** : $X_i$ 의 선형조합으로 설명할 수 없는 변동

        $$
        SSE=\displaystyle\sum_{i=1}^{n}e_i^2
        $$

- **결정계수(Coefficient of Determination; $R^2$)** : 총변동 대비 회귀변동

    $$\begin{aligned}
    R^2
    &= \displaystyle\frac{SSR}{SST} \\
    &= \displaystyle\frac{SSR}{SSR + SSE} \\
    &= 1 - \displaystyle\frac{SSE}{SST}
    \end{aligned}$$

- **분산팽창계수(Variance Inflation Factor; $VIF$)** : 변동을 기준으로 다중공선성을 계산하는 지표

    $$\begin{aligned}
    VIF_i
    &= \displaystyle\frac{1}{1-R_{i}^{2}}
    \end{aligned}$$
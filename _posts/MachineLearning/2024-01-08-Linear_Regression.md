---
order: 8
title: Linear Regression
date: 2024-01-08
categories: [Artificial Intelligence, Machine Learning]
tags: [writing]
math: true
image:
  path: /img/MachineLearning/Thumbnail.jpg
---

# 💡 What? Regression
-----

- **정의** : 반응변수와 그 설명변수 간 상관관계 추세를 요약하는 수렴 작업

- **설명변수의 개수에 따른 구분**
    - **단순 회귀 모형(Simple Regression Model)** : 반응변수에 대한 설명변수가 하나인 경우(이하는 선형모형을 가정)

        $$
        Y=\beta_0+\beta_1X+\varepsilon
        $$

    - **다중 회귀 모형(Multiple Regression Model)** : 반응변수에 대한 설명변수가 두 가지 이상인 경우(이하는 선형모형을 가정)

        $$
        Y=\beta_0+\beta_1 X_1+\beta_2 X_2+\cdots+\beta_k X_k+\varepsilon
        $$

- **선형 가정 여부에 따른 구분**
    - **선형 회귀 모형(Linear Regression Model)** : 설명변수와 반응변수 간 선형관계를 가정하는 경우
        - `sklearn.linear_model.LinearRegression`
        - `sklearn.linear_model.SGDRegressor`

    - **비선형 회귀 모형(Non-Linear Regression Model)** : 설명변수와 반응변수 간 선형관계를 가정하지 않는 경우
        - `sklearn.svm.SVR`
        - `sklearn.tree.DecisionTreeRegressor`

# 💡 Linear Regression
-----

### 단순 선형 회귀 모형

<p align="center"><img alt="reg" src="https://github.com/jayarnim/jayarnim/assets/116495744/08286995-d705-4e40-927b-4b96cbd202fb" width=80%></p>

- **단순 선형 회귀 모형의 이해**

    $$\begin{aligned}
    &Y=\beta_0+\beta_1X+\varepsilon\\
    &\Rightarrow y_i=\beta_0+\beta_1x_i+\varepsilon_i
    \end{aligned}$$

    - $\varepsilon$ : 잔차항(Residual)
        - $E[\varepsilon]=0$

    - $\beta_0$ : 편향(Bias)

    - $\beta_1$ : 가중치(Weight)

- **최소자승법에 기초한 회귀계수 최적값 도출**

    - **최소자승법(Least Square Method; OLS)** : 회귀계수 최적값을 **잔차항 $\varepsilon_{i}$ 자승의 합계를 최소화하는 값**으로 탐색하는 방법

        $$\begin{aligned}
        \hat{\beta_{0}},\hat{\beta_{1}}
        &= \argmin_{\beta_{0},\beta_{1}}{L_{OLS}}
        \end{aligned}$$
    
    - 최소자승법에 기초한 손실 함수 $L_{OLS}$

        $$\begin{aligned}
        L_{OLS}
        &= \sum_{i=1}^{n}{\varepsilon_{i}^2}\\
        \varepsilon_{i}
        &= y_{i}-\hat{y}_{i}\\
        &= y_{i}-(\beta_{0}+\beta_{1}\hat{x}_{i})
        \end{aligned}$$

    - 최소자승법에 기초한 회귀계수 $\beta_{0}$ 의 최적값 $\hat{\beta_{0}}$

        $$\begin{aligned}
        \hat{\beta_{0}}
        &= \overline{y}-\beta_{1}\overline{x}
        \end{aligned}$$

    - 최소자승법에 기초한 회귀계수 $\beta_{1}$ 의 최적값 $\hat{\beta_{1}}$

        $$\begin{aligned}
        \hat{\beta_{1}}
        &= \frac{\sum_{i=1}^{n}{(x_{i}-\overline{x})(y_{i}-\overline{y})}}{\sum_{i=1}^{n}{(x_{i}-\overline{x})^{2}}}\\
        &=\frac{\sigma_{xy}}{\sigma_{x}^{2}}
        \end{aligned}$$

### 다중 선형 회귀 모형

<p align="center"><img alt="multireg" src="https://github.com/jayarnim/jayarnim/assets/116495744/3c75c602-e85c-42aa-8050-ed054dec289f" width=80%></p>

- 관측치 $i$ 에 대한 다중 선형 회귀 모형이 다음과 같다고 하자

    $$
    y_{i}=\beta_{0}+\beta_{1}x_{i,1}+\beta_{2}x_{i,2}+\cdots+\beta_{d}x_{i,d}
    $$

    - $i\in\{1,2,\cdots,n\}$ : 관측치 번호
    - $k\in\{1,2,\cdots,d\}$ : 설명변수 번호

- $n$ 개의 관측치가 존재한다고 했을 때 위 모형을 선형대수로 표현할 수 있음

    $$
    \hat{\overrightarrow{y}} = \hat{\mathbf{X}}\overrightarrow{\beta}
    $$

- 최소자승법에 기초하여 도출한 가중치 벡터를 **정규방정식(Normal Equation)**이라고 정의함

    $$\begin{aligned}
    \hat{\overrightarrow{\beta}}
    &= \argmin_{\overrightarrow{\beta}}{L_{OLS}}\\
    &= (\mathbf{X}^{T}\mathbf{X})^{-1}\mathbf{X}^{T}\overrightarrow{y}
    \end{aligned}$$

# 💡 [sklearn.linear_model.LinearRegression](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html)
-----

```python
from sklearn.linear_model import LinearRegression
```

### General HyperParameter

- `n_jobs(default : None)` : 병렬로 작업할 코어 갯수

### Model HyperParameter

- `fit_intercept(default : True)` : 상수항 $\beta_0$ 설정 여부

### Attribute

- `n_features_in_` : 설명변수 갯수
- `feature_names_in_` : 설명변수 이름
- `coef_` : 설명변수별 가중치
- `intercept_` : 편향

-----

#### 이미지 출처

- https://medium.com/analytics-vidhya/multiple-linear-regression-an-intuitive-approach-f874f7a6a7f9
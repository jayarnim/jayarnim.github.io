---
order: 9
title: Gradient Descent
date: 2024-01-09
categories: [Artificial Intelligence, Machine Learning]
tags: [writing]
math: true
image:
  path: /img/MachineLearning/Thumbnail.jpg
---

# 💡 What? Gradient
-----

- **정의** : 다변수 함수에 대하여 모든 방향으로의 순간변화율 벡터

    <p align="center"><img alt="g" src="https://github.com/jayarnim/jayarnim/assets/116495744/51963f6a-3135-45b2-a61e-8f11ed724300" width=80%></p>

    $$\begin{aligned}
    \nabla{f(x_{1},x_{2},\cdots,x_{n})}
    &= \begin{pmatrix}
    \displaystyle\frac{\partial f(x^{\forall})}{\partial x_{1}}\\
    \displaystyle\frac{\partial f(x^{\forall})}{\partial x_{2}}\\
    \vdots\\
    \displaystyle\frac{\partial f(x^{\forall})}{\partial x_{n}}\\
    \end{pmatrix}
    \end{aligned}$$

# 💡 What? Gradient Descent
-----

### Gradient Descent

- **정의** : 회귀계수 최적값을 탐색함에 있어 손실 함수의 그라디언트를 활용하는 방법

    <p align="center"><a href="#"><img alt="gd" src="https://github.com/jayarnim/jayarnim/assets/116495744/7659ff42-651c-49ab-9d56-b69db4454af6" width=80%></a></p>

- **절차**

    1. 회귀계수 벡터 $\overrightarrow{w}$ 의 초기 아규먼트 설정
    2. 현재 아규먼트 $\overrightarrow{w}_{prev}$ 에서 손실 함수의 그라디언트 $\nabla{L_{OLS}(\overrightarrow{w}_{prev})}$ 계산
    3. 현재의 아규먼트에서 음의 방향으로 $\alpha \times \nabla{L_{OLS}(\overrightarrow{w}_{prev})}$ 만큼 이동하여 새로운 아규먼트 $\overrightarrow{w}_{new}$ 적용
    4. ②, ③을 반복하여 손실 함수를 최소화하는 지점 탐색

### 회귀계수 갱신 규칙

$$\begin{aligned}
\overrightarrow{w}_{new}
&= \overrightarrow{w}_{prev} - \alpha \times \nabla{L_{OLS}(\overrightarrow{w}_{prev})}
\end{aligned}$$

- $\overrightarrow{w}_{prev}$ : 현재 회귀계수 아규먼트
- $\overrightarrow{w}_{new}$ : 새로운 회귀계수 아규먼트
- $\alpha$ : 학습률
- $\nabla{L_{OLS}(\overrightarrow{w}_{prev})}$ : 최소자승법에 기초하여 도출한 손실 함수의 그라디언트

### Learning Rate

- **정의** : 손실 함수에 대하여 그 극소점을 탐색하기 위한 회귀계수 갱신 보폭

- **학습률이 낮을수록 과대적합될 가능성이 높음**

    <p align="center"><a href="#"><img alt="학습률이 낮을 때" src="https://github.com/jayarnim/jayarnim/assets/116495744/24dc38b6-16d6-400b-bdaa-5ba9fcf9c286" width=80%></a></p>

- **학습률이 높을수록 과소적합될 가능성이 높음**

    <p align="center"><a href="#"><img alt="학습률이 높을 때" src="https://github.com/jayarnim/jayarnim/assets/116495744/406ebc5a-7555-4bce-ba95-52703e10e0fc" width=80%></a></p>

# 💡 [`sklearn.linear_model.SGDRegressor`](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.SGDRegressor.html#sklearn-linear-model-sgdregressor)
-----

```python
from sklearn.linear_model import SGDRegressor
```

### General HyperParameter

- `random_state(default : None)`

### Model HyperParameter

- `eta0(default : 0.1)` : 학습률

- `loss(default : 'squared_error')` : 손실 함수
    - `'squared_error'`
    - `'huber'`
    - `'epsilon_insensitive'`
    - `'squared_epsilon_insensitive'`

- `fit_intercept(default : True)` : 상수항 $\beta_0$ 설정 여부

### To Prevent OverFitting

#### About Iteration

- `max_iter` : 최적 회귀계수 탐색 최대 횟수

#### About Early Stopping

- `early_stopping(default : False)` : 학습 조기 중단 여부
- `n_iter_no_change(default : 5)` : 손실이 몇 회 이상 개선되지 않을 경우 중단할 것인가
- `tol(default : 0.001)` : 허용 오차

#### About Penalty

- `penalty(default : None)` : 가중치 규제 방법
    - `'l1'` : LASSO
    - `'l2'` : Ridge
    - `'elasticnet'` : `l1`, `l2` 혼합

- `alpha(default : 0.0001)` : 가중치 규제 시 규제 강도

- `l1_ratio(default : 0.15)` : `elasticnet` 설정 시 전체 규제 강도 대비 `l1` 규제 비중

### Attribute

- `n_features_in_` : 설명변수 갯수
- `feature_names_in_` : 설명변수 이름
- `coef_` : 설명변수별 가중치
- `intercept_` : 편향

-----

#### 이미지 출처

- https://towardsdatascience.com/an-intuitive-explanation-of-gradient-descent-83adf68c9c33
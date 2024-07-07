---
order: 11
title: Logistic Regression
date: 2024-01-11
categories: [Artificial Intelligence, Machine Learning]
tags: [writing]
math: true
image:
  path: /img/MachineLearning/Thumbnail.jpg
---

# 💡 What? Logistic Regression
-----

### Logistic Regression

- **정의** : 회귀 기법을 판별분석에 활용하는 비선형 함수 알고리즘

    <p align="center"><img src="https://user-images.githubusercontent.com/116495744/221402155-596e45c2-5d0d-40a6-ae23-9589b48f807c.png" width=80%></p>

    $$
    P(c=1)
    = \frac{1}{1+\exp[-(\beta_{0}+\beta_{1}x_{1}+\cdots+\beta_{d}x_{d})]}
    $$

### Logistic Function

- **설명변수와 반응변수 가정**

    - 어떠한 관측치 벡터 $\overrightarrow{x}$ 가 다음과 같이 주어졌다고 하자

        $$\begin{aligned}
        f(\overrightarrow{x})
        &=\beta_{0}+\beta_{1}x_{1}+\cdots+\beta_{d}x_{d} \in (-\infty,\infty)
        \end{aligned}$$

    - $\overrightarrow{x}$ 의 반응변수 $y$ 는 다음과 같음

        $$\begin{aligned}
        y
        &=c \in \{0,1\}
        \end{aligned}$$

    - $y$ 와 $\overrightarrow{x}$ 간에는 공역이 일치하지 않으므로 등식이 성립하지 않음

        $$
        y \ne \beta_{0}+\beta_{1}x_{1}+\cdots+\beta_{d}x_{d}
        $$

- **반응변수 재정의** : 범주 $1$ 에 속할 확률

    $$\begin{aligned}
    y
    &= P(c=1) \in [0,1]
    \end{aligned}$$

- **공역 조정을 통한 연결함수 $f(x)$ 도출**

    - **승산(Odds)** : 범주 $1$ 에 속하지 않을 확률 대비 속할 확률

        $$\begin{aligned}
        f(x)
        &= \text{odds}\\
        &= \frac{P(c=1)}{1-P(c=1)} \in [0, \infty)
        \end{aligned}$$

    - **로짓(Logit)** : 승산에 자연로그를 취한 값

        $$\begin{aligned}
        f(x)
        &= \text{logit}\\
        &= \ln{\frac{P(c=1)}{1-P(c=1)}} \in (-\infty, \infty)
        \end{aligned}$$

    - **로짓 함수와 $\overrightarrow{x}$ 연결**

        $$\begin{aligned}
        \text{logit}
        &= f(x)\\
        &= \beta_{0}+\beta_{1}x_{1}+\cdots+\beta_{d}x_{d}
        \end{aligned}$$

- **연결함수를 활용하여 재정의된 반응변수와 설명변수 연결**

    $$\begin{aligned}
    \ln{\frac{P(c=1)}{1-P(c=1)}}
    &= f(x)\\
    &= \beta_{0}+\beta_{1}x_{1}+\cdots+\beta_{d}x_{d}\\\\

    \frac{P(c=1)}{1-P(c=1)}
    &= e^{f(x)}\\
    &= \exp[\beta_{0}+\beta_{1}x_{1}+\cdots+\beta_{d}x_{d}]\\\\

    \therefore
    y
    &= P(c=1)\\
    &= \frac{1}{1+\exp[-(\beta_{0}+\beta_{1}x_{1}+\cdots+\beta_{d}x_{d})]}
    \end{aligned}$$

# 💡 [`sklearn.linear_model.LogisticRegression`](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LogisticRegression.html#sklearn-linear-model-logisticregression)
-----

```python
from sklearn.linear_model import LogisticRegression
```

### 💡 General HyperParameter

- `random_state(default : None)`
- `warm_start(default : False)` : 동작 메시지 출력 여부 설정
- `n_jobs(default : None)` : 병렬로 작업할 코어 갯수

### 💡 Model HyperParameter

- `solver(default : 'lbfgs')` : 회귀식 종류로서 그 아규먼트에 따라 `penalty` 의 아규먼트가 한정됨
    - `'lbfgs'` : `l2` or `None`
    - `'liblinear'` : `l1` or `l2`
    - `'newton-cg'` : `l2` or `None`
    - `'newton-cholesky'` : `l2` or `None`
    - `'sag'` : `l2` or `None`
    - `'saga'` : `elasticnet`, `l1`, `l2` or `None`

- `fit_intercept(default : True)` : 상수항 $\beta_0$ 설정 여부

- `multi_class(default : 'auto')` : 다항 분류 시 분류 규칙 설정
    - `'auto'` : 이항 분류 혹은 `solver` 아규먼트가 `'liblinear'` 인 경우 `'ovr'`, 그외에는 `'multinomial'` 을 선택함
    - `'ovr'` : One VS Rest
    - `'multinomial'` : `solver` 아규먼트가 `'liblinear'` 인 경우 적용 불가

### 💡 To Prevent OverFitting

#### About Iteration

- `max_iter(default : 100)` : 최적 회귀계수 탐색 최대 횟수

#### About Early Stopping

- `tol(default : 0.0001)` : 허용 오차

#### About Penalty

- `penalty(default : l2)` : 가중치 규제 방법
    - `None`
    - `'l1'` : LASSO
    - `'l2'` : Ridge
    - `'elasticnet'` : `l1`, `l2` 혼합

- `C(default : 1.0)` : 가중치 규제 시 규제 강도

- `l1_ratio(default : None)` : `elasticnet` 설정 시 전체 규제 강도 대비 `l1` 규제 비중

### 💡 To Prevent Underfitting

- `class_weight(default : None)` : 가중할 범주와 그 값

    - `'balanced'`
    - `dictionary type`
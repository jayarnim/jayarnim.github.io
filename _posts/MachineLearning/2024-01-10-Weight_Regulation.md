---
order: 10
title: Weight Regulation
date: 2024-01-10
categories: [Artificial Intelligence, Machine Learning]
tags: [writing]
math: true
image:
  path: /img/MachineLearning/Thumbnail.jpg
---

# 💡 Weight Regulation
-----

- **p-norm** : $n$ 차원 벡터 $\overrightarrow{x}=\begin{pmatrix}x_{1}&x_{2}&\cdots&x_{n}\end{pmatrix}$ 의 크기를 정의하는 방법

    <p align="center"><img alt="p" src="https://github.com/jayarnim/jayarnim/assets/116495744/cfb01e04-13e7-4159-8b75-1c9201e2ca57" width=80%></p>

    $$
    ||x||_{p}=(|x_{1}|^{p}+|x_{2}|^{p}+\cdots+|x_{n}|^{p})^{\frac{1}{p}}
    $$

- **가중치 규제(Weight Regulation)** : 회귀계수 최적값을 탐색함에 있어 회귀계수 벡터 $\overrightarrow{\beta}$ 의 크기에 제약을 두는 것

    <p align="center"><img alt="가중치규제" src="https://github.com/jayarnim/jayarnim/assets/116495744/49f73e40-78f6-41ce-b04c-0bfc0c54f545" width=80%></p>

    $$\begin{aligned}
    \overrightarrow{\hat{\beta}}
    &= \argmin_{\overrightarrow{\beta}}{\left[L_{OLS}+\lambda||\beta||_{p}^{2}\right]}
    \end{aligned}$$

    - $L_{OLS}(\overrightarrow{\beta})$ : 최소자승법에 기초한 손실 함수

    - $\overrightarrow{\beta}$ : 회귀계수 벡터

    - $\lambda$ : 회귀계수 벡터 $\overrightarrow{\beta}$ 크기 제약 강도

    - `p` : 벡터 크기 정의 방법
        - `p=1` : LASSO
        - `p=2` : Ridge

# 💡 [`sklearn.linear_model.Lasso`](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.Lasso.html#sklearn.linear_model.Lasso)
# 💡 [`sklearn.linear_model.Ridge`](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.Ridge.html#sklearn.linear_model.Ridge)
-----

```python
from sklearn.linear_model import Lasso, Ridge
```

### General HyperParameter

- `random_state(default : None)`

### Model HyperParameter

- `alpha(default : 1.0)` : 규제 강도
- `fit_intercept(default : True)` : 상수항 $\beta_0$ 설정 여부

### To Prevent OverFitting

- `max_iter(default : 1000)` : 최적 회귀계수 탐색 최대 횟수

### Attribute

- `n_features_in_` : 설명변수 갯수
- `feature_names_in_` : 설명변수 이름
- `coef_` : 설명변수별 가중치
- `intercept_` : 편향

-----

#### 이미지 출처

- https://ekamperi.github.io/machine%20learning/2019/10/19/norms-in-machine-learning.html
- https://observablehq.com/@petulla/l1-l2l_1-l_2l1-l2-norm-geometric-interpretation 
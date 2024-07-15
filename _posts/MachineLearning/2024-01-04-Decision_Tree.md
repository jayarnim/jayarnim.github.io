---
order: 4
title: Decision Tree
date: 2024-01-04
categories: [Machine Learning Techs, Machine Learning]
tags: [Machine Learning, Supervised Learning, Classification]
math: true
description: >-
  Based on the lecture “Intro. to Machine Learning (2023-2)” by Prof. Je Hyuk Lee, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
  path: /_post_refer_img/MachineLearning/Thumbnail.jpg
---

## Decision Tree
-----

- **정의** : **순도(Uniformity)**를 최대로 가져가는 이진 판별 규칙들로 구성된 **수형도(Tree)**를 세우고 관측치를 분류하는 알고리즘

    ![01](/_post_refer_img/MachineLearning/04-01.png){: width="100%"}

- **구조**

    ![02](/_post_refer_img/MachineLearning/04-02.png){: width="100%"}

    - **루트 노드(Root Node)** : 깊이가 0인 꼭대기 노드로서 최상위 노드
    - **결정 노드(Decision Node)** : 규칙 조건
    - **리프 노드(Leaf Node)** : 하위 노드가 존재하지 않는 노드로서 최종 범주
    - **서브트리(Subtree)** : 어떠한 규칙 노드를 루트 노드로 가지는 하위 트리로서 판별 규칙 집합의 부분집합

## 재귀적 분기(Recursive Partitioning)
-----

- **정의** : **판별 규칙을 기준으로** 상위 노드를 분할하여 **순도가 높은** 하위 노드를 생성하는 반복적인 과정

    - **판별 규칙** : 어떤 분기에서 **하나의 설명변수를 사용하여** 생성한 분할 조건

        ![03](/_post_refer_img/MachineLearning/04-03.png){: width="100%"}

    - **순도(Purity)** : 어떤 노드에 속한 관측치들이 동일한 범주에 속하는 정도

        ![04](/_post_refer_img/MachineLearning/04-04.jpeg){: width="100%"}

        - 순도를 정확히 측정하기 어려우므로 그 대리변수로서 불순도(Impurity)를 사용함

### 판별 규칙

- 어떤 노드에 대하여, 설명변수 $X_{i} \ge x_{i}$ 를 기준으로 해당 노드를 분할한다고 하자

    $$
    y=\begin{cases}
    \begin{aligned}
    N_{left},\;&if\;X_{i} \ge x_{i}\\
    N_{right},\;&if\;X_{i} < x_{i}\\
    \end{aligned}
    \end{cases}
    $$

- 판별 규칙 $X_{i} \ge x_{i}$ 의 비용 $J(X_{i} \ge x_{i})$ 는 다음과 같음

    $$\begin{aligned}
    J(X_{i} \ge x_{i})
    &= \frac{m_{left}}{m}I_{left} + \frac{m_{right}}{m}I_{right}
    \end{aligned}$$

    - $m$ : 결정 노드에 속한 관측치 갯수
    - $m_{left}$ : 좌측 하위 노드로 분기한 관측치 갯수
    - $I_{left}$ : 좌측 하위 노드의 불순도
    - $m_{right}$ : 우측 하위 노드로 분기한 관측치 갯수
    - $I_{right}$ : 우측 하위 노드의 불순도

- 설명변수 $X_{i}$ 기준 분할 시 최적의 분기점 $\hat{x}_{i}$ 는 다음과 같음

    $$
    \hat{x}_{i}
    =\text{arg} \min_{x_{i}}{J(X_{i} \ge x_{i})}
    $$

- 특정 노드를 분할하는 최적의 설명변수 $\hat{X}_{i}$ 는 다음과 같음

    $$
    \hat{X}_{i}
    = \text{arg} \min_{X_{i}}{\left\{\min{J(X_{1})},\min{J(X_{2})},\cdots,\min{J(X_{n})}\right\}}
    $$

### 불순도

- **지니 지수(Gini Index)** : 불순도를 **경제적 불평등 개념**에 기초하여 계산한 지표

    $$\begin{aligned}
    I(N_{k})
    &= 1-\sum_{i=1}^{c}{p_{i}^2}
    \end{aligned}$$

    - $c$ : 범주 갯수
    - $p_{i}$ : 노드 $N_{k}$ 에서 $i$ 번째 범주에 속하는 관측치 비율

- **엔트로피 지수(Entropy Index)** : 불순도를 **정보 획득의 불확실성 개념**에 기초하여 계산한 지표

    $$\begin{aligned}
    I(N_{k})
    &= -\sum_{i=1}^{c}{\left[p_{i} \cdot \log_{2}{p_{i}}\right]}
    \end{aligned}$$

    - $c$ : 범주 갯수
    - $p_{i}$ : 노드 $N_{k}$ 에서 $i$ 번째 범주에 속하는 관측치 비율

## 가지치기(Pruning)
-----

![05](/_post_refer_img/MachineLearning/04-05.png){: width="100%"}

- **정의** : 자세하게 구분된 영역을 통합함으로써 과적합을 방지하는 기법

- **절차**
    1. Full Tree 생성
    2. 모든 노드에 대하여 비용 복잡도 지수 계산
    3. 비용 복잡도 지수가 가장 낮은 노드에 대하여 가지치기 수행
    4. 2~3 단계를 반복하며 최적의 $\alpha$ 탐색
    5. 최적의 $\alpha$ 하 Tree 도출

- **비용 복잡도 지수(Cost-Complexity)**

    $$\begin{aligned}
    R_{\alpha}(T)
    &= L(T) + \alpha \cdot |\text{leaf}(T)|\\

    L(T)
    &= \sum_{m=1}^{|\text{leaf}(T)|}{\sum_{\overrightarrow{x}_{i} \in R_{m}}{(y_{i}-\hat{y}_{i})^2}}
    \end{aligned}$$

    - $T$ : 타깃 노드를 루트 노드로 하는 서브트리
    - $\text{leaf}(T)$ : $T$ 의 리프 노드 집합
    - $R_{m} \in \text{leaf}(T)$ : $T$ 의 $m$ 번째 리프 노드
    - $$\overrightarrow{x}_{i} \in R_{m}$$ : $$R_{m}$$ 에 속한 $$i$$ 번째 관측치 벡터
    - $y_{i}$ : $\overrightarrow{x}_{i}$ 의 실제값
    - $$\hat{y}_{i}$$ : $$\overrightarrow{x}_{i}$$ 의 예측값
    - $\alpha$ : 가지치기 강도
    - $L(T)$ : $T$ 의 훈련 관측치에 대한 예측 손실
    - $R_{\alpha}(T)$ : 타깃 노드의 비용 복잡도 지수

## DTR
-----

![06](/_post_refer_img/MachineLearning/04-06.png){: width="100%"}

- **재귀적 분기**

    $$\begin{aligned}
    \hat{X}_{i}
    &= \text{arg} \min_{X_{i}}{\{J(X_{1},\hat{x}_{1}),J(X_{2},\hat{x}_{2}),\cdots,J(X_{n},\hat{x}_{n})\}}\\
    \hat{x}_{i}
    &= \text{arg} \min_{x_{i}}{J(X_{i},x_{i})}\\
    J(X_{i},x_{i})
    &= \frac{m_{left}}{m}L_{left}+\frac{m_{right}}{m}L_{right}
    \end{aligned}$$

- **차이점** : 손실 함수

    ![07](/_post_refer_img/MachineLearning/04-07.png){: width="100%"}

    - **판별 분석** : 불순도(Impurity)를 최소화하도록 분기

        $$\begin{aligned}
        L_{gini}(N_{k})
        &= 1-\sum_{i=1}^{c}{p_{i}^2}
        \end{aligned}$$

    - **회귀 분석** : 오차(Error)를 최소화하도록 분기

        $$\begin{aligned}
        L_{MSE}(N_{k})
        &= \sum_{i=1}^{m}{(y_{i}-\hat{y}_{i})^2}
        \end{aligned}$$

## [sklearn.tree.DecisionTreeClassifier](https://scikit-learn.org/stable/modules/generated/sklearn.tree.DecisionTreeClassifier.html#sklearn.tree.DecisionTreeClassifier)
-----

```python
from sklearn.tree import DecisionTreeClassifier
```

### General HyperParameter

- `random_state(default : None)`

### Model HyperParameter

- `max_features(default : None)` : 규칙 설계 시 고려할 설명변수 갯수
    - `'sqrt'` : $\sqrt{n}$
    - `'log2'` : $\log_2{n}$
    - `None` : $n$

### Recursive Partitioning

- `criterion(default : 'gini')` : 균일도 측정 방법
    - `'gini'` : 지니지수
    - `'entropy'` : 엔트로피지수

### Pruning

- `ccp_alpha(default : 0)`

### To Prevent Overfitting

- `max_depth(default : None)` : 트리 최대 깊이
- `max_leaf_nodes(default : None)` : 리프 노드의 최대 갯수
- `min_samples_split(default : 2)` : 하위 노드로 가지를 뻗기 위해 필요한 최소한의 관측치 갯수
- `min_impurity_decrease(default : 0)` : 하위 노드로 가지를 뻗기 위해 필요한 최소한의 불순도 개선 정도
- `min_samples_leaf(default : 1)` : 리프 노드의 관측치 최소 갯수

### To Prevent Underfitting

- `class_weight(default : None)` : 가중할 범주와 그 값
    - `'balanced'`
    - `dictionary type`
---
order: 2
title: Consumer Theory (1) Utility Maximization under Budget Constraint
date: 2019-07-16
categories: [ECONOMICS, 2.microeconomics]
tags: [Economics, Microeconomics, Optimization, Consumer Theory]
math: true
description: >-
    Based on the lecture "Microeconomics (2017-1)" by Prof. Jin Woo Park, Dept. of Economics, College of Economics & Commerce, Kookmin Univ.
image:
    path: /_post_refer_img/Economics/2.Microeconomics/Thumbnail.jpg
---

## Utility
-----

### Preference System

- **선호체계(Preference System)** : 상품묶음 간 선호관계를 평가하는 주관적 척도
    - **상품묶음(Commodity Bundle)** : 개별소비자가 선택 가능한 여러 상품에 대하여 각 품목의 수량 조합

        $$
        (X,Y)=(x,y)
        $$

    - **선호관계(Preference Relation)** : 임의의 상품묶음과 다른 상품묶음 간 선호의 우열관계

        $$
        (x,y) \succ (x', y')
        $$

- **선호체계의 공리**
    1. **완비성(Completeness)**; 동일한 품목의 수량을 나타내는 상품묶음 사이의 선호관계를 비교할 수 있다.

        $$
        A \succ B \; \text{or} \; B \succ A \; \text{or} \; A \sim B \quad \text{for}\;(A, B)^{\forall} \in X
        $$

    2. **이행성(Transitivity)**; 동일한 품목의 수량을 나타내는 상품묶음 A, B, C에 대하여 A보다 B를 선호하고, B보다 C를 선호하면 A보다 C를 선호한다.

        $$
        A \succ B \; \text{and} \; B \succ C \implies A \succ C \quad \text{for}\; (A, B, C)^{\forall} \in X
        $$

    3. **강단조성(Strong Monotonicity)**; 상품묶음이 나타내는 두 가지 재화 중에서 임의의 재화에 대하여 다른 재화의 수량이 일정하다면 해당 상품의 수량이 더 높은 상품묶음을 선호한다.

        $$
        x_i \ge y_i \; \text{for all} \; i \; \text{and} \; x_i > y_i \; \text{for some} \; i \implies A \succ B \quad \text{for} \; (A, B)^{\forall} \in X
        $$

    4. **연속성(Continuity)**; 두 상품묶음에 대한 선호도의 차이는 두 상품묶음이 나타내는 수량의 차이에 비례한다.

        $$
        A \succ B \; \text{and} \; C \approx A \implies C \succ B \quad \text{for}\;(A, B, C)^{\forall} \in X
        $$

    5. **볼록성(Convexity)**; 극단적인 수량의 조합을 나타내는 상품묶음보다는 두 가지 재화의 수량이 고루 섞여 있는 상품묶음을 선호한다.

        $$\begin{aligned}
        \lambda A + (1 - \lambda)B \succ A \quad \text{for} \quad
        &\lambda^{\forall} \in (0, 1)\\
        &(A, B)^{\forall} \in X
        \end{aligned}$$

### Utility

- **효용함수(Utility Function)** : 상품묶음과 선호도 값 사이의 상관관계를 나타내는 함수

    $$\begin{aligned}
    U^{(1)}:& \quad U(A)=10, U(B)=20, U(C)=30\\
    U^{(2)}:& \quad U(A)=40, U(B)=60, U(C)=80
    \end{aligned}$$

    > $U^{(1)}$ 과 $U^{(2)}$ 는 재화에 대하여 선호도 값을 다르게 매겼으나, 선호관계를 동일하게 평가하였음. 따라서 두 효용함수는 실질적으로는 무차별함. 이처럼 효용함수는 선호도 값의 기수성이 아니라 서수성이 중요함.

- **무차별곡선(Indifference curve)** : 재화 $X,Y$ 에 대하여, 동일한(무차별한) 효용 수준을 누릴 수 있는 상품묶음 $(X, Y)$ 의 집합

    ![01](/_post_refer_img/Economics/2.Microeconomics/02-01.png){: width="100%"}

    $$
    U(x,y)=u_{i}
    $$

    1. **완비성(Completeness)**; 동일한 효용함수의 상이한 효용수준을 나타내는 두 개의 무차별곡선은 교차하지 않는다.
    2. **이행성(Transitivity)**; 무차별곡선은 원점에서 멀수록 더 높은 효용수준을 나타낸다.
    3. **강단조성(Strong Monotonicity)**; 무차별곡선은 우하향한다.
    4. **연속성(Continuity)**; 제1사분면 위에 존재하는 임의의 점에 대하여 그 점을 지나는 무차별곡선이 하나 존재한다.
    5. **볼록성(Convexity)**; 무차별곡선은 원점에 대하여 볼록한 모양을 가진다.

### Subjective Rate of Substitution

- **한계효용(Marginal Utility; MU)** : 임의의 재화를 한 단위 추가 소비함으로써 추가로 누릴 수 있는 효용 수준

    $$
    MU_{X}:= \frac{\partial U}{\partial X}
    $$

- **한계대체율(Marginal Rate of Substitution; MRS)** : 재화 $X,Y$ 에 대하여, 동일한 효용 수준에서 해당 재화를 한 단위 추가 소비하기 위해 포기해야 하는 관련재 소비분

    $$
    \Delta X \cdot MU_{X} + \Delta Y \cdot MU_{Y} = 0
    $$

    $$
    \therefore MRS_{X,Y}:= -\frac{\Delta Y}{\Delta X} = \frac{MU_{X}}{MU_{Y}}
    $$

- **한계대체율 체감의 법칙** : 임의의 상품에 대하여, 해당 상품의 보유량이 증가할수록 동일한 효용수준에서 해당 상품을 한 단위 추가 소비하기 위해 포기해야 하는 관련재 소비분이 감소하는 현상

    $$
    \frac{\partial MRS_{X,Y}}{\partial X} \prec 0
    $$

## Budget Constraint
-----

![02](/_post_refer_img/Economics/2.Microeconomics/02-02.png){: width="100%"}

- **예산선(Budget Line)** : 주어진 예산($M$)과 가격 상황($P_{X}, P_{Y}$)에 맞게 취득할 수 있는 상품묶음들의 집합

    $$\begin{aligned}
    (x,y) \quad \text{s.t.}\; x \cdot P_{X} + y \cdot P_{Y} \le M
    \end{aligned}$$

- **상대가격(Relative Price)** : 재화 $X,Y$ 에 대하여, 동일한 예산 수준에서 특정 재화를 한 단위 추가 소비하기 위해 포기해야 하는 관련재 소비분

    $$
    \Delta X \cdot P_{X} + \Delta Y \cdot P_{Y} = 0
    $$
    
    $$
    \therefore - \frac{\Delta Y}{\Delta X} = \frac{P_{X}}{P_{Y}}
    $$

## Utility Maximization under Budget Constraint
-----

![03](/_post_refer_img/Economics/2.Microeconomics/02-03.png){: width="100%"}

$$
\max{U(x,y)} \quad \text{s.t.} \; x \cdot P_{X} + y \cdot P_{Y} \le M
$$

- **무차별곡선의 접선의 기울기** : X재의 Y재에 대한 주관적 교환비율로서 한계대체율

    $$
    -\frac{\Delta Y}{\Delta X}=\frac{MU_{X}}{MU_{Y}}
    $$

- **예산선의 기울기** : X재의 Y재에 대한 객관적 교환비율로서 상대가격

    $$
    -\frac{\Delta Y}{\Delta X}=\frac{P_{X}}{P_{Y}}
    $$

- **예산선과 무차별곡선의 접점** : 예산 제약 하 효용을 극대화하는 상품묶음

    $$\begin{aligned}
    \frac{MU_{X}}{MU_{Y}}=-\frac{\Delta Y}{\Delta X}=\frac{P_{X}}{P_{Y}}
    \end{aligned}$$

- 최적 선택 하에서는 $\displaystyle\frac{MU_{X}}{P_{X}}$ 과 $\displaystyle\frac{MU_{Y}}{P_{Y}}$ 이 일치함

    $$
    \frac{MU_{X}}{MU_{Y}}=\frac{P_{X}}{P_{Y}} \Leftrightarrow \frac{MU_{X}}{P_{X}}=\frac{MU_{Y}}{P_{Y}}
    $$

    - $\displaystyle\frac{MU_{X}}{P_{X}}$ : 화폐 단위당 취득 가능한 X재 단위의 한계효용
    - $\displaystyle\frac{MU_{Y}}{P_{Y}}$ : 화폐 단위당 취득 가능한 Y재 단위의 한계효용

-----

## Sourse

- https://enotesworld.com/price-budget-line-or-budget-constraint/
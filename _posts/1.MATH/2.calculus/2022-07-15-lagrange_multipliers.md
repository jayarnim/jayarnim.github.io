---
order: 5
title: Lagrange Multipliers
date: 2022-07-15
categories: [1.MATHEMATICAL TECHS, 2.calculus]
tags: [mathematics, calculus]
math: true
description: >-
    Based on the lecture “Mathematics for Artificial Intelligence (2022-1)” by Prof. Yeo Jin Chung, Dept. of AI, Big Data & Management, College of Business Administration, Kookmin Univ.
image:
    path: /_post_refer_img/1.MATH/2.calculus/Thumbnail.jpg
---

## Lagrange Multipliers
-----

- **라그랑주 승수법(Lagrange Multipliers)** : 제약 조건이 주어진 최적화 문제(즉, 제한된 범위 내에서 최대값이나 최소값을 구하는 문제)를 해결하기 위한 수학적 기법으로서, 주로 다변수 함수의 최적화 문제 풀이에 사용됨

    $$\begin{aligned}
    \Theta^{*} =
    \begin{cases}
    \text{arg} \min{\mathcal{L}} \quad & \text{minimum}\\
    \text{arg} \max{\mathcal{L}} \quad & \text{maximun}
    \end{cases}
    \end{aligned}$$

## How to Solve
-----

- Notation:
    - $f(x,y,\cdots)$ : 목적 함수
    - $g_{i}(x,y,\cdots)=0$ : $i$ 번째 등식 제약 조건
    - $h_{j}(x,y,\cdots) \le 0$ : $j$ 번째 비등식 제약 조건
    - $\lambda_{i}$ : $i$ 번째 등식 제약 조건의 라그랑주 승수로서 해당 제약 조건의 영향력
    - $\mu_{j}$ : $j$ 번째 비등식 제약 조건의 라그랑주 승수로서 해당 제약 조건의 영향력

- Lagrangian Function:

    $$\begin{aligned}
    &\mathcal{L}(x,y,\cdots,\lambda_{1}, \cdots, \mu_{1},\cdots)\\
    &= f(x,y,\cdots) + \sum_{i}{\lambda_{i} \cdot g_{i}(x,y,\cdots)} + \sum_{j}{\mu_{j} \cdot h_{j}(x,y,\cdots)}
    \end{aligned}$$

- how to solve:

    $$\begin{aligned}
    \nabla\mathcal{L}\left(x^{*},y^{*},\cdots,\lambda^{*}_{1}, \cdots, \mu_{1}^{*}, \cdots\right)
    &= 0
    \end{aligned}$$

## KKT
-----

- **KKT 조건(Karush-Kuhn-Tucker Conditions)**: 비등식 제약 하 최적화 문제에서 라그랑주 승수법을 적용하기 위한 조건

- **1차 최적성 조건(Stationarity)**: 목적 함수의 기울기와 제약 조건의 기울기가 균형을 이룸

    $$\begin{aligned}
    \nabla f(x^{*}) + \sum_{i}{\lambda_{i} \cdot \nabla g_{i}(x^{*})} + \sum_{j}{\mu_{j} \cdot \nabla h_{j}(x^{*})} = 0
    \end{aligned}$$

- **제약 조건의 만족(Primal Feasibility)**: 최적의 해가 주어진 제약 조건을 만족해야 함

    $$\begin{aligned}
    \forall g(x^{*}) = 0, \quad \forall h(x^{*}) \le 0
    \end{aligned}$$

- **이중성 조건 (Dual Feasibility)**: 비등식 제약 조건에 대한 라그랑주 승수는 음수가 될 수 없음

    $$\begin{aligned}
    \forall\mu \ge 0
    \end{aligned}$$

- **슬랙 조건 (Complementary Slackness)**: 비등식 제약 조건이 활성(active)일 때만 해당 제약 조건이 최적화 문제에 영향을 미침

    $$\begin{aligned}
    \forall\mu \cdot \forall h(x^{*}) = 0
    \end{aligned}$$
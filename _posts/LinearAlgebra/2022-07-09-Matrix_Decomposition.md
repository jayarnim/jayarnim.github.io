---
order: 6
title: Matrix Decomposition
date: 2022-07-09
categories: [Mathematical Techs, Linear Algebra]
tags: [Mathematics]
math: true
description: >-
  Based on the lecture “Mathematics for Artificial Intelligence (2022-1)” by Prof. Yeo Jin Chung, Dept. of AI, Big Data & Management, College of Business Administration, Kookmin Univ.
image:
  path: /_post_refer_img/LinearAlgebra/Thumbnail.png
---

## Matrix Decomposition
-----

- **정의** : 하나의 행렬을 특정한 구조를 가진 다른 행렬의 합과 곱으로 나타내는 작업

- **종류**
    - **스펙트럼 분해(Spectral Decomposition)** : 대칭행렬에 대한 분해
    - **특이값 분해(Singular Value Decomposition; SVD)** : 비대칭행렬에 대한 분해

## Spectral Decomposition
-----

- **대칭행렬 $A_{n \times n}$** 와 그 고유값 $ \vert \lambda_{1} \vert \ge \vert \lambda_{2} \vert \ge \cdots \ge \vert \lambda_{n} \vert$, 고유벡터 $\overrightarrow{v_{1}},\overrightarrow{v_{2}},\cdots,\overrightarrow{v_{n}}$ 에 대하여, 직교행렬 $P$ 와 대각행렬 $\Lambda$ 를 다음과 같이 정의하자

    $$\begin{aligned}
    P
    &= \begin{bmatrix} \overrightarrow{v_{1}} & \overrightarrow{v_{2}} & \cdots & \overrightarrow{v_{n}} \end{bmatrix} \\
    \Lambda
    &= diag(\lambda_1, \lambda_2, \cdots, \lambda_n)
    \end{aligned}$$

- $A_{n \times n}$ 를 다음과 같이 분해하는 작업을 스펙트럼 분해라고 정의함

    $$\begin{aligned}
    A
    &= P \Lambda P^{T} \\
    &= \lambda_1 \overrightarrow{v_{1}} \overrightarrow{v_{1}^T} + \lambda_2 \overrightarrow{v_{2}} \overrightarrow{v_{2}^T} + \cdots + \lambda_n \overrightarrow{v_{n}} \overrightarrow{v_{n}^T} \\
    &= \displaystyle\sum_{i=1}^{n}\lambda_i \overrightarrow{v_{i}} \overrightarrow{v_{i}^T}
    \end{aligned}$$

## Singular Value Decomposition
-----

### SVD

- 비대칭행렬 $A_{m \times n}$ 에 대하여 다음과 같이 분해하는 작업을 특이값 분해라고 정의함

    $$\begin{aligned}
    A_{m \times n}
    =
    \begin{cases}
    U_{n \times m} D_{m \times m} (V_{n \times m})^T\;&if\;m \le n \\
    U_{m \times n} D_{n \times n} (V_{n \times n})^T\;&if\;n \le m \\
    \end{cases}
    \end{aligned}$$

- 행렬 $U$ 는 행렬 $AA^{T}(=(A^{T}A)^T)$ 의 고유벡터 $\overrightarrow{u}$ 의 집합임

    $$\begin{aligned}
    U &= \begin{bmatrix} \overrightarrow{u_1}&\overrightarrow{u_2}&\cdots&\overrightarrow{u_k} \end{bmatrix}\\
    k &= \min (m, n)\\
    &= rank(A)\\
    \overrightarrow{u_i} 
    &\in \{\overrightarrow{u}\,|\,AA^{T}\overrightarrow{u} = \lambda \overrightarrow{u}\}
    \end{aligned}$$

- 행렬 $V$ 는 행렬 $A^{T}A(=(AA^{T})^T)$ 의 고유벡터 $\overrightarrow{v}$ 의 집합임

    $$\begin{aligned}
    U
    &= \begin{bmatrix} \overrightarrow{v_1}&\overrightarrow{v_2}&\cdots&\overrightarrow{v_k} \end{bmatrix}\\
    k
    &= \min (m, n)\\
    &= rank(A)\\
    \overrightarrow{v_i}
    &\in \{\overrightarrow{v}\,|\,A^{T}A\overrightarrow{v} = \lambda \overrightarrow{v}\}
    \end{aligned}$$

- 행렬 $D$ 는 행렬 $AA^{T}$ 혹은 그 전치행렬 $A^{T}A$ 의 고유값의 제곱근 $\sqrt{\lambda_1} \ge \sqrt{\lambda_2} \ge \cdots \ge \sqrt{\lambda_k} > 0$ 을 대각원소로 가지는 대각행렬임

    $$\begin{aligned}
    D
    &= diag(\sqrt{\lambda_1}, \sqrt{\lambda_2}, \cdots, \sqrt{\lambda_k}) \\
    &= \begin{pmatrix}
    \sqrt{\lambda_1} & 0 & \cdots & 0 \\
    0 & \sqrt{\lambda_2} & \cdots & 0 \\
    \vdots & \vdots & \ddots & \vdots \\
    0 & 0 & \cdots & \sqrt{\lambda_k}
    \end{pmatrix} \\
    k
    &= \min (m, n)\\
    &= rank(A)
    \end{aligned}$$

### Singular Value & Vector

- **특이값(Singular Value)** : 대각행렬 $D$ 의 대각원소로서, 행렬 $AA^{T}$ 혹은 그 전치행렬 $A^{T}A$ 의 고유값의 제곱근

    $$
    \sqrt{\lambda_1} \ge \sqrt{\lambda_2} \ge \cdots \ge \sqrt{\lambda_k} > 0
    $$

- **왼쪽 특이벡터(Left Singular Vector)** : 행렬 $U$ 의 열벡터로서 행렬 $AA^{T}$ 의 고유벡터

    $$\begin{aligned}
    \overrightarrow{u_i} 
    &\in \{\overrightarrow{u}\,|\,AA^{T}\overrightarrow{u} = \lambda \overrightarrow{u}\},\\
    k
    &= \min (m, n)\\
    &= rank(A)
    \end{aligned}$$

- **오른쪽 특이벡터(Right Singular Vector)** : 행렬 $V$ 의 열벡터로서 행렬 $AA^{T}$ 의 전치행렬 $A^{T}A$ 의 고유벡터

    $$\begin{aligned}
    \overrightarrow{v_i}
    &\in \{\overrightarrow{v}\,|\,A^{T}A\overrightarrow{v} = \lambda \overrightarrow{v}\},\\
    k
    &= \min (m, n)\\
    &= rank(A)
    \end{aligned}$$

- **특이값 분해의 전개**

    $$\begin{aligned}
    A_{m \times n}
    &=
    \begin{cases}
    U_{n \times m} D_{m \times m} (V_{n \times m})^T\;if\;m \le n \\
    U_{m \times n} D_{n \times n} (V_{n \times n})^T\;if\;n \le m \\
    \end{cases} \\
    &= \displaystyle\sum_{i=1}^{\min (m,n)} \sqrt{\lambda_i} u_i v_i^T
    \end{aligned}$$
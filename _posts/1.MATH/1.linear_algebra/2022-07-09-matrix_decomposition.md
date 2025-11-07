---
order: 6
title: Matrix Decomposition
date: 2022-07-09
categories: [1.MATHEMATICAL TECHS, 1.linear algebra]
tags: [mathematics, linear algebra]
math: true
description: >-
    Based on the lecture “Mathematics for Artificial Intelligence (2022-1)” by Prof. Yeo Jin Chung, Dept. of AI, Big Data & Management, College of Business Administration, Kookmin Univ.
image:
    path: /_post_refer_img/1.MATH/1.linear_algebra/Thumbnail.png
---

## Matrix Decomposition
-----

- **행렬 분해(Matrix Decomposition)**: 고차원 행렬을 특정한 구조를 가진 저차원 행렬들의 합과 곱으로 근사하는 기법
    - **스펙트럼 분해(Spectral Decomposition)**: 대칭행렬에 대한 분해
    
    $$\begin{aligned}
    \mathbf{A} \approx \mathbf{P}\Lambda\mathbf{P}^{T}, \quad \mathbf{A}=\mathbf{A}^{T}
    \end{aligned}$$
    
    - **특이값 분해(`S`ingular `V`alue `D`ecomposition)**: 비대칭 행렬에 대한 분해

    $$\begin{aligned}
    \mathbf{A} \approx \mathbf{U}\Sigma\mathbf{V}^{T}
    \end{aligned}$$

## Spectral Decomposition
-----

- 대칭행렬 $$\mathbf{A} \in \mathbb{R}^{N \times N}$$ 에 대하여, 그 차원이 $$N \times N$$  이라면 $$N$$ 개의 고유벡터 $$\mathbf{v}_{i}$$ 와 고유값 $$\lambda_{i}$$ 이 존재함

$$\begin{aligned}
\mathbf{A}\mathbf{v}_{i}=\lambda_{i}\mathbf{v}_{i},\quad i=1,2,\cdots,N
\end{aligned}$$

- 대칭행렬 $$\mathbf{A} \in \mathbb{R}^{N \times N}$$ 의 고유벡터들은 모두 직교함

$$\begin{aligned}
\mathbf{v}_{1} \perp \mathbf{v}_{2} \perp \cdots \perp \mathbf{v}_{N}
\end{aligned}$$

- 따라서 대칭행렬 $$\mathbf{A}$$ 는 항상 직교 대각화(orthogonal diagonalization) 가능함

$$\begin{aligned}
\mathbf{P}^{T}\mathbf{A}\mathbf{P}
&=\Lambda, \quad \mathbf{P}^{T}=\mathbf{P}^{-1}
\end{aligned}$$

- 이로부터 대칭행렬 $$\mathbf{A}$$ 를 대각화 행렬 $$\mathbf{P}=\begin{bmatrix}\mathbf{v}_{1} & \mathbf{v}_{2} & \cdots & \mathbf{v}_{N}\end{bmatrix}$$ 와 고유값 대각 행렬 $$\Lambda=\mathrm{diag}(\lambda_{1},\lambda_{2},\cdots,\lambda_{N})$$ 의 곱으로 근사할 수 있음

$$\begin{aligned}
\mathbf{P}^{T}\mathbf{A}\mathbf{P}
&=\Lambda\\
(\mathbf{P}\mathbf{P}^{T})\mathbf{A}(\mathbf{P}\mathbf{P}^{T})
&=\mathbf{P}\Lambda\mathbf{P}^{T}\\
\mathbf{I}\mathbf{A}\mathbf{I}
&=\mathbf{P}\Lambda\mathbf{P}^{T},\quad (\because \mathbf{P}^{T}=\mathbf{P}^{-1})\\
\therefore \mathbf{A}
&= \mathbf{P}\Lambda\mathbf{P}^{T}
\end{aligned}$$

## Singular Value Decomposition
-----

- 비대칭행렬 $$\mathbf{A} \in \mathbb{R}^{M \times N}$$ 에 대하여 다음을 정의하자

    $$
    \begin{aligned}
    \mathbf{P}
    &= \mathbf{A}\mathbf{A}^{T} \in \mathbb{R}^{M \times M}\\
    \mathbf{Q}
    &= \mathbf{A}^{T}\mathbf{A} \in \mathbb{R}^{N \times N}
    \end{aligned}$$

- 왼쪽 특이벡터 행렬 $$\mathbf{U}$$ 과 오른쪽 특이벡터 행렬 $$\mathbf{V}$$ 을 각각 다음과 같이 구성하자

    $$\begin{aligned}
    \mathbf{U}
    &= \begin{bmatrix}\mathbf{u}_{1} & \mathbf{u}_{2} & \cdots & \mathbf{u}_{K}\end{bmatrix}\\
    \mathbf{V}
    &= \begin{bmatrix}\mathbf{v}_{1} & \mathbf{v}_{2} & \cdots & \mathbf{v}_{K}\end{bmatrix}
    \end{aligned}, \quad
    K=\mathrm{rank}(\mathbf{A})
    $$

    - $$\mathbf{u}$$: 왼쪽 특이벡터(Left Singular Vector)

        $$
        \forall \mathbf{u}:\mathbf{P}\mathbf{u}=\lambda\mathbf{u}
        $$

    - $$\mathbf{v}$$: 오른쪽 특이벡터(Right Singular Vector)

        $$
        \forall \mathbf{v}:\mathbf{Q}\mathbf{v}=\lambda\mathbf{v}
        $$

- $$\mathbf{P}$$ 와 $$\mathbf{Q}$$ 는 전치 관계이므로 그 고유값이 동일하며, 이때 고유값 $$\lambda_{i}$$ 의 제곱근을 특이값(Singular Value)이라 함

    $$\begin{aligned}
    \sqrt{\lambda_{i}}
    \end{aligned}$$

- 특이값 대각 행렬 $$\Sigma$$ 는 특이값 $$\sqrt{\lambda_{i}}$$ 을 대각 원소로 가지는 대각행렬임

    $$\begin{aligned}
    \Sigma
    &= \mathrm{diag}(\sqrt{\lambda_{1}},\sqrt{\lambda_{2}},\cdots,\sqrt{\lambda_{K}})
    \end{aligned}$$

- 비대칭행렬 $$\mathbf{A} \in \mathbb{R}^{M \times N}$$ 은 다음과 같이 근사될 수 있음

    $$\begin{aligned}
    \mathbf{A}
    &\approx \mathbf{U}\Sigma\mathbf{V}^{T}
    \end{aligned}$$
---
order: 8
title: Distance Embedding based Latent Factor Model
date: 2024-04-17
categories: [AI Application, Recommender System]
tags: [AI Application, Recommender System, Collaborative Filtering, Latent Factor Model, MLP]
math: true
description: >-
    Based on the following lectures <br>
    (1) “Recommendation System Design (2024-1)” by Prof. Ha Myung Park, Dept. of Artificial Intelligence. College of SW, Kookmin Univ. <br>
    (2) "Recommender System (2024-2)" by Prof. Hyun Sil Moon, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
    path: /_post_refer_img/RecommenderSystem/Thumbnail.jpg
---

## Distance Embedding Method: DDFL
-----

- **Representation Learning based Collaborative Filtering** : 내적(Dot Product)을 활용한 유사도 계산은 삼각 부등식(Triangular Inequality)을 만족하지 못함
    - **삼각 부등식(Triangular Inequality)** : 세 점 사이의 거리에 대한 제한 조건으로서, $A$ 와 $C$ 사이 거리는 $A$ 에서 $B$, 그리고 $B$ 에서 $C$ 로 우회하는 거리보다 크거나 같아야 함

        $$\begin{aligned}
        \text{d}\left[A,C\right] \le \text{d}\left[A,B\right] + \text{d}\left[B,C\right]
        \end{aligned}$$

    - 즉, 사용자 $u$ 가 아이템 $i$ 를 직접적으로 선호하는 정도는, 사용자 $u$ 가 아이템 $j$ 를 선호하는 정도 및 아이템 $i$ 와 $j$ 간 유사한 정도의 합보다 작거나 같아야 함

        $$\begin{aligned}
        \overrightarrow{\mathbf{p}}_{u} \cdot \overrightarrow{\mathbf{q}}_{i}
        \le \overrightarrow{\mathbf{p}}_{u} \cdot \overrightarrow{\mathbf{q}}_{j}
        + \overrightarrow{\mathbf{q}}_{i} \cdot \overrightarrow{\mathbf{q}}_{j}
        \end{aligned}$$

- **DDFL(`D`eep `D`ual `F`unction `L`earning-based Model)** : 히스토리 임베딩(History Embedding)에서 표현 학습과 매칭 함수 학습을 결합하는 대신, 거리 함수 학습(MeFL)과 매칭 함수 학습(MaFL)을 결합함으로써 삼각 부등식이 위배됨에 따른 비합리적 추천 결과를 보완함
    - [DDFL: A Deep Dual Function Learning-Based Model for Recommender Systems(2020)](https://doi.org/10.1007/978-3-030-59419-0_36)

### How to Modeling

![05](/_post_refer_img/RecommenderSystem/08-01.png){: width="100%"}

- **MeFL(`Me`tric `F`unction `L`earning)** : 사용자, 아이템 표현 학습 시 삼각 부등식을 고려함으로써 합리적 추천 결과를 도모함

    - Conversion Transformation:

        $$\begin{aligned}
        y_{u,i}&=\alpha\left(1-r_{u,i}\right)
        \end{aligned}$$

        - $r_{u,i} \in \mathbf{R}$ is Implicit Feedback

    - Linear Transformation:

        $$\begin{aligned}
        \mathbf{P}^{\text{MeFL}}&= \mathbf{W}_{\text{MeFL}}^{(P)} \cdot \mathbf{Y} \in \mathbb{R}^{M \times K}\\
        \mathbf{Q}^{\text{MeFL}}&= \mathbf{W}_{\text{MeFL}}^{(P)} \cdot \mathbf{Y}^{T} \in \mathbb{R}^{N \times K}
        \end{aligned}$$

    - Calculate Euclidean Distance:

        $$\begin{aligned}
        \overrightarrow{\mathbf{d}}_{u,i}
        = \begin{bmatrix}
        \left(p^{\text{MeFL}}_{u,1}-q^{\text{MeFL}}_{i,1}\right)^{2}
        & \left(p^{\text{MeFL}}_{u,2}-q^{\text{MeFL}}_{i,2}\right)^{2} 
        & \cdots 
        & \left(p^{\text{MeFL}}_{u,K}-q^{\text{MeFL}}_{i,K}\right)^{2}
        \end{bmatrix}
        \end{aligned}$$

    - Metric Function Predictive Vector:

        $$\begin{aligned}
        \overrightarrow{\mathbf{z}}^{\text{MeFL}}_{u,i} &= \text{MLP}_{\text{ReLU}}\left[\overrightarrow{\mathbf{d}}_{u,i}\right]
        \end{aligned}$$

- **MaFL(`Ma`tching `F`unction `L`earning)**

    - Linear Transformation:

        $$\begin{aligned}
        \mathbf{P}^{\text{MaFL}}&= \mathbf{W}_{\text{MaFL}}^{(P)} \cdot \mathbf{R} \in \mathbb{R}^{M \times K}\\
        \mathbf{Q}^{\text{MaFL}}&= \mathbf{W}_{\text{MaFL}}^{(Q)} \cdot \mathbf{R}^{T} \in \mathbb{R}^{N \times K}
        \end{aligned}$$

    - Matching Function Predictive Vector:

        $$\begin{aligned}
        \overrightarrow{\mathbf{z}}^{\text{MaFL}}_{u,i} &= \text{MLP}_{\text{ReLU}}\left[\overrightarrow{\mathbf{p}}_{u} \oplus \overrightarrow{\mathbf{q}}_{i}\right]
        \end{aligned}$$

- **Fusion**

    $$\begin{aligned}
    \hat{r}_{u,i} &= \sigma\Bigg(\text{MLP}_{\text{ReLU}}\left[\overrightarrow{\mathbf{z}}^{\text{MeFL}}_{u,i} \oplus \overrightarrow{\mathbf{z}}^{\text{MaFL}}_{u,i}\right]\Bigg)
    \end{aligned}$$
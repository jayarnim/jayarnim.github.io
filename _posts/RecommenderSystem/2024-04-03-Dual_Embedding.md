---
order: 7
title: Dual Embedding based Latent Factor Model
date: 2024-04-03
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

## Embedding Type
-----

- **아이디 임베딩(ID Embedding)**
    - Embedding user and item identifiers into a low-dimensional vector space
    - 사용자의 고유한 선호 정보나 아이템의 고유한 특징 정보를 반영한 표현을 도출함
    - 사용자와 아이템의 맥락 정보가 부족하여 행동 패턴이나 구매 패턴을 반영하기 어려움

- **히스토리 임베딩(History Embedding)**
    - Generate each user and item expressions based on past interaction history
    - 사용자의 행동 패턴이나 아이템의 구매 패턴을 반영한 표현을 도출함
    - 사용자와 아이템을 상호간에 의존하여 표현하므로 고유 정보를 보존하기 어려움

## DNCF
-----

- **문제 의식**: 아이디 임베딩과 히스토리 임베딩의 상호 보완적 관계
    - 아이디 임베딩은 고유 정보를 보존한 표현을 생성하는 데 강점
    - 히스토리 임베딩은 맥락 정보를 반영한 표현을 생성하는 데 강점

- [**`DNCF`**](https://doi.org/10.48550/arXiv.2102.02549): 아이디 임베딩과 히스토리 임베딩을 결합하여 표현력을 강화하는 모형
    - He, G., Zhao, D., & Ding, L.\\
    (2021).\\
    Dual-embedding based neural collaborative filtering for recommender systems.\\
    arXiv preprint arXiv:2102.02549.

### How to Modeling

![03](/_post_refer_img/RecommenderSystem/07-01.png){: width="100%"}

- **ID based Embedding**

    $$\begin{aligned}
    \overrightarrow{\mathbf{p}}_{u}&=\text{Embedding}\left[\overrightarrow{\mathbf{z}}_{u}\right] \in \mathbb{R}^{K}\\
    \overrightarrow{\mathbf{q}}_{i}&=\text{Embedding}\left[\overrightarrow{\mathbf{z}}_{i}\right] \in \mathbb{R}^{K}
    \end{aligned}$$

    - $\overrightarrow{\mathbf{z}}_{u}$ : ID One-Hot Vector of User $i$
    - $\overrightarrow{\mathbf{z}}_{i}$ : ID One-Hot Vector of Item $j$
    - $\overrightarrow{\mathbf{p}}_{u}$ : ID Embedding Vector of User $i$
    - $\overrightarrow{\mathbf{q}}_{i}$ : ID Embedding Vector of Item $j$

- **Interaction based Embedding**

    $$\begin{aligned}
    \overrightarrow{\mathbf{m}}_{u}
    &=\text{AGG}\left[\left\{\overrightarrow{\mathbf{h}}_{j} \mid j \in \mathcal{R}_{u}^{+}\right\}\right] \in \mathbb{R}^{K}\\
    &=\frac{1}{\sqrt{\vert \mathcal{R}_{u}^{+}\vert}}\mathbf{W}^{(P)} \cdot \mathbf{R}_{u,:}\\
    \overrightarrow{\mathbf{n}}_{i}
    &=\text{AGG}\left[\left\{\overrightarrow{\mathbf{h}}_{v} \mid v \in \mathcal{R}_{i}^{+}\right\}\right] \in \mathbb{R}^{K}\\
    &=\frac{1}{\sqrt{\vert \mathcal{R}_{i}^{+}\vert}}\mathbf{W}^{(Q)} \cdot \mathbf{R}_{:,i}
    \end{aligned}$$

    - $\mathbf{R}_{u,:}$ : Multi-Hot Vector of User $u$ @ User-Item Interaction Matrix
    - $\mathbf{R}_{:,i}$ : Multi-Hot Vector of Item $i$ @ User-Item Interaction Matrix
    - $\overrightarrow{\mathbf{m}}_{u}$ : ID Embedding Vector of User $u$
    - $\overrightarrow{\mathbf{n}}_{i}$ : ID Embedding Vector of Item $i$

- **Embedding Combination**
    - User Embedding Combination:

        $$\begin{aligned}
        \overrightarrow{\mathbf{x}}_{u}
        &=\overrightarrow{\mathbf{p}}_{u} \oplus \overrightarrow{\mathbf{m}}_{u} \in \mathbb{R}^{2K}
        \end{aligned}$$

    - Item Embedding Combination:

        $$\begin{aligned}
        \overrightarrow{\mathbf{y}}_{i}
        &=\overrightarrow{\mathbf{q}}_{i} \oplus \overrightarrow{\mathbf{n}}_{i} \in \mathbb{R}^{2K}
        \end{aligned}$$

- **Neural Collaborative Filtering and Predict**

    $$\begin{aligned}
    \hat{r}_{u,i} &= \sigma\Big[\text{MLP}_{\text{ReLU}}\left[\overrightarrow{\mathbf{x}}_{u} \oplus \overrightarrow{\mathbf{y}}_{i}\right]\Big]
    \end{aligned}$$
---
order: 7
title: Dual Embedding based Latent Factor Models
date: 2024-02-29
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

## Dual Embedding Method: DNCF
-----

- **DELF(`D`ual-`E`mbedding based `L`atent `F`actor Model)**
    - **ID Embedding** : 사용자, 아이템의 ID만을 활용하므로 사용자 행동 패턴이나 아이템 구매 패턴을 유추할 만한 맥락 정보가 부족함
    - **History Embedding** : 사용자와 아이템의 고유한 정체성, 예컨대 사용자의 독립적인 선호나 아이템의 독립적 특성보다는 과거 어떤 아이템, 사용자와 상호작용했는지에 지나치게 의존함
    - 이중 임베딩(Dual-Embedding)을 결합하지 않고 독립적으로 학습하여 최종 표현을 생성하므로 각각의 한계점을 서로 보완하는 표현력을 기대하기 어려움

- **DNCF(`D`ual-embedding based `N`eural `C`ollaborative `F`iltering)** : 이중 임베딩을 사용하되, 두 임베딩을 결합하여 학습함으로써 사용자, 아이템 표현을 개선함
    - [Dual-embedding based Neural Collaborative Filtering for Recommender Systems(2021)](https://doi.org/10.48550/arXiv.2102.02549)

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
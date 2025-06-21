---
order: 7
title: Semi-Dual Embedding based Latent Factor Model
date: 2024-04-03
categories: [AI Application, Recommender System]
tags: [AI Application, Recommender System, Collaborative Filtering, MLP, Attention Mechanism]
math: true
description: >-
    Based on the following lectures <br>
    (1) “Recommendation System Design (2024-1)” by Prof. Ha Myung Park, Dept. of Artificial Intelligence. College of SW, Kookmin Univ. <br>
    (2) "Recommender System (2024-2)" by Prof. Hyun Sil Moon, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
    path: /_post_refer_img/RecommenderSystem/Thumbnail.jpg
---

## ID Embedding Assist.: DRNet
-----

- **Previous Research**
    - **User based Collaborative Filtering** : 선호 패턴이 유사한 사용자 간 연관성을 학습할 수 있지만, 아이템 특성을 명시적으로 표현할 수 없음
    - **Item based Collaborative Filtering** : 구매 패턴이 유사한 아이템 간 연관성을 학습할 수 있지만, 사용자 선호를 명시적으로 표현할 수 없음
    - **Latent Factor Model** : 사용자와 아이템의 고유성을 명시적으로 표현할 수 있지만, 희박성(Sparsity)이 높을 경우 표현력을 신뢰할 수 없고, 특정 아이템과 사용자의 과거 행동 간 연관성을 반영하지 못함

- **DRNet(`D`ual `R`elation `Net`-work)** : Latent Factor Model 과 Item based Collaborative Filtering 을 결합하여 사용자-아이템 관계와 아이템-아이템 관계를 동시에 모델링함으로써 개인화 추천 정확도를 높이면서도 데이터 희박성 문제에 대한 강건성을 도모함
    - [Dual Relations Network for Collaborative Filtering(2020)](https://doi.org/10.1109/ACCESS.2020.3002102)

### How to Modeling

![01](/_post_refer_img/RecommenderSystem/07-01.png){: width="100%"}

- **Affection Network** : Modeling User-Item Relation

    $$\begin{aligned}
    \overrightarrow{\mathbf{z}}_{u,i}^{\text{Affection}}
    &= \text{MLP}_{\text{ReLU}}\left[\overrightarrow{\mathbf{p}}_{u} \odot \overrightarrow{\mathbf{q}}_{i}\right]
    \end{aligned}$$

- **Association Network** : Modeling Item-Item Relation

    - Global Item Vector of User $u$:

        $$\begin{aligned}
        \overrightarrow{\mathbf{g}}_{u}
        &= \text{ATTN}\left[\overrightarrow{\mathbf{v}}_{i}, \overrightarrow{\mathbf{s}}^{(u)}_{j}, \overrightarrow{\mathbf{s}}^{(u)}_{j}\right] \in \mathbb{R}^{K}
        \end{aligned}$$

        - $i$ : Target Item
        - $j^{\forall} \in \mathbf{R}_{u}^{+} \setminus i$ : Interaction Item of User $u$
        - $\overrightarrow{\mathbf{v}}_{i} \in \mathbb{R}^{K}$ : Target Item Vector @ Association Network
        - $\overrightarrow{\mathbf{s}}^{(u)}_{j} \in \mathbb{R}^{K}$ : Historical Item Vector of User $u$

    - Deep Interaction:

        $$\begin{aligned}
        \overrightarrow{\mathbf{z}}_{u,i}^{\text{Association}}
        &= \text{MLP}_{\text{ReLU}}\left[\overrightarrow{\mathbf{g}}_{u} \odot \overrightarrow{\mathbf{v}}_{i}\right]
        \end{aligned}$$

- **Fusion**

    $$\begin{aligned}
    r_{u,i}
    &= \sigma\left[\overrightarrow{\mathbf{z}}_{u,i}^{\text{Affection}} \oplus \overrightarrow{\mathbf{z}}_{u,i}^{\text{Association}} \right]
    \end{aligned}$$
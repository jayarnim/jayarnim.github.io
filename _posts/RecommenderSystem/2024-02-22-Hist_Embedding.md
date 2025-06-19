---
order: 6
title: History Embedding based Latent Factor Models
date: 2024-02-22
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

## Learning Objectives
-----

- **표현 학습(Representation Learning)**

- **매칭 함수 학습(Matching Function Learning)**

## DMF
-----

![01](/_post_refer_img/RecommenderSystem/06-01.png){: width="100%"}

## J-NCF
-----

![02](/_post_refer_img/RecommenderSystem/06-02.png){: width="100%"}

## DeepCF
-----

- **Representation Learning based Collaborative Filtering** : 사용자와 아이템을 공통의 잠재 공간에 사상하여 **내적(Dot Product)** 을 통해 유사도를 측정함
    - 내적은 선형성을 가정하므로 상호작용의 비선형성을 학습할 수 없음
    - 내적은 잠재요인 차원 간 독립성을 가정하므로 차원 간 상호작용을 학습할 수 없음
    - 내적은 모든 차원의 비중을 동일하게 취급하므로 차원 간 중요도에 차등을 둘 수 없음

- **Matching Function Learning based Collaborative Filtering** : 벡터 결합(Vector Concatenation)과 **신경망 알고리즘(Neural Network Algorithm)** 을 통해 사용자와 아이템 쌍의 복잡한 매칭 함수를 학습함
    - 사용자와 아이템 간 단순 선형 유사성이나 각각의 주요 패턴을 포착하여 일반화된 표현을 학습하기에 어려움
    - 파라미터 수가 기하급수적으로 증가하므로 데이터 희박성에 따른 차원의 저주 발생

- **DeepCF(`Deep` `C`ollaborative `F`iltering)** : 표현 학습과 매칭 함수 학습을 결합함으로써 저랭크 표현 학습 효율성을 달성하는 동시에 사용자와 아이템 간 상호작용에 대한 풍부한 표현력을 확보함
    - [DeepCF: A Unified Framework of Representation Learning and Matching Function Learning in Recommender System(2019)](https://doi.org/10.48550/arXiv.1901.04704)

### How to Modeling

![03](/_post_refer_img/RecommenderSystem/06-03.png){: width="100%"}

- **Representation Learning** : Dimension Reduction

    $$\begin{aligned}
    \mathbf{Y}_{\text{RL}}
    &= \text{MLP}_{\text{ReLU}}\left[\mathbf{R}\right] \odot \text{MLP}_{\text{ReLU}}\left[\mathbf{R}^{T}\right]
    \end{aligned}$$

    - $$\mathbf{R} \in \mathbb{R}^{M \times N}$$ : User-Item Interaction Matrix
    - $$\mathbf{P}_{\text{RL}}=\text{MLP}_{\text{ReLU}}\left(\mathbf{R}\right) \in \mathbb{R}^{M \times K}$$ : User-Latent Factor Matrix of Representation Learning
    - $$\mathbf{Q}_{\text{RL}}=\text{MLP}_{\text{ReLU}}\left(\mathbf{R}^{T}\right) \in \mathbb{R}^{N \times K}$$ : Item-Latent Factor Matrix of Representation Learning
    - $$\mathbf{Y}_{\text{RL}} \in \mathbb{R}^{(M \times N) \times K}$$ : Predictive Vector of Representation Learning

- **Matching Function Learning** : Linear Transformation

    $$\begin{aligned}
    \mathbf{Y}_{\text{ML}}
    &= \text{MLP}_{\text{ReLU}}\left[\mathbf{P}_{\text{ML}} \oplus \mathbf{Q}_{\text{ML}}\right]
    \end{aligned}$$

    - $$\mathbf{P}_{\text{ML}} = \mathbf{W}^{(P)} \cdot \mathbf{R} \in \mathbb{R}^{M \times K}$$ : User-Latent Factor Matrix of Matching Function Learning
    - $$\mathbf{Q}_{\text{ML}} = \mathbf{W}^{(Q)} \cdot \mathbf{R}^{T} \in \mathbb{R}^{N \times K}$$ : Item-Latent Factor Matrix of Matching Function Learning
    - $$\mathbf{Y}_{\text{RL}} \in \mathbb{R}^{(M \times N) \times K}$$ : Predictive Vector of Matching Function Learning

- **Fusion**

    $$\begin{aligned}
    \mathbf{Y}
    &= \sigma\left[\mathbf{Y}_{\text{RL}} \oplus \mathbf{Y}_{\text{ML}}\right]
    \end{aligned}$$
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
    - 사용자와 아이템을 공동의 잠재요인 공간에 표현하는 방법
    - 매칭 강도 추정 시 내적(Inner Product) 등 선형 유사도 함수를 적용함
    - 저차원(Low-rank) 유사도 구조를 효율적으로 포착할 수 있음

- **매칭 함수 학습(Matching Function Learning)**
    - 사용자-아이템 쌍을 입력으로 하여 매칭 함수를 직접 학습하는 방법
    - 복잡하고 비선형적인 매칭 함수를 근사할 수 있음

## DMF
-----

- **문제 의식**:

- [**`DMF`**](https://doi.org/10.24963/ijcai.2017/447): 
    - Xue, H. J., Dai, X., Zhang, J., Huang, S., & Chen, J.\\
    (2017, August).\\
    Deep matrix factorization models for recommender systems.\\
    In IJCAI (Vol. 17, pp. 3203-3209).

### How to Modeling

![01](/_post_refer_img/RecommenderSystem/06-01.png){: width="100%"}

- **Annotation**

## J-NCF
-----

- **문제 의식**:

- [**`J-NCF`**](https://doi.org/10.1145/3343117):
    - Chen, W., Cai, F., Chen, H., & Rijke, M. D.\\
    (2019).\\
    Joint neural collaborative filtering for recommender systems.\\
    ACM Transactions on Information Systems (TOIS), 37(4), 1-30.

### How to Modeling

![02](/_post_refer_img/RecommenderSystem/06-02.png){: width="100%"}

- **Annotation**

## DeepCF
-----

- **문제 의식**: 표현 학습 방식과 매칭 함수 학습 방식의 상호 보완적 관계
    - 표현 학습은 저차원 유사도 구조를 포착하여 사용자, 아이템의 일반화된 표현을 도출하는 데 강점
    - 매칭 함수 학습은 사용자와 아이템 간 복잡하고 비선형적인 상호작용 과정을 근사하는 데 강점

- [**`DeepCF`**](https://doi.org/10.48550/arXiv.1901.04704): 표현 학습 모듈과 매칭 함수 학습 모듈을 병렬 학습하는 앙상블 모형
    - Deng, Z. H., Huang, L., Wang, C. D., Lai, J. H., & Yu, P. S.\\
    (2019, July).\\
    Deepcf: A unified framework of representation learning and matching function learning in recommender system.\\
    In Proceedings of the AAAI conference on artificial intelligence (Vol. 33, No. 01, pp. 61-68).

### How to Modeling

![03](/_post_refer_img/RecommenderSystem/06-03.png){: width="100%"}

- **Annotation**

- **`CFNet-rl`** : Dimension Reduction

    $$\begin{aligned}
    \mathbf{Y}_{\text{RL}}
    &= \text{MLP}_{\text{ReLU}}\left[\mathbf{R}\right] \odot \text{MLP}_{\text{ReLU}}\left[\mathbf{R}^{T}\right]
    \end{aligned}$$

    - $$\mathbf{R} \in \mathbb{R}^{M \times N}$$ : User-Item Interaction Matrix
    - $$\mathbf{P}_{\text{RL}}=\text{MLP}_{\text{ReLU}}\left(\mathbf{R}\right) \in \mathbb{R}^{M \times K}$$ : User-Latent Factor Matrix of Representation Learning
    - $$\mathbf{Q}_{\text{RL}}=\text{MLP}_{\text{ReLU}}\left(\mathbf{R}^{T}\right) \in \mathbb{R}^{N \times K}$$ : Item-Latent Factor Matrix of Representation Learning
    - $$\mathbf{Y}_{\text{RL}} \in \mathbb{R}^{(M \times N) \times K}$$ : Predictive Vector of Representation Learning

- **`CFNet-ml`** : Linear Transformation

    $$\begin{aligned}
    \mathbf{Y}_{\text{ML}}
    &= \text{MLP}_{\text{ReLU}}\left[\mathbf{P}_{\text{ML}} \oplus \mathbf{Q}_{\text{ML}}\right]
    \end{aligned}$$

    - $$\mathbf{P}_{\text{ML}} = \mathbf{W}^{(P)} \cdot \mathbf{R} \in \mathbb{R}^{M \times K}$$ : User-Latent Factor Matrix of Matching Function Learning
    - $$\mathbf{Q}_{\text{ML}} = \mathbf{W}^{(Q)} \cdot \mathbf{R}^{T} \in \mathbb{R}^{N \times K}$$ : Item-Latent Factor Matrix of Matching Function Learning
    - $$\mathbf{Y}_{\text{RL}} \in \mathbb{R}^{(M \times N) \times K}$$ : Predictive Vector of Matching Function Learning

- **`CFNet`**

    $$\begin{aligned}
    \mathbf{Y}
    &= \sigma\left[\mathbf{Y}_{\text{RL}} \oplus \mathbf{Y}_{\text{ML}}\right]
    \end{aligned}$$
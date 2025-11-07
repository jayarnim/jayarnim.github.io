---
order: 3
title: History Embedding based Latent Factor Model
date: 2024-03-13
categories: [6.RECOMMENDER SYSTEM, 2.mlp based collaborative filtering]
tags: [ai application, recommender system, collaborative filtering, latent factor model, ncf, neural networks, mlp]
math: true
description: >-
    Based on the following lectures <br>
    (1) “Recommendation System Design (2024-1)” by Prof. Ha Myung Park, Dept. of Artificial Intelligence. College of SW, Kookmin Univ. <br>
    (2) "Recommender System (2024-2)" by Prof. Hyun Sil Moon, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
    path: /_post_refer_img/6.RECSYS/2.mlp/Thumbnail.jpg
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

- **문제 의식**: 아이디 임베딩(ID Embedding) 입력 표현의 한계점
    - 아이디 임베딩 방식은 초기 표현(식별자)의 정보량이 부족하여 학습이 느리거나 성능이 제한됨

- **[`DMF`](https://doi.org/10.24963/ijcai.2017/447)(`D`eep `M`atrix `F`actorization)**: 사용자-아이템 상호작용 행렬과 그 전치 행렬을 초기 표현으로 사용하여 저차원 표현 학습을 수행하는 모형
    - Xue, H. J., Dai, X., Zhang, J., Huang, S., & Chen, J.\\
    (2017, August).\\
    Deep matrix factorization models for recommender systems.\\
    In IJCAI (Vol. 17, pp. 3203-3209).

### Notation

- $u=1,2,\cdots,M$: user idx
- $i=1,2,\cdots,N$: item idx
- $\mathbf{Y} \in \mathbb{R}^{M \times N}$: user-item interaction matrix
- $\overrightarrow{\mathbf{u}}_{u} \in \mathbb{R}^{K}$: user latent factor vector
- $\overrightarrow{\mathbf{v}}_{i} \in \mathbb{R}^{K}$: item latent factor vector
- $\hat{y}_{u,i}$: interaction probability of user $u$ and item $i$

### How to Modeling

![01](/_post_refer_img/6.RECSYS/2.mlp/03-01.png){: width="100%"}

- user latent factor vector representation learning:

    $$\begin{aligned}
    \overrightarrow{\mathbf{u}}_{u}
    &= \text{MLP}_{\text{ReLU}}(\mathbf{Y}_{u*})
    \end{aligned}$$

- item latent factor vector representation learning:

    $$\begin{aligned}
    \overrightarrow{\mathbf{v}}_{i}
    &= \text{MLP}_{\text{ReLU}}(\mathbf{Y}_{*i})
    \end{aligned}$$

- Predict interaction probability of user $u$ and item $i$:

    $$\begin{aligned}
    \hat{y}_{u,i}
    &= \cos(\overrightarrow{\mathbf{u}}_{u}, \overrightarrow{\mathbf{v}}_{i})\\
    &= \frac{\overrightarrow{\mathbf{u}}_{u} \cdot \overrightarrow{\mathbf{v}}_{i}}{\Vert \overrightarrow{\mathbf{u}}_{u} \Vert \cdot \Vert \overrightarrow{\mathbf{v}}_{i} \Vert}
    \end{aligned}$$

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

- **Components**
    - **`CFNet-rl`**: `R`epresentation `L`earning
    - **`CFNet-ml`**: `M`atching Function `L`earning
    - **`CFNet`**: `CFNet-rl` & `CFNet-ml` Ensemble

### Notation

- $u=1,2,\cdots,M$: user idx
- $i=1,2,\cdots,N$: item idx
- $\mathbf{Y} \in \mathbb{R}^{M \times N}$: user-item interaction matrix
- $\overrightarrow{\mathbf{u}}_{u} \in \mathbb{R}^{K}$: user latent factor vector
- $\overrightarrow{\mathbf{v}}_{i} \in \mathbb{R}^{K}$: item latent factor vector
- $\overrightarrow{\mathbf{z}}_{u,i}$: predictive vector of user $u$ and item $i$
- $\hat{y}_{u,i}$: interaction probability of user $u$ and item $i$

### How to Modeling

![03](/_post_refer_img/6.RECSYS/2.mlp/03-03.png){: width="100%"}

- `CFNet` is `CFNet-rl` & `CFNet-ml` Ensemble

    $$\begin{aligned}
    \hat{y}_{u,i}
    &= \sigma(\overrightarrow{\mathbf{w}} \cdot [\overrightarrow{\mathbf{z}}_{u,i}^{\text{(RL)}} \oplus \overrightarrow{\mathbf{z}}_{u,i}^{\text{(ML)}}])
    \end{aligned}$$

#### CFNet-rl

- user latent factor vector representation learning:

    $$\begin{aligned}
    \overrightarrow{\mathbf{u}}_{u}
    &= \text{MLP}_{\text{ReLU}}(\mathbf{Y}_{u*})
    \end{aligned}$$

- item latent factor vector representation learning:

    $$\begin{aligned}
    \overrightarrow{\mathbf{v}}_{i}
    &= \text{MLP}_{\text{ReLU}}(\mathbf{Y}_{*i})
    \end{aligned}$$

- predictive vector of user $u$ and item $i$:

    $$\begin{aligned}
    \overrightarrow{\mathbf{z}}_{u,i}
    &= \overrightarrow{\mathbf{u}}_{u} \odot \overrightarrow{\mathbf{v}}_{i}
    \end{aligned}$$

- if use `CFNet-rl` as a single prediction module:

    $$\begin{aligned}
    \hat{y}_{u,i}
    &= \sigma(\overrightarrow{\mathbf{w}} \cdot \overrightarrow{\mathbf{z}}_{u,i})
    \end{aligned}$$

#### CFNet-ml

- generate user latent factor vector through linear transformation:

    $$\begin{aligned}
    \overrightarrow{\mathbf{u}}_{u}
    &= \mathbf{W} \cdot \mathbf{Y}_{u*}
    \end{aligned}$$

- generate user latent factor vector through linear transformation:

    $$\begin{aligned}
    \overrightarrow{\mathbf{v}}_{i}
    &= \mathbf{W} \cdot \mathbf{Y}_{*i}
    \end{aligned}$$

- predictive vector of user $u$ and item $i$:

    $$\begin{aligned}
    \overrightarrow{\mathbf{z}}_{u,i}
    &= \text{MLP}_{\text{ReLU}}(\overrightarrow{\mathbf{u}}_{u} \oplus \overrightarrow{\mathbf{v}}_{i})
    \end{aligned}$$

- if use `CFNet-ml` as a single prediction module:

    $$\begin{aligned}
    \hat{y}_{u,i}
    &= \sigma(\overrightarrow{\mathbf{w}} \cdot \overrightarrow{\mathbf{z}}_{u,i})
    \end{aligned}$$

## J-NCF
-----

- **문제 의식**
    - **아이디 임베딩(ID Embedding)**: 사용자와 아이템 표현을 무작위로 초기화한 후 매칭 함수 학습을 수행하므로 표현 학습이 미흡함 (ex. `NCF`)
    - **히스토리 임베딩(History Embedding)**: 사용자-아이템 상호작용 행렬과 그 전치 행렬을 활용하여 표현 학습을 수행하나 매칭 함수는 선형 유사도 함수에 의존함 (ex. `DMF`)
    - **앙상블(Ensemble)**: 표현 학습과 매칭 함수 학습을 분리하여 수행하므로 각 모듈이 서로의 학습을 보완하거나 강화하지 못함 (ex. `CFNet`)

- **[`J-NCF`](https://doi.org/10.1145/3343117)(`J`oint `N`eural `C`ollaborative `F`iltering)**: 표현 학습과 매칭 함수 학습을 통합 훈련(Joint Training)하는 모형
    - Chen, W., Cai, F., Chen, H., & Rijke, M. D.\\
    (2019).\\
    Joint neural collaborative filtering for recommender systems.\\
    ACM Transactions on Information Systems (TOIS), 37(4), 1-30.

### Notation

- $u=1,2,\cdots,M$: user idx
- $i=1,2,\cdots,N$: item idx
- $\mathbf{Y} \in \mathbb{R}^{M \times N}$: user-item interaction matrix
- $\overrightarrow{\mathbf{u}}_{u} \in \mathbb{R}^{K}$: user latent factor vector
- $\overrightarrow{\mathbf{v}}_{i} \in \mathbb{R}^{K}$: item latent factor vector
- $\overrightarrow{\mathbf{z}}_{u,i}$: predictive vector of user $u$ and item $i$
- $\hat{y}_{u,i}$: interaction probability of user $u$ and item $i$

### How to Modeling

![02](/_post_refer_img/6.RECSYS/2.mlp/03-02.png){: width="100%"}

- user latent factor vector representation learning:

    $$\begin{aligned}
    \overrightarrow{\mathbf{u}}_{u}
    &= \text{MLP}_{\text{ReLU}}(\mathbf{Y}_{u*})
    \end{aligned}$$

- item latent factor vector representation learning:

    $$\begin{aligned}
    \overrightarrow{\mathbf{v}}_{i}
    &= \text{MLP}_{\text{ReLU}}(\mathbf{Y}_{*i})
    \end{aligned}$$

- matching function learning:

    $$\begin{aligned}
    \overrightarrow{\mathbf{z}}_{u,i}
    &= \text{MLP}_{\text{ReLU}}(\overrightarrow{\mathbf{u}}_{u} \oplus \overrightarrow{\mathbf{v}}_{i})
    \end{aligned}$$

- Predict interaction probability of user $u$ and item $i$:

    $$\begin{aligned}
    \hat{y}_{u,i}
    &= \sigma(\overrightarrow{\mathbf{w}} \cdot \overrightarrow{\mathbf{z}}_{u,i})
    \end{aligned}$$
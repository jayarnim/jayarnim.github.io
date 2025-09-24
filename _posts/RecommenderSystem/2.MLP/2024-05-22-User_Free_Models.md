---
order: 8
title: User Free Models
date: 2024-05-22
categories: [RECOMMENDER SYSTEM, 2.mlp based collaborative filtering]
tags: [AI Application, Recommender System, Collaborative Filtering, MLP, Attention Mechanism]
math: true
description: >-
    Based on the following lectures <br>
    (1) “Recommendation System Design (2024-1)” by Prof. Ha Myung Park, Dept. of Artificial Intelligence. College of SW, Kookmin Univ. <br>
    (2) "Recommender System (2024-2)" by Prof. Hyun Sil Moon, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
    path: /_post_refer_img/RecommenderSystem/2.MLP/Thumbnail.jpg
---

## SLIM
-----

- **문제 의식**: 효율성과 정확성의 Trade-off
    - **이웃 기반 협업 필터링(Neighborhood-based Collaborative Filtering)**: 유사도 기반 휴리스틱 함수를 통해 예측하므로 계산 효율성은 높지만 아이템 간 관계 학습이 불가하여 추천 정확도가 낮음
    - **잠재요인 모형(Latent Factor Model)**: 사용자, 아이템 간 관계 학습을 수반하므로 추천 정확도는 높지만 계산 비용이 발생하여 실시간 추천에 부적합

- **[`SLIM`](https://doi.org/10.1109/ICDM.2011.134)(`S`parse `LI`near `M`ethods)**: 아이템 간 유사도를 선형 회귀계수 행렬로 학습하고 이를 기반으로 예측을 수행하는 선형 회귀 모형
    - Ning, X., & Karypis, G.\\
    (2011, December).\\
    Slim: Sparse linear methods for top-n recommender systems.\\
    In 2011 IEEE 11th international conference on data mining (pp. 497-506).\\
    IEEE.

### Notation

- $u=1,2,\cdots,M$: user idx
- $i=1,2,\cdots,N$: item idx
- $\mathbf{Y} \in \mathbb{R}^{M \times N}$: user-item interaction matrix
- $\mathbf{W} \in \mathbb{R}^{N \times N}$: sparse aggregation coefficient matrix
- $\hat{y}_{u,i}$: interaction probability of user $u$ and item $i$

### How to Modeling

- Linear Regression:

    $$\begin{aligned}
    \hat{y}_{u,i}
    &= \mathbf{W}_{i} \cdot \mathbf{Y}_{u*}\\
    &= \sum_{j \in \mathcal{R}_{u}^{+} \setminus \{i\}}{w_{i,j} \cdot y_{u,j}}
    \end{aligned}$$

- Objective Function:

    $$\begin{gathered}
    \hat{\mathbf{W}}
    = \text{arg} \min{\frac{1}{2} \Vert \mathbf{Y} - \mathbf{Y}\mathbf{W}\Vert_{F}^{2} + \frac{\beta}{2} \Vert \mathbf{W} \Vert_{F}^{2} + \lambda \Vert \mathbf{W} \Vert_{1}}\\
    \text{subject to} \quad
    \begin{aligned}
    \mathbf{W} &\ge 0\\
    \text{diag}(\mathbf{W})&=0
    \end{aligned}
    \end{gathered}$$

    - $$\Vert \mathbf{Y} - \mathbf{Y}\mathbf{W}\Vert_{F}^{2}$$: Reconstruction Loss
    - $$\Vert \mathbf{W} \Vert_{F}^{2}$$: L2 Norm Regulation to Prevent Overfitting
    - $$\Vert \mathbf{W} \Vert_{1}$$: L1 Norm Regulation to Induce Sparsity

## FISM
-----

- **문제 의식**: `SLIM` 의 사용자 선호 구성 방식
    - `SLIM` 은 아이템 간 유사도를 휴리스틱 함수가 아니라 학습을 통해 도출한다는 점에서 아이템 기반 협업 필터링의 정확도 문제를 개선함
    - 하지만 사용자의 타깃 아이템에 대한 선호 구성 시 히스토리를 구성하는 아이템들이 서로 독립적으로 기여한다고 가정함
    - 이 독립성 가정은 사용자 선호가 과거 경험의 단순 집계로 환원될 수 있다는 잘못된 전제에 기반함
    - 즉, 사용자 선호가 히스토리 아이템들의 집합적 구성과 그 내부의 상호작용 구조에 의해 형성된다는 점을 간과함

- **[`FISM`](https://doi.org/10.1145/2487575.2487589)(`F`actored `I`tem `S`imilarity `M`odels)**: 사용자 선호를 히스토리 아이템들의 집합적 평균으로 구성하는 아이템 기반 협업 필터링 모형
    - Kabbur, S., Ning, X., & Karypis, G.\\
    (2013, August).\\
    Fism: factored item similarity models for top-n recommender systems.\\
    In Proceedings of the 19th ACM SIGKDD international conference on Knowledge discovery and data mining (pp. 659-667).

### Notation

- $u=1,2,\cdots,M$: user idx
- $i=1,2,\cdots,N$: target item idx
- $j=1,2,\cdots,N$: history item idx
- $\overrightarrow{\mathbf{p}}_{i} \in \mathbb{R}^{K}$: target item id embedding vector
- $\overrightarrow{\mathbf{q}}_{j} \in \mathbb{R}^{K}$: history item id embedding vector

### How to Modeling

- ID Embedding:

    $$\begin{aligned}
    \overrightarrow{\mathbf{p}}_{i}
    &= \text{Emb}(j)\\
    \overrightarrow{\mathbf{q}}_{j}
    &= \text{Emb}(i)
    \end{aligned}$$

- History Item Aggregation:

    $$\begin{aligned}
    \overrightarrow{\mathbf{u}}_{u}
    &= \frac{1}{\vert \mathcal{R}_{u}^{+} \setminus \{i\} \vert^{\beta}}\sum_{j \in \mathcal{R}_{u}^{+} \setminus \{i\}}{\overrightarrow{\mathbf{q}}_{j}}
    \end{aligned}$$

    - $0 < \beta \le 1$

- Predict interaction probability of user $u$ and item $i$:

    $$\begin{aligned}
    \hat{y}_{u,i}
    &= \overrightarrow{\mathbf{u}}_{u} \cdot \overrightarrow{\mathbf{p}}_{i}
    \end{aligned}$$

## NAIS
-----

- **문제 의식**: `FISM` 의 히스토리 아이템 집계 방식
    - `FISM` 은 사용자 선호 표현 시 히스토리 아이템 간 기여도 차이를 간과하여 히스토리 아이템들을 단순 평균함

- **[`NAIS`](https://doi.org/10.1109/TKDE.2018.2831682)(`N`eural `A`ttentive `I`tem `S`imilarity Model)**: 사용자 선호를 히스토리 아이템으로써 구성하되, 개별 아이템의 기여도에 따라 가중 평균하는 아이템 기반 협업 필터링 모형
    - He, X., He, Z., Song, J., Liu, Z., Jiang, Y. G., & Chua, T. S.\\
    (2018).\\
    NAIS: Neural attentive item similarity model for recommendation.\\
    IEEE Transactions on Knowledge and Data Engineering, 30(12), 2354-2366.

### Notation

- $u=1,2,\cdots,M$: user idx
- $i=1,2,\cdots,N$: target item idx
- $j=1,2,\cdots,N$: history item idx
- $\overrightarrow{\mathbf{p}}_{i} \in \mathbb{R}^{K}$: target item id embedding vector
- $\overrightarrow{\mathbf{q}}_{j} \in \mathbb{R}^{K}$: history item id embedding vector

### How to Modeling

![01](/_post_refer_img/RecommenderSystem/2.MLP/08-01.png){: width="100%"}

- ID Embedding:

    $$\begin{aligned}
    \overrightarrow{\mathbf{p}}_{i}
    &= \text{Emb}(i)\\
    \overrightarrow{\mathbf{q}}_{j}
    &= \text{Emb}(j)
    \end{aligned}$$

- History Item Aggregation:

    $$\begin{aligned}
    \overrightarrow{\mathbf{u}}_{u}
    &= \text{ATTN}(\overrightarrow{\mathbf{p}}_{i}, \mathbf{Q}[\forall j \in \mathcal{R}_{u}^{+} \setminus \{i\},:], \mathbf{Q}[\forall j \in \mathcal{R}_{u}^{+} \setminus \{i\},:])
    \end{aligned}$$

- Predict interaction probability of user $u$ and item $i$:

    $$\begin{aligned}
    \hat{y}_{u,i}
    &= \overrightarrow{\mathbf{u}}_{u} \cdot \overrightarrow{\mathbf{p}}_{i}
    \end{aligned}$$

### How to Attention

- Attention Weight is Calculated by Smoothed Softmax:

    $$\begin{aligned}
    \alpha_{i,j}
    &= \frac{\exp{f(\overrightarrow{\mathbf{p}}_{i},\overrightarrow{\mathbf{q}}_{j})}}{\left[\sum_{j \in \mathcal{R}_{u}^{+} \setminus \{i\}}{\exp{f(\overrightarrow{\mathbf{p}}_{i},\overrightarrow{\mathbf{q}}_{j})}}\right]^{\beta}}
    \end{aligned}$$

    - $0 < \beta \le 1$

- Attention Score Function:

    - Concatenation:

        $$\begin{aligned}
        f(\overrightarrow{\mathbf{p}}_{i},\overrightarrow{\mathbf{q}}_{j})
        &= \overrightarrow{\mathbf{w}} \cdot \text{ReLU}(\mathbf{W}[\overrightarrow{\mathbf{p}}_{i} \oplus \overrightarrow{\mathbf{q}}_{j}] + \overrightarrow{\mathbf{b}})
        \end{aligned}$$

    - Element-wise Product:

        $$\begin{aligned}
        f(\overrightarrow{\mathbf{p}}_{i},\overrightarrow{\mathbf{q}}_{j})
        &= \overrightarrow{\mathbf{w}} \cdot \text{ReLU}(\mathbf{W}[\overrightarrow{\mathbf{p}}_{i} \odot \overrightarrow{\mathbf{q}}_{j}] + \overrightarrow{\mathbf{b}})
        \end{aligned}$$
---
order: 104
title: TimeSVD++
date: 2024-02-29
categories: [AI Application, Recommender System]
tags: [Paper Review, AI Application, Recommender System, Collaborative Filtering, Temporal Recommender System, Latent Factor Model]
math: true
description: >-
    <ul type="square">
    <li><strong>Title</strong>: <a href="https://doi.org/10.1145/1557019.1557072"><code>Collaborative Filtering with Temporal Dynamic</code></a></li>
    <li><strong>Published</strong>: <em>2009</em></li>
    <li><strong>Data Set</strong>: <a href="https://www.kaggle.com/datasets/netflix-inc/netflix-prize-data"><code>Netflix Prize</code></a></li>
    </ul>
image:
    path: /_post_refer_img/RecommenderSystem/Thumbnail.jpg
---

## Prerequisite
-----

- **협업 필터링(Collaborative Filtering)** : 과거 여러 사용자들이 다양한 아이템에 대하여 평가 점수를 매긴 기록을 활용하여 아직 상호작용하지 않은 아이템에 대한 사용자의 평점을 추론하는 방법론

    $$\begin{aligned}
    \hat{r}_{u,i}
    &= \mu + \beta_{u} + \beta_{i} + \text{what}
    \end{aligned}$$

    - $\hat{r}_{u,i}$ : 사용자 $u$ 의 아이템 $i$ 에 대한 평점 예측값
    - $\mu$ : 커뮤니티 평점 평균
    - $\beta_{u}$ : 사용자 $u$ 의 평균 평점 편차로서 사용자의 평점 척도
    - $\beta_{i}$ : 아이템 $i$ 의 평균 평점 편차로서 아이템의 인기도

- **잠재요인 모형(Latent Factor Model)** : 사용자 벡터와 아이템 벡터를 정체를 알 수 없는 $k$ 개의 특징 공간으로 사상하는 방법

    $$\begin{aligned}
    \text{what}
    &= \overrightarrow{\mathbf{p}}_{u} \cdot \overrightarrow{\mathbf{q}}_{i}^{T}
    \end{aligned}$$

    - $$\overrightarrow{\mathbf{p}}_{u} \in \mathbf{P}_{M \times K}$$ : 사용자-잠재요인 벡터로서, 사용자 $u$ 의 요인별 선호도
    - $$\overrightarrow{\mathbf{q}}_{i} \in \mathbf{Q}_{N \times K}$$ : 아이템-잠재요인 벡터로서, 아이템 $i$ 의 요인별 특성

- **SVD++** : 특정 사용자가 특정 아이템에 대하여 매길 평점을 추론함에 있어, 목표 아이템 외에 사용자가 상호작용했던 다른 아이템들의 잠재요인 정보들을 함께 고려하는 방법

    $$\begin{aligned}
    \overrightarrow{\mathbf{p}}_{u} \leftarrow \overrightarrow{\mathbf{p}}_{u} + \frac{\sum_{j \in R(u)}{\overrightarrow{\mathbf{q}}_{j}}}{\sqrt{\vert R(u)\vert}}
    \end{aligned}$$

    - $$\displaystyle\frac{\sum_{j \in R(u)}{\overrightarrow{\mathbf{q}}_{j}}}{\sqrt{\vert R(u)\vert}}$$ : 사용자 $u$ 가 상호작용한 아이템 벡터의 평균으로서, $u$ 가 상호작용한 아이템들의 평균적인 특성
    - $R(u)$ : 사용자 $u$ 가 상호작용한 아이템 집합

## Previous Research of Temporal Recommendation
-----

- **시간 창 접근 방식(Time-Window)** : 특정 시간 내 데이터만 고려하는 방법

    $$
    x(t) = \overline{x} + \gamma \cdot \left\lfloor \frac{t-t_{0}}{N} \right\rfloor
    $$

- **인스턴스 감쇠 접근 방식(Instance-Decay)** : 상호작용 시점이 오래된 정보일수록 그 중요도를 할인하는 방법

    $$
    x(t) = \overline{x} + \exp{\Big[-\lambda(t-t_{i})\Big]} \cdot x
    $$

- **한계점** : 시간의 변화에 따라 노이즈화된 정보 뿐만 아니라 변화 양상을 추론할 수 있는 유효한 정보까지 상실함

    > 지수시간감쇠율 $\lambda$ 을 완화할수록 성능이 개선되는 양상을 보였음. 이는 시간의 흐름에 따라 사용자의 평점 척도나 취향이 변하더라도 그러한 변화 양상을 나타내는 맥락 정보로서 과거 상호작용 정보가 유효함을 시사함. <br><br> 과거 상호작용 정보를 삭제하거나(시간 창 접근 방식), 단순히 가중치를 적용하여 그 중요도를 감쇠하는 방식은(인스턴스 감쇠 접근 방식) 노이즈 뿐만 아니라 상호작용 변화 양상을 추론할 수 있는 신호까지 함께 제거하게 됨.

## TimeSVD++
-----

- **TimeSVD++** : 시간의 흐름에 따른 Concept Drift 별 변화 양상을 사용자 개별 단위에서 포착하는 잠재요인 모형 기반 Temporal Recommendation

- **Concept Drift** : 시간의 흐름에 따른 평점의 변동성을 원인에 따라 여러 요소들로 구분한 것
    - 시간의 흐름에 따른 **사용자 평점 척도의 변동성**
    - 시간의 흐름에 따른 **아이템 인기도의 변동성**
    - 시간의 흐름에 따른 **요인별 사용자 선호도의 변동성**
    - ~~요인별 아이템 특성은 통상 시간의 흐름에 따라 변하지 않으므로 모델링하지 않음~~

### How to Modeling

- **사용자 평점 척도의 변동성**

    $$\begin{aligned}
    \beta_{u}(t)
    &= b^{(u)} + b^{(u)}_{t} + b^{(u)}_{\text{period}(t)} + \alpha^{(u)} \cdot \text{dev}^{(u)}(t)
    \end{aligned}$$

    - $b^{(u)}$ : 사용자의 평균 평점 척도

    - $b^{(u)}_{t}$ : 사용자 평점 척도의 일별 변동성

    - $b^{(u)}_{\text{period}(t)}$ : 사용자 평점 척도의 주기별 변동성
        - $\text{period}(t)$ : 주기(봄/여름/가을/겨울 등) 함수

    - $\alpha^{(u)} \cdot \text{dev}^{(u)}(t)$ : 사용자 평점 척도의 시간 변동성
        - $\alpha^{(u)}$ : 사용자 $u$ 의 평점 척도 변화율
        - $\text{dev}^{(u)}(t)$ : 사용자 $u$ 의 시간 편차

            $$
            \text{dev}^{(u)}(t) = \text{sign}\left[t-t^{(u)}\right] \cdot \vert t-t^{(u)} \vert^{\gamma}
            $$

            - $t$ : 현재 시점
            - $t^{(u)}$ : 사용자 $u$ 가 평점을 매긴 평균 시점
            - $\text{sign}(\cdot)$ : 부호 함수
            - $\gamma$ : $t$ 와 $t^{(u)}$ 의 차이에 대한 감쇠율

- **아이템 인기도의 변동성**

    $$\begin{aligned}
    \beta_{i \mid u}(t)
    &= \sigma^{(u)}(t) \cdot \left(b^{(i)} + b^{(i)}_{\text{bin}(t)}\right)
    \end{aligned}$$

    - $b^{(i)}$ : 아이템의 평균 인기도

    - $b^{(i)}_{\text{bin}(t)}$ : 아이템 인기도의 기간별 변동성
        - $\text{bin}(t)$ : 기간 함수

    - $\sigma^{(u)}(t)$ : 아이템 인기도의 영향력에 대한 사용자별 차이를 모델링하기 위한 가중치

        $$
        \sigma^{(u)}(t) = c^{(u)} + c^{(u)}_{t}
        $$

- **요인별 사용자 선호도의 변동성**

    $$\begin{aligned}
    \overrightarrow{\mathbf{p}}_{u}(t)
    &= \begin{pmatrix} p^{(u)}_{1}(t) & \cdots & p^{(u)}_{k}(t) \end{pmatrix}\\
    p^{(u)}_{f}(t)
    &= \pi^{(u)}_{f} + \pi^{(u)}_{f,t} + \pi^{(u)}_{f, \text{period}(t)} + \alpha^{(u)}_{f} \cdot \text{dev}^{(u)}(t)
    \end{aligned}$$

    - $\overrightarrow{\mathbf{p}}_{u}(t)$ : 시점 $t$ 에서 사용자 $u$ 의 사용자-잠재요인 벡터
    - $$p^{(u)}_{f}(t) \in \overrightarrow{\mathbf{p}}_{u}(t)$$ : 시점 $t$ 에서 사용자 $u$ 의 $f$ 번째 잠재요인 값

### Objective Function Optimization

- **Prediction**

    $$
    \hat{r}_{u,i}(t)
    = \mu + \beta_{u}(t) + \beta_{i \mid u}(t) + \left(\overrightarrow{\mathbf{p}}_{u}(t) + \frac{\sum_{j \in R(u)}{\overrightarrow{\mathbf{q}}_{j}}}{\sqrt{\vert R(u)} \vert} \right) \cdot \overrightarrow{\mathbf{q}}_{i}^{T}
    $$

- **Optimization**

    $$
    \hat{\beta}_{u}(t), \hat{\beta}_{i}(t), \hat{\mathbf{p}}_{u}(t), \hat{\mathbf{q}}_{i} \mid k, \gamma
    = \text{arg} \min_{\Theta}{\sum_{(u,i,t) \in \Omega}{\mathcal{J}\Big[r_{u,i}(t), \hat{r}_{u,i}(t)\Big]} + \lambda_{\Theta} \Vert \Theta \Vert^{2}}
    $$
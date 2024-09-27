---
order: 15
title: SASREC
date: 2024-06-05
categories: [Research Interest, Recommender System]
tags: [Paper Review, Data Mining, Recommender System, Sequential Recommender System, Deep Learning, Attention Mechanism]
math: true
description: >-
    <ul type="square">
    <li><strong>Title</strong>: <a href="https://ieeexplore.ieee.org/abstract/document/8594844?casa_token=JT5smtt5Z5sAAAAA:lFfXP_q_01zzLRSEc7p1zEyR_jZ7l1VjeTTCOUO6QMkDmw6HUM0BDtBSnPGpvH6XZmxvQwnGi-r7"><em>Self-Attentive Sequential Recommendation</em></a></li>
    <li><strong>Author</strong>: <em>Kang and McAuley</em></li>
    <li><strong>Publisher</strong>: <em>ICDM</em></li>
    <li><strong>Published</strong>: <em>2018</em></li>
    </ul>
image:
    path: /_post_refer_img/RecommenderSystem/Thumbnail.jpg
---

## Attention Mechanism

<p align="center"><img alt="summary" src="https://github.com/jayarnim/jayarnim/assets/116495744/7c4feb17-bc5e-41c9-9986-b685770a38f3" width=100%></p>

### Process

- **주의 점수(Attention Score) 도출**

    <p align="center"><img alt="attention_score" src="https://github.com/jayarnim/jayarnim/assets/116495744/c2df6f60-8d6b-4af2-b29f-a31616f07d96" width=100%></p>

    $$
    \overrightarrow{e}_{t}=\text{score}(\overrightarrow{s}_{t},\overrightarrow{h}_{i}) \quad\text{for}\;i=1,2,\cdots,N
    $$

    - $\overrightarrow{e}_{t}$ : 주의 점수로서 쿼리 벡터와 키 벡터 간 유사도
    - $\overrightarrow{s}_{t} \in \mathbf{Q}$ : 디코더의 $t$ 번째 셀의 은닉 상태로서 쿼리 벡터
    - $\overrightarrow{h}_{i} \in \mathbf{K}$ : 시퀀스 길이가 $N$ 일 때, 인코더의 $i$ 번째 셀의 은닉 상태로서 키 벡터

- **주의 분포(Attention Distribution) 도출**

    <p align="center"><img alt="attention_dist" src="https://github.com/jayarnim/jayarnim/assets/116495744/1977389a-e8a1-4e9e-80a1-ededafe30861" width=100%></p>

    $$
    \overrightarrow{\alpha}_{t}=\text{softmax}(\overrightarrow{e}_{t})
    $$

    - $\overrightarrow{\alpha}_{t}$ : $t$ 번째 쿼리 벡터($\overrightarrow{s}_{t}$)가 입력될 때, 각각의 키 벡터($\overrightarrow{h}_{i}$)가 $t+1$ 번째 쿼리 벡터($\overrightarrow{s}_{t+1}$)로 실현될 가능성

- **인코더 출력값으로서 주의 값(Attention Value) 도출**

    <p align="center"><img alt="attention_value" src="https://github.com/jayarnim/jayarnim/assets/116495744/de4218f3-59e6-484a-802e-dff08796e113" width=100%></p>

    $$
    \overrightarrow{v}_{t}=\sum_{i=1}^{N}{(\overrightarrow{\alpha}_{t})_{i}\cdot \overrightarrow{h}_{i}}
    $$

    - $\overrightarrow{v}_{t}\in \mathbf{V}$ : 주의 값으로서 $t$ 번째 쿼리 벡터($\overrightarrow{s}_{t}$)에 대한 키 벡터들의 주의 분포($\overrightarrow{\alpha}_{t}$)를 키 벡터($\overrightarrow{h}_{i}$)에 가중평균한 벡터

- **디코더 출력값 도출**

    <p align="center"><img alt="decoder_output" src="https://github.com/jayarnim/jayarnim/assets/116495744/92d8d081-496c-45c4-9b4d-40d036d6ed01" width=100%></p>

    $$
    \tilde{s}_{t}=\text{tanh}(\mathbf{W}_{c}[\overrightarrow{v}_{t};\overrightarrow{s}_{t}]+\overrightarrow{\beta}_{c})
    $$

    - $[\overrightarrow{v}_{t};\overrightarrow{s}_{t}]$ : 주의 값($\overrightarrow{v}_{t}$)과 디코더의 은닉 상태($\overrightarrow{s}_{t}$)를 결합한 벡터

        <p align="center"><img alt="concat" src="https://github.com/jayarnim/jayarnim/assets/116495744/95d19dad-18c3-4ff8-ba3d-0be44ecd4100" width=100%></p>

- **시점 $t$ 에서 모형 예측값 도출**

    $$
    \hat{y}_{t}=\text{softmax}(\mathbf{W}_{y} \cdot \tilde{s}_{t} + \overrightarrow{\beta}_{y})
    $$

### Positional Encoding

### Self Attention

</br><hr>

#### 이미지 출처

- https://wikidocs.net/22893
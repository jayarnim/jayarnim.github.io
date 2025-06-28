---
order: 1
title: What? Network
date: 2024-01-29
categories: [DATA MINING TECHS, 7.social media analytics]
tags: [Data Mining, Social Media, Social Network, Graph]
math: true
description: >-
  Based on the lecture “Social Media Analytics (2023-2)” by Prof. Byoung Gu Choi, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
  path: /_post_refer_img/DataMiningTechs/7.SocialMediaAnalytics/Thumbnail.jpg
---

## 정의
-----

- **네트워크(Network)** : 사회 연결망으로서 액터 및 그들 간 관계
    - 네트워크의 규모 혹은 크기를 네트워크에 존재하는 액터의 수로 측정함

- **액터(Actor)** : 사회 구성원으로서 노드(Node)로 표현함

- **연결관계(Relationship)** : 액터 간 관계로서 라인(Line)으로 표현함

## 종류
-----

### Directed

- **비방향 네트워크(Undirected Network)** : 방향성이 존재하지 않는 네트워크

- **방향 네트워크(Directed Network)** : 방향성이 존재하는 네트워크
    - **액터의 내향 연결 정도(Introvert Connection Degree)** : 액터가 연결 객체가 되는 연결관계 갯수
    - **액터의 외향 연결 정도(Outrovert Connection Degree)** : 액터가 연결 주체가 되는 연결관계 갯수

### Weighted

- **이진 네트워크(Binary Network)** : 연결 강도가 존재하지 않는 네트워크
- **가중 혹은 계량 네트워크(Weighted Network)** : 연결 강도가 존재하는 네트워크

### Focus

- **전역 네트워크(Global Network)** : 네트워크 전반에 대하여 초점을 맞추는 네트워크

- **에고 네트워크(Ego Network)** : 특정 노드에 대하여 초점을 맞추는 네트워크
    - **에고(Ego)** : 초점 노드
    - **알터(Alter)** : 에고와 연결관계를 맺고 있는 노드
    - 에고 네트워크 분석 시 알터와 에고의 연결관계는 고려하지 않음

## 표현
-----

### 그래프

![01](/_post_refer_img/DataMiningTechs/7.SocialMediaAnalytics/01-01.jpg){: width="100%"}

- 방향 네트워크의 경우 연결 방향을 화살표로 표기함
- 계량 네트워크의 경우 연결 강도를 숫자로 표기함

### 행렬

- $(i, j)$ 는 $N_i$ 의 $N_j$ 에 대한 연결 여부 및 강도를 나타냄

- 비방향 네트워크의 경우 $(i, j)=(j, i)$ 인 대칭 행렬임

    $$
    \begin{bmatrix}
    -&1&1&1&1\\
    1&-&1&0&1\\ 
    1&1&-&1&0\\
    1&0&1&-&1\\
    1&1&0&1&-
    \end{bmatrix}
    $$

- 방향 네트워크의 경우 상삼각은 외향 연결 정도를, 하삼각은 내향 연결 정도를 나타냄

    $$
    \begin{bmatrix}
    -&3&4&2&3\\
    0&-&0&0&5\\ 
    0&5&-&3&0\\
    0&0&0&-&4\\
    0&0&0&4&-
    \end{bmatrix}
    $$
---
order: 2
title: Connection and Density
date: 2024-02-02
categories: [AI & Data Mining, Social Media Analytics]
tags: [Data Mining, Social Media, Social Network, Graph]
math: true
image:
  path: /_post_refer_img/SocialMediaAnalytics/Thumbnail.jpg
---

## 연결 정도
-----

- **액터의 연결 정도(Actor Connection Degree)**
    - **정의** : 액터의 활동성(Activity)
    - **계산** : 노드의 라인 갯수

        $$
        0 \leq D(N_i) \leq g-1
        $$

        - $D(N_i)$ : 노드 $i$ 의 연결 정도
        - $g$ : 네트워크에 존재하는 노드 갯수

- **네트워크의 연결 정도(Network Connection Degree)**
    - **정의** : 네트워크에 존재하는 액터들의 평균적인 활동성
    - **계산** : 네트워크에 존재하는 노드의 평균 라인 갯수

        $$\begin{aligned}
        \overline{d}
        &=\frac{\sum_{i=1}^{g}{D(N_i)}}{g}\\
        &=\frac{2L}{g}
        \end{aligned}$$

        - $L$ : 네트워크에 존재하는 라인 갯수

- **연결 정도의 분산**
    - **정의** : 네트워크의 집중도 혹은 네트워크의 액터들 간 불균등성(Uniformity)
    - **계산** : 액터 간 활동성 편차

        $$
        S_{d}^{2}=\frac{\sum_{i=1}^{g}{D(N_i)-\overline{d}}}{g}
        $$

## 밀도와 포괄성
-----

### 밀도(Density)

- **정의** : 응집력(Cohesion)을 라인을 중심으로 측정한 개념
    - 이진 네트워크의 경우 연결관계 성립률을 의미함
    - 계량 네트워크의 경우 연결관계 평균 강도를 의미함

- **계산** : 네트워크에서 성립 가능한 라인 갯수 대비 실제 성립되어 있는 라인 갯수
    - **비방향 네트워크**

        $$
        D=\frac{\sum_{j=1}^{g}(x_{i})_{j}}{_{g}C_{2}}
        $$

        - $(x_{i})_{j}$ : 노드 $N_i$ 의 노드 $N_j$ 에 대한 연결 성립 여부 및 연결 강도
        - $$ _{g}C_{2} $$ : 성립 가능한 라인 갯수

    - **방향 네트워크**

        $$
        D=\frac{\sum_{j=1}^{g}(x_{i})_{j}}{_{g}P_{2}}
        $$

        - $(x_{i})_{j}$ : 노드 $N_i$ 의 노드 $N_j$ 에 대한 연결 성립 여부 및 연결 강도
        - $$ _{g}P_{2} $$ : 성립 가능한 라인 갯수

### 포괄성(Inclusiveness)

- **정의** : 응집력(Cohesion)을 노드를 중심으로 측정한 개념

- **계산** : 네트워크에 존재하는 노드 갯수 대비 다른 노드와 연결관계를 맺고 있는 노드 갯수

    $$
    I=\frac{g_c}{g}
    $$

    - $g_c$ : 다른 노드와 연결관계를 맺고 있는 노드 갯수

## 호혜성과 이행성
-----

### 호혜성(Reciprocity)

- **정의** : 방향 네트워크에서, $N_i$ 의 $N_j$ 에 대한 연결관계가 존재하고 동시에 $N_j$ 의 $N_i$ 에 대한 연결관계가 존재하는 경우

- **계산**
    - **양자관계(dyad)** : 연결관계가 성립되어 있는 액터쌍 대비 호혜적 액터쌍
    - **선택관계(arc)** : 연결관계가 성립될 수 있는 액터쌍 대비 호혜적 액터쌍

### 이행성 조건(Transitivity Condition)

- **정의** : 액터 $A$, $B$, $C$ 로 구성되어 있는 삼자관계에서 다음의 연결관계가 모두 성립되어 있는 경우
    - $A\rightarrow B$
    - $B\rightarrow C$
    - $A\rightarrow C$

- **해석** : 이행성 조건을 충족하는 삼자관계가 많을수록 군집화된 구조를 가지는 경향이 있음

- **계산** : 성립될 수 있는 삼자관계 갯수 대비 이행성 조건을 충족하는 삼자관계 갯수

### 삼자관계(Trid Relationship)

- **정의** : 방향 이진 네트워크에서, 세 액터 및 그 액터들 간 관계

- **삼자관계 센서스(Trid Census)**
    - **정의** : 삼자관계의 16가지 유형 중 각 유형이 어느 정도 출현하는지 파악하는 절차

    - **MAN 표기법**
        - **M(mutual)** : 호혜적 연결관계 갯수
        - **A(asymmetric)** : 비호혜적 연결관계 갯수
            - U(up)
            - D(down)
            - T(transitive)
            - C(cyclic)

        - **N(null)** : 고립 노드 갯수

- **삼자관계의 이행성**
    - **불완전 이행적(Vacuous or Vacuously Transitive)** : 삼자관계의 트리플이 모두 불완전 이행적일 경우
    - **비이행적(Intransitive)** : 삼자관계의 불완전 이행적인 트리플을 제외한 트리플 중 하나라도 비이행적일 경우
    - **이행적(Transitive)** : 삼자관계의 불완전 이행적인 트리플을 제외한 트리플이 모두 이행적일 경우

### 트리플(Triple)

- **정의** : 삼자관계에서 존재하는 액터들의 중복되지 않는 배열
    - $(A,B,C)$
    - $(A,C,B)$
    - $(B,A,C)$ 
    - $(B,C,A)$
    - $(C,A,B)$
    - $(C,B,A)$

- **트리플의 이행성 조건** : 이하 조건을 모두 충족하는 경우
    - $N_1\rightarrow N_2$ : 첫 번째 노드의 두 번째 노드에 대한 연결관계가 존재함
    - $N_2\rightarrow N_3$ : 두 번째 노드의 세 번째 노드에 대한 연결관계가 존재함
    - $N_1\rightarrow N_3$ : 첫 번째 노드의 세 번째 노드에 대한 연결관계가 존재함

- **트리플의 이행성 분류**
    - **이행적(Transitive)** : 세 조건이 모두 충족되는 경우
        - $N_1\rightarrow N_2$
        - $N_2\rightarrow N_3$
        - $N_1\rightarrow N_3$

    - **비이행적(Intransitive)** : 세 번째 조건이 충족되지 않는 경우
        - $N_1\rightarrow N_2$
        - $N_2\rightarrow N_3$
        - $N_1\not\rightarrow N_3$

    - **불완전 이행적(Vacuous or Vacuously Transitive)** : 이행성 여부를 판단하기 위해 필요한 연결관계 갯수가 부족하여 판단할 수 없는 경우
        - $N_1\not\rightarrow N_2$ or $N_2\not\rightarrow N_3$

### 클러스터링 계수(Clustering Coefficient)

- **정의** : 비방향 네트워크에 대한 이행성 판단 지표

- **로컬 클러스터링 계수(Local Clustering Coefficient)**
    - **정의** : 비방향 네트워크에서 액터의 이행성 정도

    - **계산** : 액터의 에고 네트워크 밀도

        $$
        D=\frac{\sum_{j=1}^{g}(x_{i})_{j}}{_{g}C_{2}}
        $$

        - $(x_{i})_{j}$ : 노드 $N_i$ 의 노드 $N_j$ 에 대한 연결 성립 여부 및 연결 강도
        - $$ _{g}C_{2} $$ : 성립 가능한 라인 갯수

- **글로벌 클러스터링 계수(Global Clustering Coefficient)**
    - **정의** : 비방향 네트워크에서 네트워크의 군집화 정도
    - **계산** : 로컬 클러스터링 계수에 대하여 로컬 네트워크의 크기에 대한 가중 평균

## 거리
-----

- **거리(Distance)** : 임의의 두 노드에 대하여 상호간에 멀리 위치하는 정도
- **워크(Walk)** : 임의의 두 노드에 대하여 상호간에 성립 가능한 직, 간접적인 연결 방법의 가짓수
- **워크 길이(Walk Length)** : 워크에 포함된 라인 갯수
- **경로(Path)** : 노드와 라인의 중복이 없는 워크
- **경로 길이(Path Length)** : 경로에 포함된 라인 갯수
- **도달 가능성(Reachable)** : 임의의 두 노드에 대하여, 상호간에 하나 이상의 경로가 존재하는 경우
- **최단 경로(Geodesic)** : 길이가 가장 짧은 경로
- **직경(Diameter)** : 최단 경로 중 가장 긴 거리
- **플로우(Flow)** : 상호간에 라인이 중복되지 않는 경로들의 집합
- **라인 연결성(Line Connectivity or Edge Connectivity)** : 경로를 없애기 위해 제거해야 하는 최소 라인 갯수
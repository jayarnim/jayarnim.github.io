---
order: 10
title: Clustering
date: 2024-01-10
categories: [Machine Learning Techs, Machine Learning]
tags: [Machine Learning, Unsupervised Learning, Clustering, Metric]
math: true
description: >-
  Based on the lecture “Intro. to Machine Learning (2023-2)” by Prof. Je Hyuk Lee, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
  path: /_post_refer_img/MachineLearning/Thumbnail.jpg
---

## What? Cluster Analysis
-----

### Cluster Analysis

- **정의** : 표본을 관측치 간 유사성과 상이성을 계산하여 k개의 군집으로 분할하는 작업

    >Cluster analysis or clustering is the task of grouping a set of objects in such a way that objects in the same group are more similar to each other than to those in other groups. (by.Wikipedia)

- **목표** : 군집 내 응집도 최대화 및 군집 간 분리도 최대화

    ![01](/_post_refer_img/MachineLearning/12-01.png){: width="100%"}

- **판별 분석과 비교**

    ![02](/_post_refer_img/MachineLearning/12-02.png){: width="100%"}

    - **판별 분석(Classification Analysis)**
        - **학습 방식** : 지도학습(훈련 관측치의 정답 정보를 사전에 알고 있음)
        - **학습 목표** : $X$ 와 $Y$ 의 관계를 나타내는 함수를 탐색함

    - **군집 분석(Cluster Analysis)**
        - **학습 방식** : 비지도학습(훈련 관측치의 정답 정보를 사전에 알 수 없거나 존재하지 않음)
        - **학습 목표** : 주어진 표본을 분할하는 여러 개의 군집을 탐색함

### 구분

- **관측치 중복 여부에 따른 구분**

    ![03](/_post_refer_img/MachineLearning/12-03.png){: width="100%"}

    - **Hard(or Crisp) Clustering** : 관측치가 하나의 군집에만 할당됨
    - **Soft(or Fuzzy) Clustering** : 관측치가 여러 개의 군집에 할당될 수 있음

- **군집 간 위계 여부에 따른 구분**

    ![04](/_post_refer_img/MachineLearning/12-04.png){: width="100%"}

    - **Partitional Clustering** : 군집 간 위계가 존재하지 않음
    - **Hierarchical Clustering** : 군집 간 위계가 존재함

## Metrics
-----

### 군집화 유효성 평가 기준

- **External** : 정답 정보와의 비교
    - Rand Statistic
    - Jaccard Coefficient
    - Folks and Mallows Index
    - Hurbert $\Gamma$ Statistic
    - **V-Measure**

- **Internal** : 군집 내 응집도
    - Cophenetic Correlation Coefficient
    - **Sum of Squared Error(SSE)**
    - Cohesion and Separation

- **Relative** : 군집 간 분리도
    - **Dunn Family of Indices**
    - Davies-Bouldin Index
    - Semi-partial R-squared
    - SD Validity Index
    - **Silhouette**

### External Metrics

- **V-Measure** : 정확성과 완전성의 조화평균

    $$\begin{aligned}
    \text{V}
    &= 2\times\frac{H(C|K) \cdot C(K|C)}{H(C|K) + C(K|C)}
    \end{aligned}$$

    - $H(C \vert K)$ : 정확성(Homogeneity)
    - $C(K \vert C)$ : 완전성(Completeness)

- **정확성(Homogeneity)** : 각 군집의 클래스에 대한 엔트로피 합계

    $$\begin{aligned}
    H(C|K)
    &= -\sum_{k=1}^{K}{\sum_{c=1}^{C}{P(c|k) \cdot \log{P(c|k)}}}
    \end{aligned}$$

    - $k$ : 군집 번호
    - $c$ : 클래스 번호
    - $P(c \vert k)$ : 군집 $K=k$ 가 주어졌을 때, 클래스 $C=c$ 가 발생할 가능성

- **완전성(Completeness)** : 각 클래스의 군집에 대한 엔트로피 합계

    $$\begin{aligned}
    C(K|C)
    &= -\sum_{c=1}^{C}{\sum_{k=1}^{K}{P(k|c) \cdot \log{P(k|c)}}}
    \end{aligned}$$

    - $P(k \vert c)$ : 클래스 $C=c$ 가 주어졌을 때, 군집 $K=k$ 가 발생할 가능성

### Internal Metrics

- **Sum of Squared Error(SSE)** : 각 군집의 중심점 벡터와 해당 군집 내 관측치 벡터 간 거리 자승으로 측정한 **군집 응집도**

    $$\begin{aligned}
    \text{SSE}
    &= \sum_{k=1}^{K}{\sum_{\overrightarrow{x}_{i} \in C_{k}}{||\overrightarrow{x}_{i}-\overrightarrow{\mu}_{k}||^2}}
    \end{aligned}$$

    - $k$ : 군집 번호
    - $C_{k}$ : $k$ 번째 군집
    - $$\overrightarrow{x}_{i} \in C_{k}$$ : 군집 $$C_{k}$$ 의 $i$ 번째 관측치 벡터
    - $$\overrightarrow{\mu}_{k} \in C_{k}$$ : 군집 $$C_{k}$$ 의 중심 벡터

### Relative Metrics

- **Dunn Index** : 군집 내 응집도(Cohesion) 최대값 대비 군집 간 분리도(Separation) 최소값 비율

    $$\begin{aligned}
    \text{DI}
    &= \frac{\min_{1 \le i \ne j \le K}{d_{C}(C_{i},C_{j})}}{\max_{1 \le k \le K}{\Delta(C_{k})}}
    \end{aligned}$$

    - $\min_{1 \le i \ne j \le K}{d_{C}(C_{i},C_{j})}$ : 군집 간 분리도 최소값으로서 분리도에 대한 최악의 경우
    - $\max_{1 \le k \le K}{\Delta(C_{k})}$ : 군집 내 응집도 최대값으로서 응집도에 대한 최악의 경우

- **실루엣 계수(Silhouette)** : 군집 내 응집성(cohesion)과 군집 간 분리도(separation)를 종합적으로 고려하여 측정한 **개별 관측치 벡터에 대한 군집화 적합성의 평균값**

    $$\begin{aligned}
    \text{S}
    &= \frac{1}{n}\sum_{i=1}^{n}{\frac{b(\overrightarrow{x}_{i})-a(\overrightarrow{x}_{i})}{\max{[a(\overrightarrow{x}_{i}),b(\overrightarrow{x}_{i})]}}}
    \end{aligned}$$

    - $$a(\overrightarrow{x}_{i})$$ : 관측치 벡터 $$\overrightarrow{x}_{i}$$ 기준 군집 내 응집도로서, 해당 관측치와 같은 군집에 속한 관측치와의 평균 거리
    - $$b(\overrightarrow{x}_{i})$$ : 관측치 벡터 $$\overrightarrow{x}_{i}$$ 기준 군집 간 분리도로서, 해당 관측치와 다른 군집에 속한 관측치와의 평균 거리 중 최소값

## k-Means
-----

### What? k-Means

- **정의** : 중심점 기반 배타적 분리형 군집화 알고리즘

    ![01](/_post_refer_img/MachineLearning/13-01.png){: width="100%"}

- **목표** : 각 군집에 대하여, **관측치와 중심점(Centroid) 간 평균 거리(Means)**를 최소화함

    $$
    \min_{\overrightarrow{\mu}_{i}}{\sum_{i=1}^{k}\sum_{\overrightarrow{x}_{j} \in C_{i}}{||\overrightarrow{x}_{j}-\overrightarrow{\mu}_{i}||^2}}
    $$

### 한계점

- **초기 군집 중심에 민감함**

    ![02](/_post_refer_img/MachineLearning/13-02.png){: width="100%"}

- **이상치에 민감함**

    ![03](/_post_refer_img/MachineLearning/13-03.png){: width="100%"}

- **구형이 아닌 형태의 군집을 탐지하기 어려움**

    ![04](/_post_refer_img/MachineLearning/13-04.png){: width="100%"}

- **서로 다른 규모의 군집을 탐지하기 어려움**

    ![05](/_post_refer_img/MachineLearning/13-05.png){: width="100%"}

- **서로 다른 밀도의 군집을 탐지하기 어려움**

    ![06](/_post_refer_img/MachineLearning/13-06.png){: width="100%"}

### 중심점 탐색 과정

![07](/_post_refer_img/MachineLearning/13-07.png){: width="100%"}

1. **군집 갯수를 설정함**

    $$
    X=C_{1} \cup C_{2} \cup \cdots \cup C_{k}\\
    \\ C_{i} \cap C_{j \ne i} = \emptyset
    $$

2. **$k$ 개의 초기 군집 중심 벡터 $\overrightarrow{c}$ 를 임의로 선정함**

    $$
    M=\{\overrightarrow{\mu}_{1},\overrightarrow{\mu}_{2},\cdots,\overrightarrow{\mu}_{k}\}
    $$

3. **모든 관측치 벡터 $\overrightarrow{x}$ 를 가장 가까운 거리에 위치한 중심 벡터 $\overrightarrow{\mu}$ 의 군집에 배타적으로 할당함**

    $$
    \overrightarrow{x}_{j} \rightarrow C_{i}\\
    \begin{aligned}
    \\\text{s.t.} \quad 
    & i=\text{arg} \min_{i}{||\overrightarrow{x}_{j}-\overrightarrow{\mu}_{i}||^2}\\
    &\overrightarrow{\mu}_{i} \in C_{i}
    \end{aligned}$$

4. **각 군집별 할당된 관측치 벡터들의 평균 벡터로 군집 중심 벡터를 갱신함**

    $$\begin{aligned}
    \overrightarrow{\mu}_{i}
    &=\displaystyle\frac{1}{|C_{i}|}\sum_{\overrightarrow{x}_{j}\in C_{i}}{\overrightarrow{x}_{j}}
    \end{aligned}$$

5. **③, ④의 과정을 반복하여 최적의 군집 중심 벡터 집합 $\hat{M}$ 을 탐색함**

    $$\begin{aligned}
    \hat{M}
    &= \{\overrightarrow{\mu}_{i} \big| \text{arg} \min_{\overrightarrow{\mu}_{i}}{\sum_{i=1}^{k}\sum_{\overrightarrow{x}_{j} \in C_{i}}{||\overrightarrow{x}_{j}-\overrightarrow{\mu}_{i}||^2}}\}
    \end{aligned}$$

## DBSCAN
-----

### `D`ensity-`B`ased `S`patial `C`lustering of `A`pplications with `N`oise

- **정의** : 밀도 기반 배타적 분리형 군집화 알고리즘

    ![01](/_post_refer_img/MachineLearning/14-01.png){: width="100%"}

- **군집** : 사전에 주어진 $\varepsilon, \text{MinPts}$ 에 기초했을 때 Maximality, Connectivity 조건을 만족하는 Non-Empty Subset

    ![02](/_post_refer_img/MachineLearning/14-02.png){: width="100%"}

    - **Maximality**

        > 표본 $D$ 에 속하는 관측치 벡터 $\overrightarrow{p}, \overrightarrow{q}$ 에 대하여, $\overrightarrow{p} \in C \subseteq D$ 이고, $\overrightarrow{q}$ 가 $\overrightarrow{p}$ 로부터 밀도 기준 도달 가능한(Directly Density-Reachable) 벡터이면, $\overrightarrow{q} \in C$ 임

    - **Connectivity**

        > 군집 $C$ 에 속하는 관측치 벡터 $\overrightarrow{p}, \overrightarrow{q}$ 간에는 밀도 기준 연결되어 있음(Density-Connected)

### 용어의 이해

- **$\varepsilon$-neighborhood of a point**

    ![03](/_post_refer_img/MachineLearning/14-03.png){: width="100%"}

    > 표본 $D$ 에 속하는 관측치 벡터 $\overrightarrow{p}$ 에 대하여, $\overrightarrow{p}$ 의 이웃 집합 $N_{\varepsilon}(\overrightarrow{p})$ 은 $\overrightarrow{p}$ 와의 거리가 $\varepsilon$ 이하인 관측치 벡터 $\overrightarrow{q}$ 의 집합임

    $$
    N_{\varepsilon}(\overrightarrow{p})
    =\{\overrightarrow{q} \in D \big| d(\overrightarrow{p},\overrightarrow{q}) \le \varepsilon\}
    $$

- **Directly Density-Reachable**

    ![04](/_post_refer_img/MachineLearning/14-04.jpg){: width="100%"}

    > **Core Point Condition** 을 만족하는 관측치 벡터 $\overrightarrow{p} \in D$ 에 대하여, **그 이웃 관측치 벡터($\varepsilon$-neighborhood of a point)** $\overrightarrow{q}$ 는 **$\overrightarrow{p}$ 로부터 밀도 기준 직접 도달 가능한(Directly Density-Reachable)** 관측치 벡터임

    - **Core Point Condition**

        $$
        |N_{\varepsilon}(\overrightarrow{p})| \ge \text{MinPts}
        $$

    - **Reachability**

        $$
        \overrightarrow{q} \in N_{\varepsilon}(\overrightarrow{p})
        $$

- **Density-Reachable**

    ![05](/_post_refer_img/MachineLearning/14-05.jpg){: width="100%"}

    > **Core Point Condition** 을 만족하는 관측치 벡터 $$\overrightarrow{p} \in D$$ 에 대하여, $$\overrightarrow{p}$$ 와 $$\overrightarrow{q}$$ 사이에 **$$\overrightarrow{p}$$ 로부터 밀도 기준 직접 도달 가능한 관측치 벡터 $$\overrightarrow{x}_{1},\overrightarrow{x}_{2},\cdots,\overrightarrow{x}_{n}$$ 이 연쇄적으로 존재**한다면, $$\overrightarrow{q}$$ 는 **$$\overrightarrow{p}$$ 로부터 밀도 기준 도달 가능한(Density-Reachable)** 관측치 벡터임

    - $$\vert N_{\varepsilon}(\overrightarrow{p})\vert \ge \text{MinPts}$$ : Core Point Condition
    - $$\overrightarrow{x}_{1} \in N_{\varepsilon}(\overrightarrow{p})$$ : Reachability
    - $$\vert N_{\varepsilon}(\overrightarrow{x}_{\forall})\vert \ge \text{MinPts}$$ : $$\overrightarrow{x}_{\forall}$$ 의 이웃 벡터 갯수가 하한선 $\text{MinPts}$ 이상임
    - $$\overrightarrow{x}_{i+1} \in N_{\varepsilon}(\overrightarrow{x}_{i})$$ : $$\overrightarrow{x}_{i+1}$$ 는 $$\overrightarrow{x}_{i}$$ 의 이웃 벡터임
    - $$\overrightarrow{q} \in N_{\varepsilon}(\overrightarrow{x}_{n})$$ : $\overrightarrow{q}$ 는 $\overrightarrow{x}_{n}$ 의 이웃 벡터임

- **Density-Connected**

    ![06](/_post_refer_img/MachineLearning/14-06.jpeg){: width="100%"}

    > **Core Point Condition** 을 만족하는 관측치 벡터 $$\overrightarrow{p},\overrightarrow{q} \in D$$ 에 대하여, **$$\overrightarrow{p}$$ 로부터 밀도 기준 도달 가능한(Density-Connected) 동시에 $$\overrightarrow{q}$$ 로부터 밀도 기준 도달 가능한(Density-Connected)** 관측치 벡터 $$\overrightarrow{x} \in D$$ 가 적어도 하나 존재한다면, **$$\overrightarrow{p},\overrightarrow{q}$$ 는 밀도 기준 연결되어 있음(Density-Connected)**

    - $\vert N_{\varepsilon}(\overrightarrow{p})\vert \ge \text{MinPts}$
    - $\overrightarrow{x} \in N_{\varepsilon}(\overrightarrow{p})$
    - $\vert N_{\varepsilon}(\overrightarrow{q})\vert \ge \text{MinPts}$
    - $\overrightarrow{x} \in N_{\varepsilon}(\overrightarrow{q})$

## Hierarchical Clustering
-----

### What? Hierarchical Clustering

- **정의** : 계층적 트리모형을 활용하여 개별 개체들을 유사한 개체/군집과 계층적으로 통합하거나, 표본을 유의미하게 구분되는 지점에서 계층적으로 분할해가는 알고리즘

- **덴드로그램(Dendrogram)** : 결합 혹은 분할하는 순서를 나타내는 계층적 트리모형

    ![01](/_post_refer_img/MachineLearning/15-01.png){: width="100%"}

- **종류**

    ![02](/_post_refer_img/MachineLearning/15-02.png){: width="100%"}

    - **상향식 군집화(Agglomerative Clustering)** : 개별 개체들을 유사한 개체/군집과 계층적으로 통합해가는 방식
    - **하향식 군집화(Divisive Clustering)** : 표본을 유의미하게 구분되는 지점마다 계층적으로 분할해가는 방식

### How to Agglomerative Clustering

1. 모든 개체를 개별 군집으로서 정의함

    $$
    C_{i} = \{\overrightarrow{x}_{i}\} \quad \text{for} \quad i=1,2,\cdots, n
    $$

2. 군집 간 거리 행렬을 계산함

    $$
    \mathbf{D}_{i,j}=d(C_{i},C_{j})
    $$

3. 가장 가까운 두 개의 군집을 하나의 군집으로 통합함

    $$\begin{aligned}
    C_{k}&=\hat{C}_{i} \cup \hat{C}_{j}\\
    \hat{C}_{i},\hat{C}_{j}&=\text{arg} \min_{C_{i},C_{j}}{d(C_{i},C_{j})}
    \end{aligned}$$

4. 군집 간 거리 행렬을 갱신함

    $$
    \mathbf{D}_{N} = \mathbf{D}_{N-1} \quad \text{Recalculate} \quad d(C_{i^{\forall} \ne k},C_{k})
    $$

5. 모든 개체가 하나의 군집으로 통합될 때까지 ③, ④의 과정을 반복함

### How to Calculate Distance

- **Single Linkage(Minimum Distance)** : 각 군집에 속한 개체들 사이 거리 최소값

    $$\begin{aligned}
    d(\mathbf{A},\mathbf{B})
    &= \min_{\overrightarrow{a} \in \mathbf{A},\overrightarrow{b} \in \mathbf{B}}{d(\overrightarrow{a},\overrightarrow{b})}
    \end{aligned}$$

- **Complete Linkage(Maximum Distance)** : 각 군집에 속한 개체들 사이 거리 최대값

    $$\begin{aligned}
    d(\mathbf{A},\mathbf{B})
    &= \max_{\overrightarrow{a} \in \mathbf{A},\overrightarrow{b} \in \mathbf{B}}{d(\overrightarrow{a},\overrightarrow{b})}
    \end{aligned}$$

- **Average Linkage(Mean Distance)** : 각 군집에 속한 개체들 사이 거리 평균

    $$\begin{aligned}
    d(\mathbf{A},\mathbf{B})
    &= \sum_{\overrightarrow{a} \in \mathbf{A}}\sum_{\overrightarrow{b} \in \mathbf{B}}{d(\overrightarrow{a},\overrightarrow{b})}
    \end{aligned}$$

- **Centroid Linkage(Distance Between Centroids)** : 각 군집 중심 간 거리

    $$\begin{aligned}
    d(\mathbf{A},\mathbf{B})
    &= d(\overrightarrow{\mu}_{A},\overrightarrow{\mu}_{B})\\
    \overrightarrow{\mu}_{A}
    &= \frac{1}{|\mathbf{A}|}\sum_{\overrightarrow{a} \in \mathbf{A}}{\overrightarrow{a}}\\
    \overrightarrow{\mu}_{B}
    &= \frac{1}{|\mathbf{B}|}\sum_{\overrightarrow{b} \in \mathbf{B}}{\overrightarrow{b}}
    \end{aligned}$$

- **Ward's Method** : 병합 후 SSE와 병합 전 개별 군집의 SSE의 합의 차

    $$\begin{aligned}
    d(\mathbf{A},\mathbf{B})
    &= \sum_{\overrightarrow{c} \in \mathbf{C}}{d(\overrightarrow{c},\overrightarrow{\mu}_{C})} - \Big[\sum_{\overrightarrow{a} \in \mathbf{A}}{d(\overrightarrow{a},\overrightarrow{\mu}_{A})} + \sum_{\overrightarrow{b} \in \mathbf{B}}{d(\overrightarrow{b},\overrightarrow{\mu}_{B})}\Big]\\
    \mathbf{C}
    &= \mathbf{A} \cup \mathbf{B}
    \end{aligned}$$

-----

### 이미지 출처

- https://www.scaler.com/topics/supervised-and-unsupervised-learning/
- https://towardsdatascience.com/a-brief-introduction-to-unsupervised-learning-20db46445283
- https://tyami.github.io/machine%20learning/clustering/
- https://ai-times.tistory.com/158
- https://github.com/pilsung-kang/multivariate-data-analysis/blob/master/09%20Clustering/09-2_K-Means%20Clustering.pdf
- https://github.com/lovit/python_ml_intro/blob/master/lecture_notes/10_clustering.pdf
- https://paulvanderlaken.com/2018/12/12/visualizing-the-inner-workings-of-the-k-means-clustering-algorithm/
- https://ai.plainenglish.io/dbscan-density-based-clustering-aaebd76e2c8c
- https://journals.sagepub.com/doi/10.1177/1748301817735665
- https://towardsdatascience.com/hierarchical-clustering-explained-e59b13846da8
- https://harshsharma1091996.medium.com/hierarchical-clustering-996745fe656b
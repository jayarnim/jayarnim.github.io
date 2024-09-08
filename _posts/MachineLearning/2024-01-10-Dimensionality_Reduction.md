---
order: 10
title: Dimensionality Reduction
date: 2024-01-10
categories: [Machine Learning Techs, Machine Learning]
tags: [Machine Learning, Unsupervised Learning, Feature Engineering]
math: true
description: >-
  Based on the lecture “Intro. to Machine Learning (2023-2)” by Prof. Je Hyuk Lee, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
  path: /_post_refer_img/MachineLearning/Thumbnail.jpg
---

## Curse of Dimensionality
-----

### Curse of Dimensionality

- **정의** : 고차원일수록 알고리즘이 제대로 학습하지 못하는 현상

    ![01](/_post_refer_img/MachineLearning/09-01.png){: width="100%"}

    - 관측치 간 거리가 기하급수적으로 멀어짐에 따라 차원별 학습 가능한 관측치가 희소해짐

- **차원 축소의 당위성**

    ![02](/_post_refer_img/MachineLearning/09-02.jpeg){: width="100%"}

    > #### Manifold hypothesis
    > Many high-dimensional data sets that occur in the real world actually lie along low-dimensional latent manifolds inside that high-dimensional space.

### Dimensionality Reduction Methods

- **차원 선택(Feature Selection)** : 유효한 차원을 선별하는 방법
    - **Filter Approach**

    - **Wrapper Approach**
        - Forward Selection
        - Backward Elimination
        - Stepwise Selection

- **차원 추출(Feature Extraction)** : 원본의 특징을 보존하는 새로운 차원을 추출하는 방법
    - $\text{arg} \max_{\overrightarrow{w}}{\sigma^{2}}$
        - 주성분 분석(`P`rinciple `C`omponent `A`nalysis; PCA)
        - 선형 판별 분석(`L`inear `D`iscriminant `A`nalysis; LDA)

    - $\text{arg} \max_{\overrightarrow{w}}{dist}$
        - 다차원 척도법(`M`ulti-`D`imensional `S`caling; MDS)

    - **Reveal Non-Linear Structure**
        - t-SNE(`t`-distributed `S`tochastic `N`eighbor `E`mbedding)
        - LLE(`L`ocally `L`inear `E`mbedding)
        - ISOMAP(`ISO`metric feature `MAP`ping)

## PCA
-----

### Principal Component Analysis

- **정의** : 고차원 데이터에 대하여, X의 방향적 분포를 가장 잘 설명하는 **새로운 저차원 직교 좌표**를 학습하는 기법

    ![04](/_post_refer_img/MachineLearning/10-04.jpeg){: width="100%"}

    - **주성분(Principal Component; PC)** : 새로운 저차원 직교 좌표

- **방법** : **관측치 간 상대적 특성**을 잘 보존하는 성분들을 추출함

    ![05](/_post_refer_img/MachineLearning/10-05.png){: width="100%"}

    - $\text{component}$ : 주성분 벡터 $\overrightarrow{w}$
    - $\text{datapoint}$ : 관측치 벡터 $\overrightarrow{x}\in \mathbf{X}$
    - $\text{projected data}$ : 주성분 벡터에 대한 관측치 벡터의 정사영 벡터 $\text{proj}_{\overrightarrow{w}}(\overrightarrow{x})$
    - $D_{1}$ : 관측치 벡터에 대하여 보존하는 정보로서 **분산**
    - $D_{2}$ : 관측치 벡터에 대하여 유실하는 정보
    - $D_{3}$ : 관측치 벡터의 본래 정보

### How to Extract

![06](/_post_refer_img/MachineLearning/10-06.png){: width="100%"}

- 관측치 행렬 $X_{N \times P}$ 를 단위벡터 $\overrightarrow{w}$ 에 정사영한다고 하자

    $$\begin{aligned}
    proj_{\overrightarrow{w}}(\mathbf{X})
    &= \frac{<\mathbf{X},\overrightarrow{w}>}{\Vert w \Vert ^2}\cdot\overrightarrow{w}\\
    &= (\overrightarrow{w}^{T}\mathbf{X})\cdot\overrightarrow{w} \quad (\because \Vert w \Vert=1)
    \end{aligned}$$

    - $\overrightarrow{w}$ : 정사영 벡터의 방향
    - $\overrightarrow{w}^{T}\mathbf{X}$ : 정사영 벡터의 크기

- $\overrightarrow{w}$ 에 정사영된 관측치들의 분산 $\mathbf{V}$ 은 다음과 같음

    $$\begin{aligned}
    \mathbf{V}
    &= \frac{1}{n}(\overrightarrow{w}^{T}\mathbf{X})(\overrightarrow{w}^{T}\mathbf{X})^{T}\\
    &= \frac{1}{n}(\overrightarrow{w}^{T}\mathbf{X}\mathbf{X}^{T}\overrightarrow{w})\\
    &= \overrightarrow{w}^{T}\Sigma\overrightarrow{w}
    \end{aligned}$$

    - $\Sigma=\displaystyle\frac{1}{n}\mathbf{X}\mathbf{X}^{T}$ : 관측치 행렬 $X$ 의 공분산 행렬

- $\mathbf{V}$ 을 최대화하는 $\overrightarrow{w}$ 를 채택한다고 하자

    $$
    \hat{\overrightarrow{w}}
    = \text{arg} \max_{\overrightarrow{w}}{\overrightarrow{w}^{T}\Sigma\overrightarrow{w}}
    \quad \text{s.t.} \quad
    \overrightarrow{w}^{T}\overrightarrow{w}=1
    $$

- 라그랑주 승수법에 기초하여 $\hat{\overrightarrow{w}}$ 도출

    $$\begin{aligned}
    L(\overrightarrow{w},\lambda)
    &= \overrightarrow{w}^{T}\Sigma\overrightarrow{w}-\lambda(\overrightarrow{w}^{T}\overrightarrow{w}-1)\\
    \frac{\partial L(\overrightarrow{w},\lambda)}{\overrightarrow{w}}
    &= 0\\
    \therefore (\Sigma-\lambda\mathbf{I})\hat{\overrightarrow{w}}
    &=0
    \end{aligned}$$

- $\mathbf{V}$ 를 최대화하는 주성분 $\overrightarrow{w}$ 은 $\mathbf{X}$ 의 공분산 행렬 $\Sigma$ 의 고유벡터임

    $$\begin{aligned}
    \Sigma
    &= \mathbb{V}\mathbb{\Lambda}\mathbb{V}^{-1},\\
    \mathbb{V}
    &= \begin{pmatrix}\overrightarrow{w}_{1}&\overrightarrow{w}_{2}&\cdots&\overrightarrow{w}_{p}\end{pmatrix}\\
    \mathbb{\Lambda}
    &= \text{diag}(\lambda_{1},\lambda_{2},\cdots,\lambda_{p})
    \end{aligned}$$

### Explanatory Power

- **주성분 벡터의 고유값** : 관측치 행렬 $\mathbf{X}$ 에 대하여 **주성분 벡터에 대한 정사영 벡터 간 분산**

    $$\begin{aligned}
    \mathbf{V}
    &= \frac{1}{n}(\overrightarrow{w}^{T}\mathbf{X})(\overrightarrow{w}^{T}\mathbf{X})^{T}\\
    &= \frac{1}{n}\overrightarrow{w}^{T}\mathbf{X}\mathbf{X}^{T}\overrightarrow{w}\\
    &= \overrightarrow{w}^{T}\Sigma\overrightarrow{w}\\
    &= \hat{\overrightarrow{w}}^{T}\lambda\hat{\overrightarrow{w}} \quad (\because \Sigma\hat{\overrightarrow{w}}-\lambda\hat{\overrightarrow{w}}=0)\\
    &= \lambda \quad (\because \overrightarrow{w}^{T}\overrightarrow{w}=1)
    \end{aligned}$$

- **주성분 벡터의 설명력** : 관측치 행렬 $\mathbf{X}_{N \times P}$ 에 대하여 생성 가능한 $P$ 개의 주성분 벡터 고유값 합계 대비 해당 주성분 벡터 고유값 비율

    $$
    \frac{\lambda_{k}}{\sum_{i=1}^{p}{\lambda_{i}}}
    $$

## LDA; PCA for Classification
-----

### Linear Discriminant Analysis

- **정의** : 고차원 데이터에 대하여, **주어진 클래스를 가장 잘 구분할 수 있는** 새로운 저차원 직교 좌표(선형 판별 함수)를 찾는 기법

    ![07](/_post_refer_img/MachineLearning/10-07.png){: width="100%"}

- **방법** : **클래스 간 분산은 최대화**하는 동시에 **클래스 내 관측치 간 분산은 최소화**하는 성분들을 추출함

    $$
    \hat{\overrightarrow{w}}
    =\text{arg} \max_{\overrightarrow{w}}{\frac{\Sigma^{2}}{\sigma_{1}^{2}+\sigma_{2}^{2}}}
    \quad \text{s.t.} \quad
    \overrightarrow{w}^{T}\overrightarrow{w}=1
    $$

    - $\Sigma^{2}$ : 정사영 후 클래스 간 분산
    - $\sigma_{i}^{2}$ : 정사영 후 $i$ 번째 클래스 내 관측치 간 분산

### How to Extract

- **정사영 후 범주 간 분산 $\Sigma^{2}$**

    $$\begin{aligned}
    \Sigma^{2}
    &= (\overrightarrow{\mu}_{1}-\overrightarrow{\mu}_{2})(\overrightarrow{\mu}_{1}-\overrightarrow{\mu}_{2})^{T}\\
    &= (\overrightarrow{w}^{T}\overrightarrow{m}_{1}-\overrightarrow{w}^{T}\overrightarrow{m}_{2})(\overrightarrow{w}^{T}\overrightarrow{m}_{1}-\overrightarrow{w}^{T}\overrightarrow{m}_{2})^{T}\quad(\because \overrightarrow{\mu}_{i}=\overrightarrow{w}^{T}\overrightarrow{m}_{i})\\
    &= \overrightarrow{w}^{T}(\overrightarrow{m}_{1}-\overrightarrow{m}_{2})(\overrightarrow{m}_{1}-\overrightarrow{m}_{2})^{T}\overrightarrow{w}\\
    &= \overrightarrow{w}^{T}\mathbf{S}_{B}\overrightarrow{w}
    \end{aligned}$$

    - $$\overrightarrow{m}_{i}$$ : $$i$$ 번째 범주 $$C_{i}$$ 의 중심점 벡터
    - $$\overrightarrow{\mu}_{i}=\text{proj}_{\overrightarrow{w}}(\overrightarrow{m}_{i})$$ : $$\overrightarrow{m}_{i}$$ 의 정사영 벡터
    - $$\mathbf{S}_{B}$$ : 범주 $$C_{i},C_{j}$$ 간 편차
    - $$\Sigma$$ : 정사영 후 범주 $$C_{i},C_{j}$$ 간 편차

- **정사영 후 범주 내 분산 $\sigma_{i}^{2}$**

    $$\begin{aligned}
    \sigma_{i}^{2}
    &= \sum_{j=1}^{|C_{i}|}{(\overrightarrow{y}_{j}-\overrightarrow{\mu}_{i})(\overrightarrow{y}_{j}-\overrightarrow{\mu}_{i})^{T}}\quad(\overrightarrow{x}_{j} \in C_{i})\\
    &= \sum_{j=1}^{|C_{i}|}{(\overrightarrow{w}^{T}\overrightarrow{x}_{j}-\overrightarrow{w}^{T}\overrightarrow{m}_{i})(\overrightarrow{w}^{T}\overrightarrow{x}_{j}-\overrightarrow{w}^{T}\overrightarrow{m}_{i})^{T}}\quad(\because \overrightarrow{y}_{j}=\overrightarrow{w}^{T}\overrightarrow{x}_{j})\\
    &= \overrightarrow{w}^{T}\left[\sum_{j=1}^{|C_{i}|}{(\overrightarrow{x}_{j}-\overrightarrow{m}_{i})(\overrightarrow{x}_{j}-\overrightarrow{m}_{i})^{T}}\right]\overrightarrow{w}\\
    &= \overrightarrow{w}^{T}\mathbf{S}_{i}\overrightarrow{w}
    \end{aligned}$$

    - $$\overrightarrow{x}_{j} \in C_{i}$$ : $$i$$ 번째 범주 $$C_{i}$$ 의 $$j$$ 번째 관측치 벡터
    - $$\overrightarrow{y}_{j}=\text{proj}_{\overrightarrow{w}}(\overrightarrow{x}_{j})$$ : $$\overrightarrow{x}_{j}$$ 의 정사영 벡터
    - $$S_{i}$$ : $$i$$ 번째 범주 $$C_{i}$$ 의 범주 내 관측치 간 편차
    - $$\sigma_{i}$$ : 정사영 후 $$i$$ 번째 범주 $$C_{i}$$ 의 범주 내 관측치 간 편차

- **목적 함수 재정의**

    $$\begin{aligned}
    \hat{\overrightarrow{w}}
    =\text{arg} \max_{\overrightarrow{w}}{\frac{\overrightarrow{w}^{T}\mathbf{S}_{B}\overrightarrow{w}}{\overrightarrow{w}^{T}(\mathbf{S}_{1}+\mathbf{S}_{2})\overrightarrow{w}}}
    \quad \text{s.t.} \quad
     \overrightarrow{w}^{T}\overrightarrow{w}=1
    \end{aligned}$$

- **라그랑주 승수법을 통한 최적화 문제 풀이**

    $$\begin{aligned}
    L(\overrightarrow{w},\lambda)
    &= \frac{\overrightarrow{w}^{T}\mathbf{S}_{B}\overrightarrow{w}}{\overrightarrow{w}^{T}(\mathbf{S}_{1}+\mathbf{S}_{2})\overrightarrow{w}}-\lambda(\overrightarrow{w}^{T}\overrightarrow{w}-1)\\
    \frac{\partial L(\overrightarrow{w},\lambda)}{\partial \overrightarrow{w}}
    &= 0\\
    \therefore \left[\mathbf{S}_{B}^{-1}(\mathbf{S}_{1}+\mathbf{S}_{2})-\lambda\mathbf{I}\right]\hat{\overrightarrow{w}}
    &=0
    \end{aligned}$$

## t-SNE
-----

### What? t-SNE

- **`S`tochastic `N`eighbor `E`mbedding** : 관측치 간 고차원 공간 상 확률적 유사도를 보존하면서 저차원으로 매핑하는 비선형 차원 축소

    ![01](/_post_refer_img/MachineLearning/11-01.jpeg){: width="100%"}

- **SNE의 문제점** : Crowding Problem

    ![02](/_post_refer_img/MachineLearning/11-02.png){: width="100%"}

    - 가우시안 분포는 양쪽 꼬리 부분이 충분히 두텁지 않은 형태를 보임
    - 즉, 확률변수 $$\Vert \overrightarrow{x}_{i}-\overrightarrow{x}_{j} \Vert$$ 가 일정한 값 이상부터는 유사도에 큰 차이가 없음

- **t-SNE의 해결책** : Student t-Dristribution

    ![03](/_post_refer_img/MachineLearning/11-03.jpg){: width="100%"}

    $$\begin{aligned}
    T
    &= \frac{Z}{\sqrt{\displaystyle\frac{V}{\nu}}}\\
    V
    &= \sum_{i=1}^{k}{Z_{i}^{2}}
    \end{aligned}$$

    - $Z$ : 표준 가우시안 분포
    - $V$ : 자유도가 $\nu$ 인 카이제곱 분포

### How to Extract

- **두 관측치의 고차원 공간 상 유사도 도출**

    - 확률변수 $X$ 가 가우시안 분포 $N(\mu, \sigma^{2})$ 을 따른다고 했을 때, $X$ 의 확률밀도함수는 다음과 같음

        $$\begin{aligned}
        f(x)
        &= \frac{1}{\sqrt{2\pi\sigma^{2}}}\exp{\left[-\frac{(x-\mu)^{2}}{2\sigma^{2}}\right]}
        \end{aligned}$$

    - **관측치 $$\overrightarrow{x}_{i}$$ 로부터의 거리에 대한 $$\overrightarrow{x}_{i}$$ 와의 유사도**의 가우시안 분포에 기초했을 때, $$\overrightarrow{x}_{j}$$ 가 $$\overrightarrow{x}_{i}$$ 와 유사할 가능성을 다음과 같이 정의하자

        $$\begin{aligned}
        p_{j \mid i} 
        &= \frac{\exp{\left[-\frac{\Vert\overrightarrow{x}_{i}-\overrightarrow{x}_{j}\Vert^{2}}{2\sigma^{2}}\right]}}{\sum_{k \ne i}{\exp{\left[-\frac{\Vert\overrightarrow{x}_{i}-\overrightarrow{x}_{k}\Vert^{2}}{2\sigma^{2}}\right]}}}\\
        \Vert\overrightarrow{x}_{i}-\overrightarrow{x}_{j}\Vert &\sim N_{i}(0,\sigma^{2})
        \end{aligned}$$

    - **또한 관측치 $$\overrightarrow{x}_{j}$$ 로부터의 거리에 대한 $$\overrightarrow{x}_{j}$$ 와의 유사도**의 가우시안 분포에 기초했을 때, $$\overrightarrow{x}_{i}$$ 가 $$\overrightarrow{x}_{j}$$ 와 유사할 가능성을 다음과 같이 정의하자

        $$\begin{aligned}
        p_{i|j}
        &= \frac{\exp{\left[-\frac{\vert\overrightarrow{x}_{i}-\overrightarrow{x}_{j}\vert^{2}}{2\sigma^{2}}\right]}}{\sum_{k \ne j}{\exp{\left[-\frac{\vert\overrightarrow{x}_{j}-\overrightarrow{x}_{k}\vert^{2}}{2\sigma^{2}}\right]}}}\\
        \Vert\overrightarrow{x}_{i}-\overrightarrow{x}_{j}\Vert
        &\sim N_{j}(0,\sigma^{2})
        \end{aligned}$$

    - 두 가능성은 **서로 다른 확률 분포에 기초하고 있으므로** 그 값이 반드시 일치한다고 볼 수 없음

        $$
        p_{j \mid i} \ne p_{i \mid j}
        $$

    - 따라서 $$\overrightarrow{x}_{i}$$ 와 $$\overrightarrow{x}_{j}$$ 의 유사도를 다음과 같이 정의함

        $$\begin{aligned}
        p_{i,j}
        &= \frac{p_{j \mid i} + p_{i \mid j}}{2n}
        \end{aligned}$$

- **두 관측치의 2차원 공간 상 유사도 도출**

    - **관측치 $$\overrightarrow{y}_{i}$$ 로부터의 거리에 대한 $$\overrightarrow{y}_{i}$$ 와의 유사도**의 가우시안 분포에 기초했을 때, $$\overrightarrow{y}_{j}$$ 가 $$\overrightarrow{y}_{i}$$ 와 유사할 가능성을 다음과 같이 정의하자

        $$\begin{aligned}
        q_{j \mid i} 
        &= \frac{\exp{\left[-\Vert\overrightarrow{y}_{i}-\overrightarrow{y}_{j}\Vert^{2}\right]}}{\sum_{k \ne i}{\exp{\left[-\Vert\overrightarrow{y}_{i}-\overrightarrow{y}_{k}\Vert^{2}\right]}}}\\
        \Vert\overrightarrow{y}_{i}-\overrightarrow{y}_{j}\Vert 
        &\sim N_{i}(0,\sigma^{2})
        \end{aligned}$$

        - $$\overrightarrow{y}$$ : 고차원 공간 상의 관측치 벡터 $$\overrightarrow{x}$$ 를 2차원 공간 상에 매핑한 벡터

    - $$\overrightarrow{y}_{i}$$ 와 $$\overrightarrow{y}_{j}$$ 의 유사도를 다음과 같이 정의함

        $$\begin{aligned}
        q_{i,j}
        &= \frac{q_{j \mid i} + q_{i \mid j}}{2n}
        \end{aligned}$$

- **비용 함수를 최소화하는 아규먼트 도출**

    - **KL(Kullback-Leibler Divergence)** : 확률변수 $X$ 의 동일한 아규먼트 $x_{i}$ 에 대하여 두 확률 분포 $P,Q$ 의 차이를 측정하는 지표

        $$
        \text{KL}(P \mid Q)
        = \sum_{i=1}^{n}{P(X=x_{i})\cdot\log{\frac{P(X=x_{i})}{Q(X=x_{i})}}}
        $$

    - KL에 기초한 비용함수 정의

        $$\begin{aligned}
        Cost
        &= \sum_{i}{\text{KL}(P_{i} \mid Q_{i})}\\
        &= \sum_{i}{\sum_{j}{p_{i,j}\cdot\log{\frac{p_{i,j}}{q_{i,j}}}}}
        \end{aligned}$$

    - $\hat{\mathbf{Y}}$ 도출

        $$\begin{aligned}
        \hat{\mathbf{Y}}
        &= \{\hat{\overrightarrow{y}}_{i} \mid \text{arg} \min_{\overrightarrow{y}_{i}}{Cost}\}
        \end{aligned}$$

### 이미지 출처

- http://alexhwilliams.info/itsneuronalblog/2016/03/27/pca/
- http://matrix.skku.ac.kr/math4ai-intro/W12/
- https://www.incodom.kr/%EC%B0%A8%EC%9B%90%EC%B6%95%EC%86%8C#h_85f3fb207a586b3f9b5702a3be7799e1
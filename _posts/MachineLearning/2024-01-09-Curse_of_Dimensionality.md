---
order: 9
title: Curse of Dimensionality
date: 2024-01-09
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

### 차원의 저주

- **정의** : 고차원일수록 알고리즘이 제대로 학습하지 못하는 현상

    ![01](/_post_refer_img/MachineLearning/09-01.png){: width="100%"}

    - 관측치 간 거리가 기하급수적으로 멀어짐에 따라 차원별 학습 가능한 관측치가 희소해짐

- **차원 축소의 당위성**

    ![02](/_post_refer_img/MachineLearning/09-02.jpeg){: width="100%"}

    > #### Manifold hypothesis
    > Many high-dimensional data sets that occur in the real world actually lie along low-dimensional latent manifolds inside that high-dimensional space.

### 차원 축소 기법의 종류

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

## Feature Selection
-----

> #### Occam's Razor
> Entities should not be multiplied beyond necessity.

### Wrapper Approach

- **Forward Selection** : 어떤 변수도 선택되지 않은 상태에서 가장 설명력이 좋은 변수를 하나씩 추가하는 방법

    $$
    \begin{aligned}
    \hat{x}_{i}&=\text{arg} \max_{x_{i}}R^2[y,f(x_{i})]\\
    \hat{x}_{j}&=\text{arg} \max_{x_{j}}R^2[y,f(x_{j \ne i};\hat{x}_{i})]\\
    \hat{x}_{k}&=\text{arg} \max_{x_{k}}R^2[y,f(x_{k \ne i,j};\hat{x}_{i},\hat{x}_{j})]\\
    &\vdots
    \end{aligned}
    $$

- **Backward Elimination** : 모든 변수가 포함된 상태에서 시작하여 불필요한 변수를 하나씩 제거하는 방법

    $$\begin{aligned}
    \hat{x}_{i}&=\text{arg} \max_{x_{i}}R^2[y,f(\not{x_{i}})]\\
    \hat{x}_{j}&=\text{arg} \max_{x_{j}}R^2[y,f(\not{x_{j \ne i}};\not{\hat{x}_{i}})]\\
    \hat{x}_{k}&=\text{arg} \max_{x_{k}}R^2[y,f(\not{x_{k \ne i,j}};\not{\hat{x}_{i}},\not{\hat{x}_{j}})]\\
    &\vdots
    \end{aligned}$$

- **Stepwise Selection** : 어떤 변수도 선택되지 않은 상태에서 Forward Selection 과 Backward Elimination 을 번갈아 수행하는 방법

### Metrics

- **Akaike Information Criteria(AIC)**

    $$\begin{aligned}
    \text{AIC}
    &= -2\ln{\hat{L}}+2k
    \end{aligned}$$

    - $\hat{L}$ : 모델 적합도로서 $$\overrightarrow{x}_{i}$$ 가 주어졌을 때 $y_{i}$ 가 발생할 가능성

        $$\begin{aligned}
        \hat{L}
        &= \prod_{i=1}^{n}{P(Y=y_{i}|X=\overrightarrow{x}_{i};\hat{\overrightarrow{\theta}})}\\
        \hat{\overrightarrow{\theta}}
        &= \begin{pmatrix}\hat{\beta_{0}}&\hat{\beta_{1}}&\cdots&\hat{\beta_{d}}\end{pmatrix}
        \end{aligned}$$

    - $k$ : 모델 복잡도

- **Bayesian Information Criteria(BIC)**

    $$\begin{aligned}
    \text{BIC}
    &= -2\ln{\hat{L}}+k\ln{n}
    \end{aligned}$$

-----

### 이미지 출처

- https://www.incodom.kr/%EC%B0%A8%EC%9B%90%EC%B6%95%EC%86%8C#h_85f3fb207a586b3f9b5702a3be7799e1
- http://matrix.skku.ac.kr/math4ai-intro/W12/
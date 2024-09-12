---
order: 11
title: Dimensionality Reduction
date: 2024-01-11
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

- **정의** : 고차원일수록 알고리즘이 제대로 학습하지 못하는 현상

    ![01](/_post_refer_img/MachineLearning/11-01.png){: width="100%"}

    - 관측치 간 거리가 기하급수적으로 멀어짐에 따라 차원별 학습 가능한 관측치가 희소해짐

- **차원 축소의 당위성**

    ![02](/_post_refer_img/MachineLearning/11-02.jpeg){: width="100%"}

    > #### Manifold hypothesis
    > Many high-dimensional data sets that occur in the real world actually lie along low-dimensional latent manifolds inside that high-dimensional space.

## Dimensionality Reduction Methods
-----

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
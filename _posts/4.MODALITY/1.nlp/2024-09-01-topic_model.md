---
order: 7
title: Topic Model
date: 2024-09-01
categories: [4.MODALITY, 1.netural language processing]
tags: [modality, nlp, topic model, matrix decomposition, latent factor, dirichlet distribution]
math: true
description: >-
    Based on the lecture “Text Analytics (2024-1)” by Prof. Je Hyuk Lee, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
    path: /_post_refer_img/4.MODALITY/1.nlp/Thumbnail.png
---

## Topic Model
-----

- **토픽 모형(Topic Model)** : 관측 가능한 단어(Word) 및 문서(Document)로부터 말뭉치(Corpus)에 내재되어 있는(Latent) 토픽(Topic)을 탐색하는 방법
    - 문서(Document)는 토픽(Topic)으로 어떻게 표현할 수 있을까?
    - 단어(Word)는 토픽(Topic) 별로 어떻게 등장하는가?
    - 탐색된 Something(Topic)의 정체를 무엇이라 정의하면 좋을까?

## LSA
-----

- **잠재 의미 분석(Latent Semantic Analysis; LSA)** : 특이값 분해(Singular Value Decomposition; SVD)를 활용하여 Document-Term Matrix 를 분해하는 방법

    $$
    \mathbf{A} \approx \mathbf{U} \cdot \Sigma \cdot \mathbf{V}^{T}
    $$

    | Dimension | Interpretation | |
    |---|---|---|
    | $n$ | Number of Document | |
    | $d$ | Number of Term | |
    | $k$ | Number of Topic | Hyper-Parameter |

    - $\mathbf{A} \in \mathbb{R}^{n \times d}$ : Document-Term Matrix
    - $$\mathbf{U} \cdot \Sigma$$ : Document-Topic Matrix
        - $\mathbf{U} \in \mathbb{R}^{n \times k}$
        - $\Sigma \in \mathbb{R}^{k \times k}$
    - $\Sigma \cdot \mathbb{V}^{T}$ : Term-Topic Matrix
        - $\mathbf{V} \in \mathbb{R}^{d \times k}$
        - $\Sigma \in \mathbb{R}^{k \times k}$

### SVD

- **특이값 분해(Singular Value Decomposition; SVD)** : 차원의 크기가 $n \times d$ 인 임의의 행렬 $\mathbb{A}$ 를 세 개의 행렬의 곱으로 분해하는 방법

    ![04](/_post_refer_img/4.MODALITY/1.nlp/07-01.png){: width="100%"}

- **$$\mathbf{U} \in \mathbb{R}^{n \times k}$$ : 직교 정규 행렬(Ortho-normal Matrix)**
    - 열벡터 $\mathbf{u}_{i} \in \mathbf{U}$ 는 행렬 $\mathbf{A} \cdot \mathbf{A}^{T}$ 의 고유벡터(Eigen Vector)임

        $$
        \mathbf{A}\mathbf{A}^{T} \cdot \mathbf{u}_{i} = \lambda_i \mathbf{u}_{i}
        $$

    - 열벡터 $\mathbf{u}_{i}$ 의 길이는 $1$ 임

        $$
        \Vert \mathbf{u}_{i} \Vert = 1
        $$

    - 열벡터 $$\mathbf{u}_{i}, \mathbf{u}_{j}$$ 은 직교함

        $$
        \mathbf{u}_{i} \perp \mathbf{u}_{j} \Leftrightarrow \langle \mathbf{u}_{i}, \mathbf{u}_{j} \rangle = 0
        $$

- **$\mathbf{V} \in \mathbb{R}^{d \times k}$ : 직교 정규 행렬(Ortho-normal Matrix)**
    - 열벡터 $\mathbf{v}_{i} \in \mathbf{V}$ 는 행렬 $\mathbf{A}^{T} \cdot \mathbf{A}$ 의 고유벡터(Eigen Vector)임

        $$
        \mathbf{A}^{T}\mathbf{A} \cdot \mathbf{v}_{i} = \lambda_{i} \mathbf{v}_{i}
        $$

    - 열벡터 $\mathbf{v}_{i}$ 의 길이는 $1$ 임

        $$
        \Vert \mathbf{v}_{i} \Vert = 1
        $$

    - 열벡터 $$\mathbf{v}_{i}, \mathbf{v}_{j}$$ 은 직교함

        $$
        \mathbf{v}_{i} \perp \mathbf{v}_{j} \Leftrightarrow \langle \mathbf{v}_{i}, \mathbf{v}_{j} \rangle = 0
        $$

- **$\Sigma \in \mathbb{R}^{k \times k}$ : 대각 행렬(Diagonal Matrix)**

    $$
    \Sigma
    = \begin{pmatrix}
    \sigma_{1} & 0 & \cdots & 0 \\
    0 & \sigma_{2} & \cdots & 0 \\
    \vdots & \vdots & \ddots & \vdots \\
    0 & 0 & \cdots & \sigma_{k}
    \end{pmatrix}
    $$

    - 대각항의 원소 $\sigma_{i}$ 는 행렬 $\mathbf{A} \cdot \mathbf{A}^{T}$ 혹은 $\mathbf{A}^{T} \cdot \mathbf{A}$ 의 고유값(Eigen Value) $\lambda_{i}$ 의 자승근임 

        $$
        \sigma_{i} = \sqrt{\lambda_i}
        $$

## LDA
-----

- **잠재 디리클레 할당(Latent Dirichlet Allocation; LDA)** : 베이지안 프레임워크를 활용하여 문서에 내재된 잠재적인 토픽 구조를 탐색하는 방법

    $$\begin{aligned}
    &\hat{\theta}, \hat{\psi}\\
    &=\text{arg} \max_{\theta, \psi}{\prod_{d=1}^{D}{\prod_{n=1}^{N_d}{P(\theta_d, \psi_{z(d,n)}; z(d,n) \mid w(d,n))}}}\\
    &\propto \text{arg} \max_{\theta, \psi}{\prod_{d=1}^{D}{\prod_{n=1}^{N_d}{P(\theta_d \mid z(d,n)) \times P(\psi_{z(d,n)} \mid w(d,n))}}}\\
    &\propto \text{arg} \max_{\theta, \psi}{\prod_{d=1}^{D}{\prod_{n=1}^{N_d}{\underbrace{P(\theta_d) \cdot P(z(d,n) \mid \theta_d)}_{\begin{array}{c} \text{Document-Topic} \\ \text{Allocation} \end{array}} \times \underbrace{P(\psi_{z(d,n)}) \cdot P(w(d,n) \mid \psi_{z(d,n)})}_{\begin{array}{c} \text{Topic-Word} \\ \text{Allocation} \end{array}}}}}
    \end{aligned}$$

    - $P(\theta_d \mid z(d,n)) \propto P(\theta_d) \cdot P(z(d,n) \mid \theta_d)$ : Posterior Probability of Document-Topic Allocation
    - $P(\psi_{z(d,n)} \mid w(d,n)) \propto P(\psi_{z(d,n)}) \cdot P(w(d,n) \mid \psi_{z(d,n)})$ : Posterior Probability of Topic-Word Allocation

### Posterior Probability

> 각 문서는 여러 토픽의 혼합으로 구성되어 있고, 각 토픽은 특정 단어들의 혼합으로 구성되어 있다고 가정하자. 특정 문서를 구성하고 있는 단어들로부터, 해당 단어들을 발생시킨 토픽들의 비중을 추론할 수 있음.

1. **문서 $d$ 에는 여러 토픽들이 담겨 있으며, 각 토픽 발생 확률은 디리클레 분포를 따름**

    $$\begin{aligned}
    k \mid \theta_d &\sim \text{Multinomial}(\theta_{d})\\
    \theta_{d} &\sim \text{Dirichlet}(\alpha)
    \end{aligned}$$

    - $k \mid \theta_d$ : 문서 $d$ 에서 토픽 $k$ 가 발생할 확률
    - $\theta_d$ : $d$ 번째 문서에서 각 토픽들이 발생할 확률

2. **토픽 $k$ 에서는 여러 단어들이 발생할 수 있으며, 각 단어 발생 확률은 디리클레 분포를 따름**

    $$\begin{aligned}
    w \mid \psi_{k} &\sim \text{Multinomial}(\psi_{k})\\
    \psi_{k} &\sim \text{Dirichlet}(\beta)
    \end{aligned}$$

    - $w \mid \psi_{k}$ : 토픽 $k$ 에서 단어 $w$ 가 발생할 확률
    - $\psi_{k}$ : 토픽 $k$ 에서 각 단어들이 발생할 확률

3. **따라서 단어 $w(d,n)$ 이 발생했을 때, $\theta_d$ 및 $\psi_{z(d,n)}$ 의 사후 확률 분포는 다음과 같음**

    $$\begin{aligned}
    &P(\theta_d, \psi_{z(d,n)}; z(d,n) \mid w(d,n))\\
    &\propto \underbrace{P(\theta_d \mid z(d,n))}_{\begin{array}{c} \text{Posterior of} \\ \text{Document-Topic} \\ \text{Allocation} \end{array}} \times \underbrace{P(\psi_{z(d,n)} \mid w(d,n))}_{\begin{array}{c} \text{Posterior of} \\ \text{Topic-Word} \\ \text{Allocation} \end{array}}\\
    &\propto \left[\underbrace{P(\theta_d)}_{\text{Prior}} \cdot \underbrace{P(z(d,n) \mid \theta_d)}_{\text{Likelihood}}\right] \times \left[\underbrace{P(\psi_{z(d,n)})}_{\text{Prior}} \cdot \underbrace{P(w(d,n) \mid \psi_{z(d,n)})}_{\text{Likelihood}}\right]
    \end{aligned}$$

    - $w(d,n)$ : 문서 $d$ 의 $n$ 번째 단어
    - $z(d,n)$ : 단어 $w(d,n)$ 에 대하여 해당 단어가 할당된 토픽
    - $\theta_d$ : 문서 $d$ 의 토픽 분포
    - $\psi_{z(d,n)}$ : 토픽 $z(d,n)$ 의 단어 분포

-----

## Sourse

- https://intoli.com/blog/pca-and-svd/
---
order: 6
title: Improvement of OLS
date: 2024-07-13
categories: [Statistical Techs, Regression Analysis]
tags: [Statistics, Regression]
math: true
description: >-
    Based on the following lectures <br>
    (1) “Statistics (2018-1)” by Prof. Sang Ah Lee, Dept. of Economics, College of Economics & Commerce, Kookmin Univ. <br>
    (2) “Intro. to Machine Learning (2023-2)” by Prof. Je Hyuk Lee, Dept. of Data Science, The Grad. School, Kookmin Univ. <br>
    (3) "Statistical Models and Application (2024-1)" by Prof. Yeo Jin Chung, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
    path: /_post_refer_img/RegressionAnalysis/Thumbnail.jpg
---

## Feature Selection
-----

> #### Occam's Razor
> Entities should not be multiplied beyond necessity.

### Wrapper Approach

- **전진 선택(Forward Selection)** : 어떤 변수도 선택되지 않은 상태에서 가장 설명력이 좋은 변수를 하나씩 추가하는 방법

    $$
    \begin{aligned}
    \hat{x}_{i}&=\text{arg} \max_{x_{i}}R^2[y,f(x_{i})]\\
    \hat{x}_{j}&=\text{arg} \max_{x_{j}}R^2[y,f(x_{j \ne i};\hat{x}_{i})]\\
    \hat{x}_{k}&=\text{arg} \max_{x_{k}}R^2[y,f(x_{k \ne i,j};\hat{x}_{i},\hat{x}_{j})]\\
    &\vdots
    \end{aligned}
    $$

- **후진 선택(Backward Elimination)** : 모든 변수가 포함된 상태에서 시작하여 불필요한 변수를 하나씩 제거하는 방법

    $$\begin{aligned}
    \hat{x}_{i}&=\text{arg} \max_{x_{i}}R^2[y,f(\not{x_{i}})]\\
    \hat{x}_{j}&=\text{arg} \max_{x_{j}}R^2[y,f(\not{x_{j \ne i}};\not{\hat{x}_{i}})]\\
    \hat{x}_{k}&=\text{arg} \max_{x_{k}}R^2[y,f(\not{x_{k \ne i,j}};\not{\hat{x}_{i}},\not{\hat{x}_{j}})]\\
    &\vdots
    \end{aligned}$$

- **혼합 선택(Stepwise Selection)** : 어떤 변수도 선택되지 않은 상태에서 Forward Selection 과 Backward Elimination 을 번갈아 수행하는 방법

### Metrics

- **Adjusted Coefficient of Determination($\text{Adj.}R^2$)**

    $$
    \text{Adj.}R^2 = \frac{(n-1)R^2-p}{n-p-1}
    $$

- **Akaike Information Criteria(AIC)**

    $$\begin{aligned}
    \text{AIC}
    &= -2\ln{\hat{L}}+2k
    \end{aligned}$$

    - $\hat{L}$ : 모델 적합도로서 $$\overrightarrow{x}_{i}$$ 가 주어졌을 때 $y_{i}$ 가 발생할 가능성

        $$\begin{aligned}
        \hat{L}
        &= \prod_{i=1}^{n}{P(Y=y_{i} \mid X=\overrightarrow{x}_{i};\hat{\overrightarrow{\theta}})}\\
        \hat{\overrightarrow{\theta}}
        &= \begin{pmatrix}\hat{\beta_{0}}&\hat{\beta_{1}}&\cdots&\hat{\beta_{d}}\end{pmatrix}
        \end{aligned}$$

    - $k$ : 모델 복잡도

- **Bayesian Information Criteria(BIC)**

    $$\begin{aligned}
    \text{BIC}
    &= -2\ln{\hat{L}}+k\ln{n}
    \end{aligned}$$

## Shrinkage Methods
-----

- **p-norm** : $n$ 차원 벡터 $\overrightarrow{x}=\begin{pmatrix}x_{1}&x_{2}&\cdots&x_{n}\end{pmatrix}$ 의 크기를 정의하는 방법

    ![03](/_post_refer_img/MachineLearning/08-03.png){: width="100%"}

    $$
    \Vert x \Vert _{p}=(\vert x_{1} \vert ^{p}+ \vert x_{2} \vert ^{p}+\cdots+ \vert x_{n} \vert ^{p})^{\frac{1}{p}}
    $$

- **가중치 규제(Weight Regulation)** : 회귀계수 최적값을 탐색함에 있어 회귀계수 벡터 $\overrightarrow{\beta}$ 의 크기에 제약을 두는 것

    ![04](/_post_refer_img/MachineLearning/08-04.png){: width="100%"}

    $$\begin{aligned}
    \overrightarrow{\hat{\beta}}
    &= \text{arg} \min_{\overrightarrow{\beta}}{\left[L_{OLS}+\lambda \Vert \beta \Vert _{p}^{2}\right]}
    \end{aligned}$$

    - $L_{OLS}(\overrightarrow{\beta})$ : 최소자승법에 기초한 손실 함수
    - $\overrightarrow{\beta}$ : 회귀계수 벡터
    - $\lambda$ : 회귀계수 벡터 $\overrightarrow{\beta}$ 크기 제약 강도
    - `p` : 벡터 크기 정의 방법
        - `p=1` : LASSO
        - `p=2` : Ridge

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
    &= \frac{<\mathbf{X},\overrightarrow{w}>}{||w||^2}\cdot\overrightarrow{w}\\
    &= (\overrightarrow{w}^{T}\mathbf{X})\cdot\overrightarrow{w} \quad (\because ||w||=1)
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
    &= \overrightarrow{w}^{T}\Sigma\overrightarrow{w}-\lambda(\overrightarrow{w}^{T}\overrightarrow{w}-1)\\\\
    \frac{\partial L(\overrightarrow{w},\lambda)}{\overrightarrow{w}}
    &= \Sigma\overrightarrow{w}-\lambda\overrightarrow{w}\\
    &= 0\\\\
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

## `refer.` Prerequisite for PCA
-----

### Projection

![01](/_post_refer_img/MachineLearning/10-01.png){: width="100%"}

> 벡터 $\overrightarrow{a}$ 를 벡터 $\overrightarrow{b}$ 에 정사영했을 때, 정사영 벡터 $\text{proj}_{\overrightarrow{b}}(\overrightarrow{a})$ 는 다음과 같음

$$\begin{aligned}
\cos{90^{\circ}}
&= \frac{(\overrightarrow{a}-p\overrightarrow{b})^{T}\overrightarrow{b}}{||\overrightarrow{a}||\cdot||\overrightarrow{b}||}\\
&= 0\\
\therefore \text{proj}_{\overrightarrow{b}}(\overrightarrow{a})
&= p\overrightarrow{b}\\
&= \left(\frac{\overrightarrow{a}^{T}\overrightarrow{b}}{||\overrightarrow{b}||^{2}}\right)\overrightarrow{b}
\end{aligned}$$

- $p=\displaystyle\frac{\overrightarrow{a}^{T}\overrightarrow{b}}{\Vert\overrightarrow{b}\Vert^{2}}$ : 정사영 벡터의 크기
- $\overrightarrow{b}$ : 정사영 벡터의 방향

### Covariance Matrix

- **공분산(Covariance)** : 두 확률변수의 선형관계를 나타내는 지표로서, 두 확률변수의 편차(관측치와 평균 사이 거리)를 곱한 값의 평균

    $$
    \sigma_{XY} = \frac{1}{N}\sum_{i=1}^{N}(X_{i}-\mu_X)(Y_{i}-\mu_Y)
    $$

- **공분산행렬(Covariance Matrix)** : $n$ 개 변수들 간 공분산을 나열한 $n \times n$ 정방행렬

    $$
    \Sigma=
    \begin{matrix}
    & \overrightarrow{A} & \overrightarrow{B} & \overrightarrow{C} \\
    \overrightarrow{A} & \sigma_{A}^2 & \sigma_{AB} & \sigma_{AC} \\
    \overrightarrow{B} & \sigma_{BA} & \sigma_{B}^2 & \sigma_{BC} \\
    \overrightarrow{C} & \sigma_{CA} & \sigma_{CB} & \sigma_{C}^2
    \end{matrix}
    $$

### Linear Transformation

![02](/_post_refer_img/MachineLearning/10-02.png){: width="100%"}

- 행렬 $\mathbf{X}$ 을 통한 선형변환은 어떤 좌표를 $$\begin{pmatrix}1\\0\end{pmatrix},\begin{pmatrix}0\\1\end{pmatrix}$$ 를 기저로 사용하는 2차원 좌표계에서 $$\overrightarrow{x}_{1},\overrightarrow{x}_{2}$$ 를 기저로 사용하는 2차원 좌표계로 변환하는 것을 의미함

    $$\begin{aligned}
    \mathbf{X}
    &= \begin{pmatrix} 1&3\\-2&0 \end{pmatrix}\\
    &= \begin{pmatrix} \overrightarrow{x}_{1}&\overrightarrow{x}_{2} \end{pmatrix}
    \end{aligned}$$

- 벡터 $\overrightarrow{v}$ 는 $$\begin{pmatrix}1\\0\end{pmatrix},\begin{pmatrix}0\\1\end{pmatrix}$$ 를 기저로 사용하는 2차원 좌표계의 좌표 $(-1,2)$ 를 나타냄

    $$\begin{aligned}
    \overrightarrow{v}
    &= \begin{pmatrix} 1\\-2 \end{pmatrix}\\
    &= -1\begin{pmatrix}1\\0\end{pmatrix} + 2\begin{pmatrix}0\\1\end{pmatrix}\\
    \end{aligned}$$

- $\mathbf{X}$ 를 통한 선형 변환 결과 $$\overrightarrow{v}$$ 는 $$\overrightarrow{x}_{1},\overrightarrow{x}_{2}$$ 를 기저로 사용하는 2차원 좌표계의 좌표 $(-1,2)$ 로 변환되었음

    $$\begin{aligned}
    \mathbf{X}\cdot\overrightarrow{v}
    &= \begin{pmatrix} 1&3\\-2&0 \end{pmatrix} \cdot \begin{pmatrix} 1\\-2 \end{pmatrix}\\
    &= \begin{pmatrix}-5\\2\end{pmatrix}\\
    &= -1\overrightarrow{x}_{1} + 2\overrightarrow{x}_{2}
    \end{aligned}$$

### Eigen-Vector

![03](/_post_refer_img/MachineLearning/10-03.png){: width="100%"}

- **고유벡터(Eigen-Vector; $\overrightarrow{v}$)** : 정방행렬 $A_n$ 으로 선형변환했을 때, 그 방향은 변하지 않고 단지 크기만 변하는 $\overrightarrow{0}$ 이 아닌 벡터

    $$\begin{aligned}
    \begin{pmatrix}
    a_{11}&a_{12}&\cdots&a_{1n}\\
    a_{21}&a_{22}&\cdots&a_{1n}\\
    \vdots&\vdots&\ddots&\vdots\\
    a_{n1}&a_{n2}&\cdots&a_{nn}
    \end{pmatrix}
    \begin{pmatrix}
    v_{1} \\ v_{2} \\ \vdots \\ v_{n}
    \end{pmatrix}
    =
    \lambda
    \begin{pmatrix}
    v_{1} \\ v_{2} \\ \vdots \\ v_{n}
    \end{pmatrix}
    \Leftrightarrow
    A_{n \times n} \overrightarrow{v} 
    = \lambda \overrightarrow{v}
    \end{aligned}$$

- **고유값(Eigen-Value; $\lambda$)** : 고유벡터의 선형변환 전 크기 대비 선형변환 후 크기의 비율

-----

### 이미지 출처

- https://www.incodom.kr/%EC%B0%A8%EC%9B%90%EC%B6%95%EC%86%8C#h_85f3fb207a586b3f9b5702a3be7799e1
- http://matrix.skku.ac.kr/math4ai-intro/W12/
- http://alexhwilliams.info/itsneuronalblog/2016/03/27/pca/
- https://github.com/lovit/python_ml_intro
- https://ekamperi.github.io/machine%20learning/2019/10/19/norms-in-machine-learning.html
- https://observablehq.com/@petulla/l1-l2l_1-l_2l1-l2-norm-geometric-interpretation
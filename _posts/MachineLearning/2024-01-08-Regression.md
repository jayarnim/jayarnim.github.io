---
order: 8
title: Regression
date: 2024-01-08
categories: [Machine Learning Techs, Machine Learning]
tags: [Machine Learning, Supervised Learning, Regression, Regulation, Optimization]
math: true
image:
  path: /_post_refer_img/MachineLearning/Thumbnail.jpg
---

## What? Regression
-----

- **정의** : 반응변수와 그 설명변수 간 상관관계 추세를 요약하는 수렴 작업

- **설명변수의 개수에 따른 구분**
    - **단순 회귀 모형(Simple Regression Model)** : 반응변수에 대한 설명변수가 하나인 경우(이하는 선형모형을 가정)

        $$
        Y=\beta_0+\beta_1X+\varepsilon
        $$

    - **다중 회귀 모형(Multiple Regression Model)** : 반응변수에 대한 설명변수가 두 가지 이상인 경우(이하는 선형모형을 가정)

        $$
        Y=\beta_0+\beta_1 X_1+\beta_2 X_2+\cdots+\beta_k X_k+\varepsilon
        $$

- **선형 가정 여부에 따른 구분**
    - **선형 회귀 모형(Linear Regression Model)** : 설명변수와 반응변수 간 선형관계를 가정하는 경우
        - `sklearn.linear_model.LinearRegression`
        - `sklearn.linear_model.SGDRegressor`

    - **비선형 회귀 모형(Non-Linear Regression Model)** : 설명변수와 반응변수 간 선형관계를 가정하지 않는 경우
        - `sklearn.svm.SVR`
        - `sklearn.tree.DecisionTreeRegressor`

## Linear Regression
-----

### 단순 선형 회귀 모형

![01](/_post_refer_img/MachineLearning/08-01.png){: width="100%"}

- **단순 선형 회귀 모형의 이해**

    $$\begin{aligned}
    &Y=\beta_0+\beta_1X+\varepsilon\\
    &\Rightarrow y_i=\beta_0+\beta_1x_i+\varepsilon_i
    \end{aligned}$$

    - $\varepsilon$ : 잔차항(Residual)
        - $E[\varepsilon]=0$

    - $\beta_0$ : 편향(Bias)

    - $\beta_1$ : 가중치(Weight)

- **최소자승법에 기초한 회귀계수 최적값 도출**
    - **최소자승법(Least Square Method; OLS)** : 회귀계수 최적값을 **잔차항 $\varepsilon_{i}$ 자승의 합계를 최소화하는 값**으로 탐색하는 방법

        $$\begin{aligned}
        \hat{\beta_{0}},\hat{\beta_{1}}
        &= \text{arg} \min_{\beta_{0},\beta_{1}}{L_{OLS}}
        \end{aligned}$$
    
    - 최소자승법에 기초한 손실 함수 $L_{OLS}$

        $$\begin{aligned}
        L_{OLS}
        &= \sum_{i=1}^{n}{\varepsilon_{i}^2}\\
        \varepsilon_{i}
        &= y_{i}-\hat{y}_{i}\\
        &= y_{i}-(\beta_{0}+\beta_{1}\hat{x}_{i})
        \end{aligned}$$

    - 최소자승법에 기초한 회귀계수 $\beta_{0}$ 의 최적값 $\hat{\beta_{0}}$

        $$\begin{aligned}
        \hat{\beta_{0}}
        &= \overline{y}-\beta_{1}\overline{x}
        \end{aligned}$$

    - 최소자승법에 기초한 회귀계수 $\beta_{1}$ 의 최적값 $\hat{\beta_{1}}$

        $$\begin{aligned}
        \hat{\beta_{1}}
        &= \frac{\sum_{i=1}^{n}{(x_{i}-\overline{x})(y_{i}-\overline{y})}}{\sum_{i=1}^{n}{(x_{i}-\overline{x})^{2}}}\\
        &=\frac{\sigma_{xy}}{\sigma_{x}^{2}}
        \end{aligned}$$

### 다중 선형 회귀 모형

![02](/_post_refer_img/MachineLearning/08-02.png){: width="100%"}

- 관측치 $i$ 에 대한 다중 선형 회귀 모형이 다음과 같다고 하자

    $$
    y_{i}=\beta_{0}+\beta_{1}x_{i,1}+\beta_{2}x_{i,2}+\cdots+\beta_{d}x_{i,d}
    $$

    - $i\in\{1,2,\cdots,n\}$ : 관측치 번호
    - $k\in\{1,2,\cdots,d\}$ : 설명변수 번호

- $n$ 개의 관측치가 존재한다고 했을 때 위 모형을 선형대수로 표현할 수 있음

    $$
    \hat{\overrightarrow{y}} = \hat{\mathbf{X}}\overrightarrow{\beta}
    $$

- 최소자승법에 기초하여 도출한 가중치 벡터를 **정규방정식(Normal Equation)**이라고 정의함

    $$\begin{aligned}
    \hat{\overrightarrow{\beta}}
    &= \text{arg} \min_{\overrightarrow{\beta}}{L_{OLS}}\\
    &= (\mathbf{X}^{T}\mathbf{X})^{-1}\mathbf{X}^{T}\overrightarrow{y}
    \end{aligned}$$

## Logistic Regression
-----

- **정의** : 회귀 기법을 판별분석에 활용하는 비선형 함수 알고리즘

    ![01](/_post_refer_img/MachineLearning/08-09.png){: width="100%"}

    $$
    P(c=1)
    = \frac{1}{1+\exp[-(\beta_{0}+\beta_{1}x_{1}+\cdots+\beta_{d}x_{d})]}
    $$

### Logistic Function

- **설명변수와 반응변수 가정**

    - 어떠한 관측치 벡터 $\overrightarrow{x}$ 가 다음과 같이 주어졌다고 하자

        $$\begin{aligned}
        f(\overrightarrow{x})
        &=\beta_{0}+\beta_{1}x_{1}+\cdots+\beta_{d}x_{d} \in (-\infty,\infty)
        \end{aligned}$$

    - $\overrightarrow{x}$ 의 반응변수 $y$ 는 다음과 같음

        $$\begin{aligned}
        y
        &=c \in \{0,1\}
        \end{aligned}$$

    - $y$ 와 $\overrightarrow{x}$ 간에는 공역이 일치하지 않으므로 등식이 성립하지 않음

        $$
        y \ne \beta_{0}+\beta_{1}x_{1}+\cdots+\beta_{d}x_{d}
        $$

- **반응변수 재정의** : 범주 $1$ 에 속할 확률

    $$\begin{aligned}
    y
    &= P(c=1) \in [0,1]
    \end{aligned}$$

- **공역 조정을 통한 연결함수 $f(x)$ 도출**

    - **승산(Odds)** : 범주 $1$ 에 속하지 않을 확률 대비 속할 확률

        $$\begin{aligned}
        f(x)
        &= \text{odds}\\
        &= \frac{P(c=1)}{1-P(c=1)} \in [0, \infty)
        \end{aligned}$$

    - **로짓(Logit)** : 승산에 자연로그를 취한 값

        $$\begin{aligned}
        f(x)
        &= \text{logit}\\
        &= \ln{\frac{P(c=1)}{1-P(c=1)}} \in (-\infty, \infty)
        \end{aligned}$$

    - **로짓 함수와 $\overrightarrow{x}$ 연결**

        $$\begin{aligned}
        \text{logit}
        &= f(x)\\
        &= \beta_{0}+\beta_{1}x_{1}+\cdots+\beta_{d}x_{d}
        \end{aligned}$$

- **연결함수를 활용하여 재정의된 반응변수와 설명변수 연결**

    $$\begin{aligned}
    \ln{\frac{P(c=1)}{1-P(c=1)}}
    &= f(x)\\
    &= \beta_{0}+\beta_{1}x_{1}+\cdots+\beta_{d}x_{d}\\\\

    \frac{P(c=1)}{1-P(c=1)}
    &= e^{f(x)}\\
    &= \exp[\beta_{0}+\beta_{1}x_{1}+\cdots+\beta_{d}x_{d}]\\\\

    \therefore
    y
    &= P(c=1)\\
    &= \frac{1}{1+\exp[-(\beta_{0}+\beta_{1}x_{1}+\cdots+\beta_{d}x_{d})]}
    \end{aligned}$$

## 가중치 규제(Weight Regulation)
-----

- **p-norm** : $n$ 차원 벡터 $\overrightarrow{x}=\begin{pmatrix}x_{1}&x_{2}&\cdots&x_{n}\end{pmatrix}$ 의 크기를 정의하는 방법

    ![03](/_post_refer_img/MachineLearning/08-03.png){: width="100%"}

    $$
    ||x||_{p}=(|x_{1}|^{p}+|x_{2}|^{p}+\cdots+|x_{n}|^{p})^{\frac{1}{p}}
    $$

- **가중치 규제(Weight Regulation)** : 회귀계수 최적값을 탐색함에 있어 회귀계수 벡터 $\overrightarrow{\beta}$ 의 크기에 제약을 두는 것

    ![04](/_post_refer_img/MachineLearning/08-04.png){: width="100%"}

    $$\begin{aligned}
    \overrightarrow{\hat{\beta}}
    &= \text{arg} \min_{\overrightarrow{\beta}}{\left[L_{OLS}+\lambda||\beta||_{p}^{2}\right]}
    \end{aligned}$$

    - $L_{OLS}(\overrightarrow{\beta})$ : 최소자승법에 기초한 손실 함수

    - $\overrightarrow{\beta}$ : 회귀계수 벡터

    - $\lambda$ : 회귀계수 벡터 $\overrightarrow{\beta}$ 크기 제약 강도

    - `p` : 벡터 크기 정의 방법
        - `p=1` : LASSO
        - `p=2` : Ridge

## 경사하강법(Gradient Descent)
-----

- **그라디언트(Gradient)** : 다변수 함수에 대하여 모든 방향으로의 순간변화율 벡터

    ![05](/_post_refer_img/MachineLearning/08-05.png){: width="100%"}

    $$\begin{aligned}
    \nabla{f(x_{1},x_{2},\cdots,x_{n})}
    &= \begin{pmatrix}
    \displaystyle\frac{\partial f(x^{\forall})}{\partial x_{1}}\\
    \displaystyle\frac{\partial f(x^{\forall})}{\partial x_{2}}\\
    \vdots\\
    \displaystyle\frac{\partial f(x^{\forall})}{\partial x_{n}}\\
    \end{pmatrix}
    \end{aligned}$$

- **경사하강법(Gradient Descent)** : 회귀계수 최적값을 탐색함에 있어 손실 함수의 그라디언트를 활용하는 방법

    ![06](/_post_refer_img/MachineLearning/08-06.png){: width="100%"}

- **절차**

    1. 회귀계수 벡터 $\overrightarrow{w}$ 의 초기 아규먼트 설정
    2. 현재 아규먼트 $$\overrightarrow{w}_{prev}$$ 에서 손실 함수의 그라디언트 $$\nabla{L_{OLS}(\overrightarrow{w}_{prev})}$$ 계산
    3. 현재의 아규먼트에서 음의 방향으로 $$\alpha \times \nabla{L_{OLS}(\overrightarrow{w}_{prev})}$$ 만큼 이동하여 새로운 아규먼트 $$\overrightarrow{w}_{new}$$ 적용
    4. ②, ③을 반복하여 손실 함수를 최소화하는 지점 탐색

- **회귀계수 갱신 규칙**

    $$\begin{aligned}
    \overrightarrow{w}_{new}
    &= \overrightarrow{w}_{prev} - \alpha \times \nabla{L_{OLS}(\overrightarrow{w}_{prev})}
    \end{aligned}$$

    - $\overrightarrow{w}_{prev}$ : 현재 회귀계수 아규먼트
    - $\overrightarrow{w}_{new}$ : 새로운 회귀계수 아규먼트
    - $\alpha$ : 학습률
    - $\nabla{L_{OLS}(\overrightarrow{w}_{prev})}$ : 최소자승법에 기초하여 도출한 손실 함수의 그라디언트

- **학습률(Learning Rate)** : 손실 함수에 대하여 그 극소점을 탐색하기 위한 회귀계수 갱신 보폭

    - **학습률이 낮을수록 과대적합될 가능성이 높음**

        ![07](/_post_refer_img/MachineLearning/08-07.png){: width="100%"}

    - **학습률이 높을수록 과소적합될 가능성이 높음**

        ![08](/_post_refer_img/MachineLearning/08-08.png){: width="100%"}

-----

### 이미지 출처

- https://medium.com/analytics-vidhya/multiple-linear-regression-an-intuitive-approach-f874f7a6a7f9
- https://towardsdatascience.com/an-intuitive-explanation-of-gradient-descent-83adf68c9c33
- https://ekamperi.github.io/machine%20learning/2019/10/19/norms-in-machine-learning.html
- https://observablehq.com/@petulla/l1-l2l_1-l_2l1-l2-norm-geometric-interpretation
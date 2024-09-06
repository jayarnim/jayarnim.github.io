---
order: 7
title: Logistic Regression Analysis
date: 2024-07-14
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

### Filter Approach

- **승산(Odds)** : 변수 $Y$ 가 반응할 가능성이 반응하지 않을 가능성보다 몇 배 높은가

    $$\begin{aligned}
    \text{odds}(Y)
    &= \frac{P(Y=1)}{1-P(Y=1)}
    \end{aligned}$$

- **승산비(Odds Ratio; OR)** : 변수 $X$ 가 참일 때 $Y$ 가 반응할 가능성이, $X$ 가 거짓일 때 $Y$ 가 반응할 가능성보다 몇 배 높은가

    $$\begin{aligned}
    \text{OR}(Y|X)
    &= \frac{\text{odds}(X=1)}{\text{odds}(X=0)}\\
    &= \frac{\frac{P(Y=1 \vert X=1)}{1-P(Y=1 \vert X=1)}}{\frac{P(Y=1 \vert X=0)}{1-P(Y=1 \vert X=0)}}
    \end{aligned}$$

    - $$ \text{OR}(Y \vert X) = 1 $$ : $X$ 의 변동이 $Y$ 의 변동에 영향을 미치지 않음
    - $$ \text{OR}(Y\vert X) < 1 $$ : $X$ 는 $Y$ 와 음의 상관관계에 있음
    - $$ \text{OR}(Y \vert X) > 1 $$ : $X$ 는 $Y$ 와 양의 상관관게에 있음

- **로지스틱 회귀식 가중치와 승산비의 상관관계 이해**

    - 단순 회귀 분석 하 로지스틱 회귀식은 다음과 같음

        $$
        \ln{\frac{P(Y=1)}{1-P(Y=1)}}
        =\beta_0 + \beta_1 X
        $$

    - $X=1$ 일 때의 로지스틱 회귀식

        $$\begin{aligned}
        \ln{\displaystyle\frac{P(Y=1 \vert X=1)}{1-P(Y=1 \vert X=1)}}
        &= \beta_0 + \beta_1 \times 1 \\
        &= \beta_0 + \beta_1
        \end{aligned}$$

    - $X=0$ 일 때의 로지스틱 회귀식

        $$\begin{aligned}
        \ln{\displaystyle\frac{P(Y=1 \vert X=0)}{1-P(Y=1 \vert X=0)}}
        &= \beta_0 + \beta_1 \times 0 \\
        &= \beta_0
        \end{aligned}$$

    - 두 회귀식을 빼면 다음과 같음

        $$\begin{aligned}
        &\ln{\displaystyle\frac{P(Y=1 \vert X=1)}{1-P(Y=1 \vert X=1)}} - \ln{\displaystyle\frac{P(Y=1 \vert X=0)}{1-P(Y=1 \vert X=0)}}\\
        &= \ln{\frac{\frac{P(Y=1 \vert X=1)}{1-P(Y=1 \vert X=1)}}{\frac{P(Y=1 \vert X=0)}{1-P(Y=1 \vert X=0)}}}\\
        &= (\beta_0 + \beta_1) - \beta_0\\
        &= \beta_1
        \end{aligned}$$

    - 따라서 설명변수 $X$ 의 가중치 $\beta_1$ 과 승산비 $\text{OR}(Y\|X)$ 간에는 다음과 같은 관계가 성립함

        $$\begin{aligned}
        \therefore \text{OR}(Y|X)
        &= \frac{\frac{P(Y=1 \vert X=1)}{1-P(Y=1 \vert X=1)}}{\frac{P(Y=1 \vert X=0)}{1-P(Y=1 \vert X=0)}} \\
        &= \exp[\beta_1]
        \end{aligned}$$

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

    $$
    \hat{\overrightarrow{w}}
    =\text{arg} \max_{\overrightarrow{w}}{\frac{\overrightarrow{w}^{T}\mathbf{S}_{B}\overrightarrow{w}}{\overrightarrow{w}^{T}(\mathbf{S}_{1}+\mathbf{S}_{2})\overrightarrow{w}}}\\
    \begin{aligned}
    \\\text{s.t.} \quad
    & \overrightarrow{w}^{T}\overrightarrow{w}=1
    \end{aligned}
    $$

- **라그랑주 승수법을 통한 최적화 문제 풀이**

    $$\begin{aligned}
    L(\overrightarrow{w},\lambda)
    &= \frac{\overrightarrow{w}^{T}\mathbf{S}_{B}\overrightarrow{w}}{\overrightarrow{w}^{T}(\mathbf{S}_{1}+\mathbf{S}_{2})\overrightarrow{w}}-\lambda(\overrightarrow{w}^{T}\overrightarrow{w}-1)\\\\

    \frac{\partial L(\overrightarrow{w},\lambda)}{\partial \overrightarrow{w}}
    &= 0\\\\

    \therefore \left[\mathbf{S}_{B}^{-1}(\mathbf{S}_{1}+\mathbf{S}_{2})-\lambda\mathbf{I}\right]\hat{\overrightarrow{w}}
    &=0
    \end{aligned}$$
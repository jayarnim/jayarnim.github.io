---
order: 4
title: Naive Bayes
date: 2024-01-04
categories: [Data Mining Techs, Machine Learning]
tags: [Machine Learning, Supervised Learning, Classification, Bayesian]
math: true
description: >-
  Based on the lecture “Intro. to Machine Learning (2023-2)” by Prof. Je Hyuk Lee, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
  path: /_post_refer_img/MachineLearning/Thumbnail.jpg
---

## Naive Bayes
-----

- **정의** : 조건부 확률에 기초하여 관측치의 범주를 판별하는 알고리즘

- **조건부 확률의 이해**

    $$\begin{aligned}P(B \mid A)&= \frac{P(A,B)}{P(A)}\end{aligned}$$

    - $$P(B \mid A)$$ : 사건 $$A$$ 가 발생한 상태에서 사건 $$B$$ 가 발생할 확률
    - $$P(A,B)$$ : 사건 $$A$$, $$B$$ 가 공동으로 발생할 확률
    - $$P(A)$$ : 사건 $$A$$ 가 발생할 확률
    - $$P(B)$$ : 사건 $$B$$ 가 발생할 확률

- **Class Conditional Independent Assumption** : 범주 내에서 특정 특성의 존재 또는 부재가 다른 특성의 존재 또는 부재와 독립적이라는 가정을 전제함함

    $$\begin{aligned}
    P(X_{1},X_{2},\cdots,X_{n} \mid Y)
    &= P(X_{1} \mid Y) \times P(X_{2} \mid Y) \times \cdots \times P(X_{n} \mid Y)
    \end{aligned}$$

## Decision Function
-----

- **문제 정의**

    $$\begin{aligned}
    \hat{Y}
    &= f(\overrightarrow{x})\\
    &= \text{arg} \max_{Y}{P(Y=i \mid X_{1}=x_{1},X_{2}=x_{2},\cdots,X_{n}=x_{n})}
    \end{aligned}$$

    - 관측치 벡터 $$\overrightarrow{x}$$ 의 범주 $$\hat{Y}$$ 는 $$\overrightarrow{x}$$ 가 $$(x_{1},x_{2},\cdots,x_{n})$$ 로 주어졌을 때, 범주 $$Y$$ 가 $$i=1,2,\cdots$$ 일 확률이 최대인 $$i$$ 임

- **베이즈 정리에 의해 다음이 성립함**

    $$\begin{aligned}
    &P(Y=i \mid X_{1}=x_{1},X_{2}=x_{2},\cdots,X_{n}=x_{n})\\
    &= \frac{P(X_{1}=x_{1},X_{2}=x_{2},\cdots,X_{n}=x_{n} \mid Y=i) \cdot P(Y=i)}{P(X_{1}=x_{1},X_{2}=x_{2},\cdots,X_{n}=x_{n})}
    \end{aligned}$$

    - $$P(Y=i \mid X_{1}=x_{1},X_{2}=x_{2},\cdots,X_{n}=x_{n})$$ : 관측치 벡터 $$\overrightarrow{x}=(x_{1},x_{2},\cdots,x_{n})$$ 가 주어졌을 때, 해당 관측치의 범주 $$Y$$ 가 $i$ 일 확률
    - $$P(X_{1}=x_{1},X_{2}=x_{2},\cdots,X_{n}=x_{n} \mid Y=i)$$ : 범주 $$Y=i$$ 가 주어졌을 때, 관측치 벡터 $$\overrightarrow{x}$$ 가 $$(x_{1},x_{2},\cdots,x_{n})$$ 일 확률
    - $$P(Y=i)$$ : 범주 $$Y$$ 가 $$i$$ 일 확률
    - $$P(X_{1}=x_{1},X_{2}=x_{2},\cdots,X_{n}=x_{n})$$ : 관측치 벡터 $$\overrightarrow{x}$$ 가 $$(x_{1},x_{2},\cdots,x_{n})$$ 일 확률

- **클래스 조건부 독립 가정 하 다변량 조건부 확률을 단변량 조건부 확률로 변환할 수 있음**

    $$\begin{aligned}
    &P(X_{1},X_{2},\cdots,X_{n} \mid Y)\\
    &= P(X_{1} \mid Y) \times P(X_{2} \mid Y) \times \cdots \times P(X_{n} \mid Y)
    \end{aligned}$$

- **따라서 관측치 벡터 $$\overrightarrow{x}$$ 의 범주 $$Y$$ 가 $$i$$ 일 확률은 다음과 같음**

    $$\begin{aligned}
    &P(Y=i \mid X_{1}=x_{1},X_{2}=x_{2},\cdots,X_{n}=x_{n})\\
    &= \frac{P(X_{1}=x_{1},X_{2}=x_{2},\cdots,X_{n}=x_{n} \mid Y=i) \cdot P(Y=i)}{P(X_{1}=x_{1},X_{2}=x_{2},\cdots,X_{n}=x_{n})}\\
    &= \frac{P(X_{1}=x_{1},X_{2}=x_{2},\cdots,X_{n}=x_{n} \mid Y=i) \cdot P(Y=i)}{\sum_{j}P(X_{1}=x_{1},X_{2}=x_{2},\cdots,X_{n}=x_{n} \mid Y=j)}\\
    &= \frac{\prod_{k=1}^{n}{P(X_{k}=x_{k} \mid Y=i)} \cdot P(Y=i)}{\sum_{j}{\prod_{k=1}^{n}{P(X_{k}=x_{k} \mid Y=j)}}}
    \end{aligned}$$

## Laplace Smoothing
-----

- **라플라스 평활화(Laplace Smoothing)** : 훈련 데이터 세트에 존재하지 않는 사례 $$\overrightarrow{x}_{k}$$ 에 대한 확률을 $$0$$ 으로 부여하는 것을 방지하기 위한 기법

- **계산 방법**

    $$
    P(\overrightarrow{x}_{k} \mid Y)
    = \frac{\text{count}(\overrightarrow{x}_{k},Y)+\alpha}{\text{count}(Y)+2\alpha}
    $$

    - $$P(\overrightarrow{x}_{k} \mid Y)$$ : 관측치 벡터 $$\overrightarrow{x}_{k}$$ 가 범주 $$Y$$ 에 속할 조건부 확률
    - $$\text{count}(\overrightarrow{x}_{k},Y)$$ : 관측치 벡터 $$\overrightarrow{x}_{k}$$ 와 범주 $$Y$$ 의 동시 출현 빈도
    - $$\text{count}(Y)$$ : 범주 $$Y$$ 의 출현 빈도
    - $$\alpha$$ : 라플라스 평활화 강도
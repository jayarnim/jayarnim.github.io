---
order: 4
title: Naive Bayes
date: 2024-08-15
categories: [5.BAYES, 3.bayes applications]
tags: [bayesian, categorical data analysis]
math: true
description: >-
    Based on the lecture “Intro. to Machine Learning (2023-2)” by Prof. Je Hyuk Lee, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
  path: /_post_refer_img/5.BAYES/3.application/Thumbnail.jpg
---

## Naive Bayes
-----

- **나이브 베이즈(Naive Bayes)**: 베이즈 정리에 기초하여 관측치의 범주를 판별하는 알고리즘

    ![01](/_post_refer_img/5.BAYES/3.application/04-01.png){: width="100%"}

- Class Conditional Independent Assumption:

    $$\begin{aligned}
    P(X_{1},X_{2},\cdots,X_{n} \mid Y)
    &= P(X_{1} \mid Y) \times P(X_{2} \mid Y) \times \cdots \times P(X_{n} \mid Y)
    \end{aligned}$$

## Decision Function
-----

- problem definition:

    $$\begin{aligned}
    \hat{Y}
    &= f(\mathbf{x})\\
    &= \text{arg} \max_{Y}{P(Y=i \mid X_{1}=x_{1},X_{2}=x_{2},\cdots,X_{n}=x_{n})}
    \end{aligned}$$

    - 관측치 벡터 $$\mathbf{x}$$ 의 범주 $$\hat{Y}$$ 는 $$\mathbf{x}$$ 가 $$(x_{1},x_{2},\cdots,x_{n})$$ 로 주어졌을 때, 범주 $$Y$$ 가 $$i=1,2,\cdots$$ 일 확률이 최대인 $$i$$ 임

- By Bayes' theorem:

    $$\begin{aligned}
    &P(Y=i \mid X_{1}=x_{1},X_{2}=x_{2},\cdots,X_{n}=x_{n})\\
    &= \frac{P(X_{1}=x_{1},X_{2}=x_{2},\cdots,X_{n}=x_{n} \mid Y=i) \cdot P(Y=i)}{P(X_{1}=x_{1},X_{2}=x_{2},\cdots,X_{n}=x_{n})}
    \end{aligned}$$

    - $$P(Y=i \mid X_{1}=x_{1},X_{2}=x_{2},\cdots,X_{n}=x_{n})$$ : 관측치 범주에 대한 사후 확률로서, 관측치 벡터 $$\mathbf{x}=(x_{1},x_{2},\cdots,x_{n})$$ 가 주어졌을 때, 해당 관측치의 범주 $$Y$$ 가 $i$ 일 확률
    - $$P(X_{1}=x_{1},X_{2}=x_{2},\cdots,X_{n}=x_{n} \mid Y=i)$$ : 관측치 범주에 대한 우도로서, 범주 $$Y=i$$ 가 주어졌을 때, 관측치 벡터 $$\mathbf{x}$$ 가 $$(x_{1},x_{2},\cdots,x_{n})$$ 일 확률
    - $$P(Y=i)$$ : 관측치 범주에 대한 사전 확률로서, 범주 $$Y$$ 가 $$i$$ 일 확률
    - $$P(X_{1}=x_{1},X_{2}=x_{2},\cdots,X_{n}=x_{n})$$ : 관측치 범주에 대한 주장의 근거로서, 관측치 벡터 $$\mathbf{x}$$ 가 $$(x_{1},x_{2},\cdots,x_{n})$$ 일 확률

- Multivariate conditional probability can be converted to univariate conditional probability under class conditional independence assumption:

    $$\begin{aligned}
    &P(X_{1},X_{2},\cdots,X_{n} \mid Y)\\
    &= P(X_{1} \mid Y) \times P(X_{2} \mid Y) \times \cdots \times P(X_{n} \mid Y)
    \end{aligned}$$

- therefore:

    $$\begin{aligned}
    &P(Y=i \mid X_{1}=x_{1},X_{2}=x_{2},\cdots,X_{n}=x_{n})\\
    &= \frac{P(X_{1}=x_{1},X_{2}=x_{2},\cdots,X_{n}=x_{n} \mid Y=i) \cdot P(Y=i)}{P(X_{1}=x_{1},X_{2}=x_{2},\cdots,X_{n}=x_{n})}\\
    &= \frac{P(X_{1}=x_{1},X_{2}=x_{2},\cdots,X_{n}=x_{n} \mid Y=i) \cdot P(Y=i)}{\sum_{j}P(X_{1}=x_{1},X_{2}=x_{2},\cdots,X_{n}=x_{n} \mid Y=j)}\\
    &= \frac{\prod_{k=1}^{n}{P(X_{k}=x_{k} \mid Y=i)} \cdot P(Y=i)}{\sum_{j}{\prod_{k=1}^{n}{P(X_{k}=x_{k} \mid Y=j)}}}
    \end{aligned}$$

## Laplace Smoothing
-----

- **라플라스 평활화(Laplace Smoothing)**: 훈련 데이터 세트에 존재하지 않는 사례 $$\mathbf{x}_{k}$$ 에 대한 확률을 $$0$$ 으로 부여하는 것을 방지하기 위한 기법

    $$
    P(\mathbf{x}_{k} \mid Y)
    = \frac{\text{Count}(\mathbf{x}_{k},Y)+\alpha}{\text{Count}(Y)+2\alpha}
    $$

    - $$P(\mathbf{x}_{k} \mid Y)$$ : 관측치 벡터 $$\mathbf{x}_{k}$$ 가 범주 $$Y$$ 에 속할 조건부 확률
    - $$\text{Count}(\mathbf{x}_{k},Y)$$ : 관측치 벡터 $$\mathbf{x}_{k}$$ 와 범주 $$Y$$ 의 동시 출현 빈도
    - $$\text{Count}(Y)$$ : 범주 $$Y$$ 의 출현 빈도
    - $$\alpha$$ : 라플라스 평활화 강도

-----

## Sourse

- https://www.linkedin.com/pulse/naive-bayes-theorem-machine-learning-rohit-bele/
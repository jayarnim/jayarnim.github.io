---
order: 1
title: Simple Linear Regression Analysis
date: 2024-06-24
categories: [Statistical Techs, Regression Analysis]
tags: [Statistics, Regression, OLS, R2]
math: true
description: >-
  Based on the lecture "Statistical Models and Application (2024-1)" by Prof. Yeo Jin Chung, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
  path: /_post_refer_img/RegressionAnalysis/Thumbnail.jpg
---

## 회귀분석

- **회귀분석(Regression)**
    - **정의** : 반응변수 $Y$ 와 설명변수 $X$ 의 상관관계를 분석하는 작업

    - **예시**
        - 광고지출비용이 증가할 때 매출액은 어떻게 변하는가?
        - 소득이 높은 국가의 국민들이 더 행복한가?
        - 소득이 증가할 때 소비는 얼마나 증가하는가?
        - 교육수준이 높을수록 임금이 증가하는가?

- **선형회귀모형(Linear Regression Model)**
    - **정의** : 반응변수 $Y$ 와 그 설명변수 $X$ 가 선형관계를 가지는 모형

    - **구분**
        - **단순선형회귀모형** : 설명변수가 하나인 경우

            $$
            Y=\beta_0+\beta_1X+\varepsilon
            $$

        - ~~**다중선형회귀모형** : 설명변수가 두 개 이상인 경우~~

            $$
            Y=\beta_0+\beta_1 X_1+\beta_2 X_2+\cdots+\beta_k X_k+\varepsilon
            $$

- **단순선형회귀모형의 이해**

    $$\begin{aligned}
    &Y=\beta_0+\beta_1X+\varepsilon\\
    &\Rightarrow y_i=\beta_0+\beta_1x_i+\varepsilon_i
    \end{aligned}$$

    - $Y$ : 종속변수(Dependent Variable), 반응변수(Response Variable)

    - $X$ : 독립변수(Independent Variable), 설명변수(Explanatory Variable)

    - $\varepsilon$ : 오차항(Error Term)
        - 설명변수 이외 잠재변수들의 영향력
        - 오차항의 기대값 $E(\varepsilon)$ 은 $0$

    - $\beta_0$ : 편향(Bias)
        - 반응변수의 초기 상태로서 설명변수의 영향력이 존재하지 않는 상태
        - 회귀식을 좌표평면에 표현하는 경우 $Y$ 절편에 해당함

    - $\beta_1$ : 가중치(Weight)
        - 반응변수에 대한 설명변수의 상관관계 방향과 세기
        - 회귀식을 좌표평면에 표현하는 경우 기울기에 해당함

- **선형회귀분석의 실질적 목표**
    - 선형회귀분석은 모든 관측치에 대하여 $Y$ 와 $X$ 의 상관관계를 가장 잘 나타내는 하나의 직선을 찾는 작업임

    - 하나의 직선이 모든 관측치를 두루 잘 설명하기 위해서는 모수(실제값)와 그 추정량(예측값)의 차이의 크기를 최소화하는 것이 중요함

        <p align="center"><img src="https://user-images.githubusercontent.com/116495744/221339174-de431950-85c5-4156-afbc-0d3ba0b9c8e4.png" width=80%></p>

    - 선형회귀분석의 실질적 목표는 모수(실제값)와 그 추정량(예측값)의 차이의 크기를 최소화하는 회귀계수 조합을 찾는 것임

        - **회귀계수(Regression Coefficient)** : 편향 $\beta_0$ 과 가중치 $\beta_1$

</br>

## 최소자승법

- **잔차(Residual; $e_i$)** : 관측치 $y_i$ 와 그 추정량 $\hat{y_i}$ 의 차이

    - 회귀계수 $\beta_0, \beta_1$ 의 추정량 $\hat{\beta_0}, \hat{\beta_1}$ 에 대하여 관측치 $y_i$ 를 추정하는 회귀식은 다음과 같음

        $$
        \hat{y_i}=\hat{\beta_0}+\hat{\beta_1}x_i
        $$

    - 관측치 $y_i$ 와 그 추정량 $\hat{y_i}$ 의 차이를 잔차로 정의함

        $$\begin{aligned}
        e_i
        &= y_i - \hat{y_i}\\
        &= y_i - (\hat{\beta_0}+\hat{\beta_1}x_i)
        \end{aligned}$$

- **최소자승법(Ordinary Least Squares; $OLS$)** : 잔차 자승(제곱)의 합을 최소화하는 회귀계수 조합을 추정하는 방법

    $$\begin{aligned}
    \displaystyle\min_{\hat{\beta_0}, \hat{\beta_1}}S(\hat{\beta_0}, \hat{\beta_1})
    \end{aligned}$$

    $$\begin{aligned}
    S(\hat{\beta_0}, \hat{\beta_1})
    &= \displaystyle\sum_{i=1}^{n}(e_i)^2 \\
    &= \displaystyle\sum_{i=1}^{n}(y_i - \hat{y_i})^2 \\
    &= \displaystyle\sum_{i=1}^{n}(y_i - (\hat{\beta_0}+\hat{\beta_1}x_i))^2
    \end{aligned}$$

- **최소자승추정량은 다음을 만족함**
    - $\overline{Y}=\hat{\beta_0}+\hat{\beta_1}\overline{X}$
    - $\overline{e}=\displaystyle\frac{1}{n}\displaystyle\sum_{i=1}^{n}e_i=0$
    - $\displaystyle\sum_{i=1}^{n}e_iX_i=0$

</br>

## 최소자승법에 의한 회귀계수 추정량 도출

- **회귀계수의 추정량**

    - 편향 $\beta_0$ 의 최소자승추정량

        $$\begin{aligned}
        \hat{\beta_0}
        &= \overline{Y} - \hat{\beta_1}\overline{X}
        \end{aligned}$$

    - 가중치 $\beta_1$ 의 최소자승추정량

        $$\begin{aligned}
        \hat{\beta_1}
        &= \displaystyle\frac{Cov(X,Y)}{Var(X)} \\
        &= \displaystyle\frac{\displaystyle\sum_{i=1}^{n}(X_i-\overline{X})(Y_i-\overline{Y})}{\displaystyle\sum_{i=1}^{n}(X_i-\overline{X})^2}
        \end{aligned}$$

- **증명**
    - 반응변수 $Y$ 의 표본평균 $\overline{Y}$ 와 설명변수 $X$ 의 표본평균 $\overline{X}$ 는 다음과 같음

        $$\begin{aligned}
        \overline{Y}
        &= \frac{1}{n}\displaystyle\sum_{i=1}^{n}Y_i \\
        \overline{X}
        &= \frac{1}{n}\displaystyle\sum_{i=1}^{n}X_i
        \end{aligned}$$

    - 잔차 자승의 합 $S(\hat{\beta_0}, \hat{\beta_1})$ 을 $\hat{\beta_0}$ 로 편미분

        $$\begin{aligned}
        \displaystyle\frac{\partial S(\hat{\beta_0}, \hat{\beta_1})}{\partial \hat{\beta_0}}
        &= -2\times\displaystyle\sum_{i=1}^{n}(Y_i-\hat{\beta_0}-\hat{\beta_1}X_i) \\
        &= -2\times(\displaystyle\sum_{i=1}^{n}Y_i-n\hat{\beta_0}-\hat{\beta_1}\displaystyle\sum_{i=1}^{n}X_i) \cdots①\\
        &= -2n \times (\overline{Y} - \hat{\beta_0} - \hat{\beta_1}\overline{X}) \\
        &= 0 \\ \\
        \therefore\hat{\beta_0}
        &= \overline{Y} - \hat{\beta_1}\overline{X}\;(s.t.\;n\ne 0)
        \end{aligned}$$

    - 잔차 자승의 합 $S(\hat{\beta_0}, \hat{\beta_1})$ 을 $\hat{\beta_1}$ 로 편미분

        $$\begin{aligned}
        \displaystyle\frac{\partial S(\hat{\beta_0}, \hat{\beta_1})}{\partial \hat{\beta_1}}
        &= -2\times\displaystyle\sum_{i=1}^{n}(Y_i-\beta_0-\beta_1X_i)\times X_i \\
        &= -2\times(\displaystyle\sum_{i=1}^{n}Y_iX_i-\beta_0\displaystyle\sum_{i=1}^{n}X_i-\beta_1\displaystyle\sum_{i=1}^{n}(X_i)^2) \cdots②\\
        &= 0
        \end{aligned}$$

    - 식 ①, ② 를 적절히 변형하여 뺄셈

        $$\begin{aligned}
        -\frac{1}{2}(① \times \displaystyle\sum_{i=1}^{n}X_i - ② \times n)
        &= \displaystyle\sum_{i=1}^{n}Y_i \displaystyle\sum_{i=1}^{n}X_i - n \times \displaystyle\sum_{i=1}^{n}Y_iX_i - \hat{\beta_1}(\displaystyle\sum_{i=1}^{n}X_i)^2 + n \times \beta_1 \times \displaystyle\sum_{i=1}^{n}(X_i)^2 \\
        &= n\overline{Y} \times n\overline{X}-n\displaystyle\sum_{i=1}^{n}Y_iX_i-\hat{\beta_1}(n\overline{X})^2+ n \times \hat{\beta_1} \times \displaystyle\sum_{i=1}^{n}(X_i)^2 \\
        &= \hat{\beta_1}(n\displaystyle\sum_{i=1}^{n}(X_i)^2-n^2(\overline{X})^2)-(\displaystyle\sum_{i=1}^{n}Y_iX_i-n^2\overline{Y}\overline{X}) \\
        &= \hat{\beta_1} \times n^2 \times (\frac{1}{n}\displaystyle\sum_{i=1}^{n}(X_i)^2 - \overline{X}^2) - n^2 \times (\frac{1}{n^2}\displaystyle\sum_{i=1}^{n}Y_iX_i - \overline{Y}\overline{X}) \\
        &= 0
        \end{aligned}$$

    - $\hat{\beta_1}$ 에 대하여 정리

        $$\begin{aligned}
        \hat{\beta_1}
        &= \frac{n^2 \times (\displaystyle\frac{1}{n^2}\displaystyle\sum_{i=1}^{n}Y_iX_i - \overline{Y}\overline{X})}{n^2 \times (\displaystyle\frac{1}{n}\displaystyle\sum_{i=1}^{n}(X_i)^2 - \overline{X}^2)} \\
        &= \frac{\displaystyle\frac{1}{n^2}\displaystyle\sum_{i=1}^{n}Y_iX_i - \overline{Y}\overline{X}}{\displaystyle\frac{1}{n}\displaystyle\sum_{i=1}^{n}(X_i)^2 - \overline{X}^2} \\ \\
        \therefore \hat{\beta_1}
        &= \displaystyle\frac{Cov(X,Y)}{Var(X)}
        \end{aligned}$$
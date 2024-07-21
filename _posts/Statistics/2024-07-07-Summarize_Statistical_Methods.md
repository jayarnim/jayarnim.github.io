---
order: 7
title: Summarize Statistical Method
date: 2024-07-07
categories: [Statistical Techs, Statistics]
tags: [Statistics, Normality Test, Shapiro-Wilk Test, Homogeneity of Variance Test, Levene’s Test, ANOVA]
math: true
description: >-
  Based on the following lectures <br>
  (1) “Statistics (2018-1)” by Prof. Sang Ah Lee, Dept. of Economics, College of Economics & Commerce, Kookmin Univ. <br>
  (2) "Statistical Models and Application (2024-1)" by Prof. Yeo Jin Chung, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
  path: /_post_refer_img/Statistics/Thumbnail.png
---

## 수치형 변수의 평균에 대한 추론
-----

| 문제 | 관심모수 | 점추정량 | 가정체크 | 검정가설 | 검정방법 | Python Module |
|---|---|---|---|---|---|---|
| 단일 집단의 평균 | $\mu$ | $\bar{X}$ | $n>30$ or $X \sim N$ | $H_0: \mu=\mu_0$ | One Sample t-Test | `statsmodels.stats.ttest_mean` |
| 두 집단 간 평균 비교 <br> (독립표본) | $\mu_1-\mu_2$ | $$\bar{X}_{1} - \bar{X}_{2}$$ | $(n_1 + n_2)>30$ or $X_{1}\sim N, X_{2} \sim N$ | $H_0: \mu_1 - \mu_2 = 0$ | Two Sample t-Test | `statsmodels.stats.weightstats.ttest_ind` |
| 두 집단 간 평균 비교 <br> (쌍체표본)  | $\mu_d$ | $\bar{X}_d$ | $n>30$ or $X \sim N$ | $H_0: \mu_d=0$ | Paired t-Test | `statsmodels.stats.ttest_mean` |
| 셋 이상 그룹 간 평균 비교 | $\mu_1, \cdots, \mu_m$ |  $\bar{X}_1, \cdots, \bar{X}_m$ |  $n_i>30$ or $X_{i} \sim N$ <br> $\sigma_{i}^{2}=\sigma_{j}^{2}$ | $H_0: \mu_1 = \cdots = \mu_m$ | ANOVA | `statsmodels.stats.anova.AnovaRM` |
| 양적변수 간의 상관관계 | $\beta_0, \beta_1$ <br> $(y=\beta_0+\beta_1 x + \epsilon)$ | $\hat{\beta}_0, \hat{\beta}_1$ | 반응변수와 설명변수 간 선형성 <br> 설명변수 간 독립성 <br> 오차의 등분산성 <br> 오차의 정규성 | $H_0: \beta_i=0$ | Regression | `statsmodels.api.OLS` |

## 범주형 변수의 비율에 대한 추론
-----

| 문제 | 관심모수 | 점추정량 | 가정체크 | 검정가설 | 검정방법 | Python Module |
|---|---|---|---|---|---|---|
| 단일 집단의 비율 | $\pi$ | $p$ | $np>5$ <br> $n(1-p)>5$ | $H_0: \pi=\pi_0$ | One Sample z-Test | `statsmodels.stats.proportion.proportions_ztest` |
| 두 집단 간 비율 비교 | $\pi_1 - \pi_2$ | $p_1 - p_2$ | $n_i p_i > 5$ <br> $n_i (1-p_i)>5$ | $H_0: \pi_1-\pi_2=0$ | Two Sample z-Test | `statsmodels.stats.proportion.proportions_ztest` |
| 적합성 검정 | $\pi_1, \cdots, \pi_m$ | $p_1, \cdots, p_m$ | $n_i p_i > 5$ <br> $n_i (1-p_i)>5$ | $H_0: \pi_1=p_{0}^{(1)}, \cdots, \pi_m=p_{0}^{(m)}$ | Chi-square test | `scipy.stats.chisquare` |
| 독립성 검정 | | | $n_i p_i > 5$ <br> $n_i (1-p_i)>5$ | $H_0:$ 두 범주형 변수가 독립 | Chi-square test | `scipy.stats.chi2_contingency` |
| 양적변수와의 상관관계 | $\beta_0, \beta_1$ <br> $(\pi=\beta_0+\beta_1 x)$ | $\hat{\beta}_0, \hat{\beta}_1$ | $Y \sim B$ | $H_0: \beta_i=0$ | Logistic regression | `sklearn.linear_models.LogisticRegression` |

## refer.
-----

### 정규성 검정(Shapiro-Wilk Test)

- **귀무가설과 대립가설 설정**
    - $H_{0}:\quad X \sim N(\mu, \sigma^2)$
    - $H_{1}:\quad X \not\sim N(\mu, \sigma^2)$

- **검정통계량 도출**

    $$
    W=\frac{\left(\sum_{i=1}^{n} \alpha_{i} X_{i}\right)^2}{\sum_{i=1}^{n}\left(X_{i} - \overline{X}\right)^2}
    $$

    - $\overrightarrow{X}$ : 표본의 관측치 $X_{i}$ 를 크기에 따라 오름차순 정렬한 순위 통계량 벡터

        $$\begin{aligned}
        \overrightarrow{X}
        =\begin{pmatrix} X_{1}&X_{2}&\cdots&X_{n} \end{pmatrix}^{T}
        \end{aligned}$$

        - $\overline{X}=\displaystyle\frac{1}{n}\sum_{i=1}^{n}{X_{i}}$ : 표본평균

    - $\overrightarrow{\alpha}$ : 순위 통계량 벡터 $\overrightarrow{X}$ 의 계수 벡터

        $$
        \overrightarrow{\alpha}=\displaystyle\frac{\overrightarrow{m}^{T}\mathbb{V}^{-1}}{\Vert \mathbb{V}^{-1}\overrightarrow{m} \Vert}
        $$

        - $\overrightarrow{m}$ : 기대 순위 통계량 벡터

            $$
            \overrightarrow{m}=\begin{pmatrix} E\left[X_{1}\right]&E\left[X_{2}\right]&\cdots&E\left[X_{n} \right]\end{pmatrix}^{T}
            $$

        - $\mathbb{V}$ : 기대 순위 통계량의 공분산 행렬

            $$
            \mathbb{V}_{i,j}=\text{Cov}\Big[E\left[X_{i}\right],E\left[X_{j}\right]\Big]
            $$

        - $\overrightarrow{m}^{T}\mathbb{V}^{-1}$ : $\mathbb{V}^{-1}$ 에 의해 선형 변환되어 상호 독립된 기대 순위 통계량 벡터
        - $\Vert \mathbb{V}^{-1}\overrightarrow{m} \Vert$ : 정규화 항

- **표본 $Y \sim N(0,1)$ 를 활용한 경험적 분포 생성**
    1. 표준정규분포로부터 $n$ 개의 관측치로 구성된 표본을 반복적으로 생성

        $$\begin{aligned}
        \overrightarrow{Y}^{(k)}
        =\begin{pmatrix} Y_{1}^{(k)}&Y_{2}^{(k)}&\cdots&Y_{k}^{(k)} \end{pmatrix}^{T} \quad \text{for}\; Y^{(k)}_{i} \sim N(0,1)
        \end{aligned}$$

    2. 각 표본에 대하여 검정통계량 도출

        $$
        W^{(k)}=\frac{\left(\sum_{i=1}^{k} \alpha_{i} Y_{i}\right)^2}{\sum_{i=1}^{k}\left(Y_{i} - \overline{Y}\right)^2}
        $$

    3. $n$ 의 크기에 따른 $W$ 의 경험적 분포 도출

        $$
        f_{W}:n \rightarrow W
        $$

    4. $W$ 의 경험적 분포에서 특정 $w$ 값보다 작거나 같은 값을 가질 확률 도출

        $$\begin{aligned}
        \text{p-value}
        &=F_{W}(w)\\
        &=P(W \le w)
        \end{aligned}$$

- **표본 $X$ 에 대한 검정통계량 $W$ 의 $\text{p-value}$ 와 유의수준 $\alpha$ 비교**
    - $F_{W}(W) \le \alpha$ : $X \not\sim N(\mu, \sigma^2)$

        > 귀무가설이 참이라는 가정 하에 도출된 검정통계량보다 극단적인 실현값이 발생할 가능성이 현저히 낮다. 이는 귀무가설이 참이라는 가정 하에 표본이 실현될 가능성이 현저히 낮음을 의미한다. 따라서 유의수준 $\alpha$ 하 귀무가설을 기각한다.

    - $\alpha < F_{W}(W)$ : $X \sim N(\mu, \sigma^2)$

        > 귀무가설이 참이라는 가정 하에 도출된 검정통계량보다 극단적인 실현값이 발생할 가능성이 어느 정도 존재한다. 이는 귀무가설이 참이라는 가정 하에 표본이 실현될 가능성이 현저히 낮다고 볼 수 없음을 의미한다. 따라서 유의수준 $\alpha$ 하 귀무가설을 기각하지 않는다.

### 등분산 검정(Levene’s Test)

- **관심 모수에 대한 점 추정량 도출**
    - **관심 모수** : $$\sigma_{1}^{2},\sigma_{2}^{2},\cdots,\sigma_{k}^{2}$$
    - **점 추정량** : $$S_{1}^{2},S_{2}^{2},\cdots,S_{k}^{2}$$

- **귀무가설과 대립가설 설정**
    - $H_{0}:\quad$ 모든 $i$ 에 대하여 $\displaystyle\frac{\sigma_{i}^{2}}{\sigma_{j \ne i}^{2}}=1$
    - $H_{1}:\quad$ 어떤 $i$ 에 대하여 $\displaystyle\frac{\sigma_{i}^{2}}{\sigma_{j \ne i}^{2}} \ne 1$

- **검정통계량 도출**

    $$
    F=\frac{\text{SSB} / (k-1)}{\text{SSW} / (N-k)} \sim F(k-1, N-k)
    $$

    - **SSB(Sum of Square Between)** : 집단 간 편차 자승의 합

        $$
        \text{SSB}=\sum_{i=1}^{k}{N_{i}\left(\overline{Z}^{(i)}-\overline{Z}\right)^2} \sim \chi^2(k-1)
        $$

        - $\overline{Z}^{(i)}$ : $i$ 번째 집단에 대하여 그 절대편차 $$Z^{(i)}_{\forall}$$ 의 평균
        - $\overline{Z}$ : 모든 관측치 $X^{(\forall)}_{\forall}$ 에 대하여 그 절대편차 $$Z^{(\forall)}_{\forall}$$ 의 평균
        - $k$ : 표본 내 집단 갯수

    - **SSW(Sum of Within)** : 집단 내 편차 자승의 합

        $$
        \text{SSW}=\sum_{i=1}^{k}\sum_{j=1}^{N_{i}}{\left(Z^{(i)}_{j}-\overline{Z}^{(i)}\right)^2} \sim \chi^2(N-k)
        $$

        - $$Z^{(i)}_{j}$$ : $$i$$ 번째 집단의 $$j$$ 번째 관측치 $$X^{(i)}_{j}$$ 의 절대편차

            $$
            Z^{(i)}_{j}=\left\vert X^{(i)}_{j}-\overline{X}^{(i)} \right\vert
            $$

        - $\overline{Z}^{(i)}$ : $i$ 번째 집단에 대하여 그 절대편차 $$Z^{(i)}_{\forall}$$ 의 평균
        - $N$ : 표본 내 관측치 갯수

    - **F-Dist.($F(\nu_1, \nu_2)$)** : 서로 독립인 확률변수 $V_{1}\sim\chi^2(\nu_1),V_{2}\sim\chi^2(\nu_2)$ 간 비율로 구성되는 확률변수의 분포

        $$
        F=\frac{V_1/\nu_1}{V_2/\nu_2} \sim F(\nu_1,\nu_2)
        $$
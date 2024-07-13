---
order: 7
title: Summarize Statistical Method
date: 2024-06-23
categories: [Statistical Techs, Statistics]
tags: [Statistics]
math: true
image:
  path: /_post_refer_img/Statistics/Thumbnail.png
---

## Summary
-----

### 수치형 변수의 평균에 대한 추론

| 문제 | 관심모수 | 점추정량 | 가정체크 | 검정가설 | 검정방법 | Python Module |
|---|---|---|---|---|---|---|
| 단일 집단의 평균 | $\mu$ | $\bar{X}$ | $n>30$ or $X \sim N$ | $H_0: \mu=\mu_0$ | One Sample t-Test | `statsmodels.stats.ttest_mean` |
| 두 집단 간 평균 비교 <br> (독립표본) | $\mu_1-\mu_2$ | $$\bar{X}_{1} - \bar{X}_{2}$$ | $(n_1 + n_2)>30$ or $X_{1}\sim N, X_{2} \sim N$ | $H_0: \mu_1 - \mu_2 = 0$ | Two Sample t-Test | `statsmodels.stats.weightstats.ttest_ind` |
| 두 집단 간 평균 비교 <br> (쌍체표본)  | $\mu_d$ | $\bar{x}_d$ | $n>30$ or $X \sim N$ | $H_0: \mu_d=0$ | Paired t-Test | `statsmodels.stats.ttest_mean` |
| 셋 이상 그룹 간 평균 비교 | $\mu_1, \cdots, \mu_m$ |  $\bar{X}_1, \cdots, \bar{X}_m$ |  $n_i>30$ or $X_{i} \sim N$ <br> $\sigma_{i}^{2}=\sigma_{j}^{2}$ | $H_0: \mu_1 = \cdots = \mu_m$ | ANOVA | `statsmodels.stats.anova.AnovaRM` |
| 양적변수 간의 상관관계 | $\beta_0, \beta_1$ <br> $(y=\beta_0+\beta_1 x + \epsilon)$ | $\hat{\beta}_0, \hat{\beta}_1$ | 반응변수와 설명변수 간 선형성 <br> 설명변수 간 독립성 <br> 오차의 등분산성 <br> 오차의 정규성 | $H_0: \beta_i=0$ | Regression | `statsmodels.api.OLS` |

### 범주형 변수의 비율에 대한 추론

| 문제 | 관심모수 | 점추정량 | 가정체크 | 검정가설 | 검정방법 | Python Module |
|---|---|---|---|---|---|---|
| 단일 집단의 비율 | $\pi$ | $p$ | $np>5$ <br> $n(1-p)>5$ | $H_0: \pi=\pi_0$ | One Sample z-Test | `statsmodels.stats.proportion.proportions_ztest` |
| 두 집단 간 비율 비교 | $\pi_1 - \pi_2$ | $p_1 - p_2$ | $n_i p_i > 5$ <br> $n_i (1-p_i)>5$ | $H_0: \pi_1-\pi_2=0$ | Two Sample z-Test | `statsmodels.stats.proportion.proportions_ztest` |
| 적합성 검정 | $\pi_1, \cdots, \pi_m$ | $p_1, \cdots, p_m$ | $n_i p_i > 5$ <br> $n_i (1-p_i)>5$ | $H_0: \pi_1=p_{0}^{(1)}, \cdots, \pi_m=p_{0}^{(m)}$ | Chi-square test | `scipy.stats.chisquare` |
| 독립성 검정 | | | $n_i p_i > 5$ <br> $n_i (1-p_i)>5$ | $H_0:$ 두 범주형 변수가 독립 | Chi-square test | `scipy.stats.chi2_contingency` |
| 양적변수와의 상관관계 | $\beta_0, \beta_1$ <br> $(\pi=\beta_0+\beta_1 x)$ | $\hat{\beta}_0, \hat{\beta}_1$ | $Y \sim B$ | $H_0: \beta_i=0$ | Logistic regression | `sklearn.linear_models.LogisticRegression` |

## refer.
-----

### Shapiro-Wilk Test

### Levene’s Test
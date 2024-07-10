---
order: 4
title: Sample Dist.
date: 2024-06-20
categories: [Statistical Techs, Statistics]
tags: [Statistics]
math: true
image:
  path: /_post_refer_img/Statistics/Thumbnail.png
---

## Random Sample
-----

### Population & Sample

> 모수는 그 값이 알려져 있지 않은 고정된 수이다. 이 값을 추정하기 위하여 표본의 통계량을 사용하므로, 통계량은 모수의 추정량이라 할 수 있다. 그런데 모집단에서 어떤 표본을 추출하느냐에 따라 통계량의 실현값이 달라진다. 따라서 모수는 **상수(Constant)**, 통계량은 **확률변수(Random Variable)**라고 볼 수 있다.

- **모집단(Population)의 모수(Parameter)**
    - 모평균 : $\mu = E(X)$
    - 모분산 : $\sigma^2 = Var(X)$
    - 모표준편차 : $\sigma = \sqrt{Var(X)}$

- **표본(Sample)의 통계량(Statistic)**
    - 표본평균 : $\overline{X}$
    - 표본분산 : $S^2$
    - 표본표준편차 : $S$

### Random Sample

- 모집단으로부터 관측치 $X_1, X_2, X_3, \cdots, X_n$ 를 추출하여 구성한 표본에 대하여

    $$\begin{aligned}
    \{X_1, X_2, X_3, \cdots, X_N\}
    \end{aligned}$$

- 모집단의 각 개체가 표본의 원소로서 선택될 확률이 모두 같고,

    $$
    P(X_{i}=x_{i})=\frac{1}{N} \quad \text{for}\;i=1,2,\cdots,N
    $$

- 원소 $X_1, X_2, X_3, \cdots, X_n$ 이 모두 모집단의 분포를 따르는 확률변수이고,

    $$\begin{aligned}
    E(X_{i^{\forall}})&=\mu \\
    Var(X_{i^{\forall}})&=\sigma^2
    \end{aligned}$$

- 원소 $X_1, X_2, X_3, \cdots, X_n$ 이 모두 통계적으로 독립인 경우

    $$
    P(X_{j^{\forall}} \vert X_{i^{\forall}}) = P(X_{j^{\forall}})
    $$

## Sample Distribution
-----

### What? Sample Dist.

- **표본분석의 목적** : 모수 추정
    - 표본의 평균 $\overline{X}$ 가 모집단의 평균 $\mu$ 를 얼마나 잘 추정하는가
    - 확률변수 $\overline{X}$ 의 기대값 $E(\overline{X})$ 은 상수 $\mu$ 에 가까운가
    - 추정량 $\overline{X}$ 의 기대값 $E(\overline{X})$ 과 모수 $\mu$ 사이에는 얼마나 큰 추정오차가 존재하는가

- **추정량과 추정치의 정의**
    - **추정량(Estimator)** : 모수를 추정하는 값으로서 통계량(Statistics)
        - 모평균 $\mu$ 의 추정량 : 표본평균 $\overline{X}$
        - 모분산 $\sigma^2$ 의 추정량 : 표본분산 $S^2$
        - 모표준편차 $\sigma$ 의 추정량 : 표본표준편차 $S$

    - **추정치(Estimate)** : 특정 표본에서 얻어진 추정량의 실현값(Realized Value)

- **표본분포(Sampling Distribution)** : 모수에 대한 추정량의 확률분포
    - 모집단의 평균을 추정하기 위해 여러 표본을 뽑을 때 표본 평균의 추정치들의 분포
    - 모집단의 평균을 추정하기 위해 여러 표본을 뽑을 때 표본 비율의 추정치들의 분포

### Statistics

- **$\overline{X}$ 의 기대값** : $E\left[\overline{X}\right]=\mu$

    $$\begin{aligned}
    E\left[\overline{X}\right]
    &= E\left[\frac{1}{n}(X_1+X_2+X_3+\cdots+X_n)\right]\\
    &=\frac{1}{n}\bigg[E\left[X_1+X_2+X_3+\cdots+X_n\right]\bigg]\\
    &=\frac{1}{n}\bigg[E\left[X_1\right]+E\left[X_2\right]+E\left[X_3\right]+\cdots+E\left[X_n\right]\bigg]\\
    &=\frac{1}{n}(\mu + \cdots + \mu)\\
    &=\mu
    \end{aligned}$$

- **$\overline{X}$ 의 분산** : $Var\left[\overline{X}\right]=\displaystyle\frac{\sigma^2}{n}$

    $$\begin{aligned}
    Var\left[\overline{X}\right]
    &= Var\left[\frac{1}{n}(X_1+X_2+X_3+\cdots+X_n)\right]\\
    &=Var\left[\frac{1}{n}X_1\right]+Var\left[\frac{1}{n}X_2\right]+Var\left[\frac{1}{n}X_3\right]+\cdots+Var\left[\frac{1}{n}X_n\right]\\
    &(\because Cov\left[X_i, X_j\right]=0)\\
    &=\frac{1}{n^2}Var\left[X_1\right]+\frac{1}{n^2}Var\left[X_2\right]+\frac{1}{n^2}Var\left[X_3\right]+\cdots+\frac{1}{n^2}Var\left[X_n\right]\\
    &=\frac{1}{n^2}\sigma^2 + \frac{1}{n^2}\sigma^2 +\frac{1}{n^2}\sigma^2 + \cdots + \frac{1}{n^2}\sigma^2\\
    &=\frac{1}{n^2}(\sigma^2 + \cdots + \sigma^2)\\
    &=\frac{\sigma^2}{n}
    \end{aligned}$$

- **표준오차(Standard Error; $SE$)** : $\overline{X}$ 의 표준편차
    
    > 표본 $sample1, sample2, \cdots$ 에 의해 얻어진 추정량 $\overline{X}$ 의 실현값 $\overline{x_1}, \overline{x_2}, \overline{x_3}, \cdots$ 은 $\mu$ 를 기준으로 얼마나 널리 퍼져 있는가

    $$\begin{aligned}
    SE
    &=\frac{\sigma^2}{n}\\
    &=E\left[\vert\overline{x}_{i}-\mu\vert\right]
    \end{aligned}$$

    - $\overline{X}$ 의 표준편차는 모수 $\mu$ 와 그 추정치 $\overline{x}_{i}$ 의 차이의 평균임
    - $Var(\overline{X})$ 가 작을수록 모수 $\mu$ 에 근사하는 추정량 $\overline{X}$ 가 실현될 가능성이 높음

### Central Limit Theorem

- **중심극한정리(Central Limit Theorem; $CLT$)**

    > 평균이 $\mu$ 이고, 분산이 $\sigma^2$ 인 모집단에서 크기가 $n$ 인 표본을 추출하는 경우 $n$ 이 증가할수록 표본평균 $\overline{X}$ 의 분포는 평균이 $\mu$ 이고, 분산이 $\sigma^2$ 일 때의 가우시안 분포에 근사함

    $$
    \overline{X} \sim N(\mu, \frac{\sigma^2}{n}),\quad \text{s.t.}\,n > 30
    $$

    - $n \le 30$ 인 경우에는 모집단의 분포에 의존함
    - $n > 30$ 인 경우에는 모집단의 분포와 상관 없이 성립함

## Proportion
-----

### Population Proportion

- **모비율(Population Proportion; $\pi$)** : 모집단 중 특정 성질을 가지는 관측치 비율

    $$
    \pi \times 100\%
    $$

- **모비율에 대한 확률변수 정의** : 베르누이 확률변수

    $$
    X \sim Bernoulli(\pi)
    $$

    - 관측치 $X_i$ 가 성질을 만족하면 $1$, 만족하지 않으면 $0$ 이라고 하자

        $$
        X=
        \begin{cases}
        1\quad \text{with probability}\;\pi\\
        0\quad \text{with probability}\;1-\pi
        \end{cases}
        $$

    - 확률변수 $X$ 의 기대값

        $$\begin{aligned}
        E(X)
        &=\mu \\
        &=1\times\pi + 0\times(1-\pi) \\
        &=\pi
        \end{aligned}$$

    - 확률변수 $X$ 의 분산

        $$\begin{aligned}
        Var(X)
        &=\sigma^2 \\
        &=(1-\pi)^2\times\pi + (0-\pi)^2\times(1-\pi) \\
        &=\pi(1-\pi)
        \end{aligned}$$

### Sample Proportion

- **표본비율(Sample Proportion; $P$)** : 모비율에 대한 표본평균
    
    > 크기가 $n$ 인 표본을 추출할 때 모비율 $\pi$ 에 대한 표본평균 $P$ 는 다음과 같음

    $$\begin{aligned}
    P
    &= \overline{X} \\
    &= \frac{1}{n}\displaystyle\sum_{i=1}^{n}{X_i}
    \end{aligned}$$

- **표본비율의 분산 도출**

    $$\begin{aligned}
    &Var\left[\frac{1}{n}(X_1+X_2+\cdots+X_n)\right]\\
    &= Var\left[\frac{1}{n}X_1\right]+Var\left[\frac{1}{n}X_2\right]+\cdots+Var\left[\frac{1}{n}X_n\right]\\
    &= \frac{1}{n^2}Var\left[X_1\right]+\frac{1}{n^2}Var\left[X_2\right]+\cdots+\frac{1}{n^2}Var\left[X_n\right]\\
    &= \frac{1}{n^2}(\sigma^2+\sigma^2+\cdots+\sigma^2)\\
    &= \frac{1}{n^2}\times n\times \sigma^2\\
    &= \frac{\pi(1-\pi)}{n}
    \end{aligned}$$

- **표본비율에 대한 중심극한정리**

    > 표본의 크기 $n$ 이 충분히 크면 표본비율 $P$ 는 다음과 같은 분포를 따르게 됨

    $$
    P \sim N(\pi, \frac{\pi(1-\pi)}{n})
    $$

## Inference
-----

### 수치형 변수의 평균에 대한 추론

| 문제 | 관심모수 | 점추정량 | 가정체크 | 검정가설 | 검정방법 | Python Module |
|---|---|---|---|---|---|---|
| 단일 집단의 평균 | $\mu$ | $\bar{X}$ | $n>30$ or $X \sim N$ | $H_0: \mu=\mu_0$ | One-sample T-test | `statsmodels.stats.ttest_mean` |
| 두 집단 간 평균 비교 <br> (독립표본) | $\mu_1-\mu_2$ | $$\bar{X}_{1} - \bar{X}_{2}$$ | $(n_1 + n_2)>30$ or $X_{1}\sim N, X_{2} \sim N$ | $H_0: \mu_1 - \mu_2 = 0$ | Two-sample t-test | `statsmodels.stats.weightstats.ttest_ind` |
| 두 집단 간 평균 비교 <br> (쌍체표본)  | $\mu_d$ | $\bar{x}_d$ | $n>30$ or $X \sim N$ | $H_0: \mu_d=0$ | Paired t-test | `statsmodels.stats.ttest_mean` |
| 셋 이상 그룹 간 평균 비교 | $\mu_1, \cdots, \mu_m$ |  $\bar{X}_1, \cdots, \bar{X}_m$ |  $n_i>30$ or $X_{i} \sim N$ <br> $\sigma_{i}^{2}=\sigma_{j}^{2}$ | $H_0: \mu_1 = \cdots = \mu_m$ | ANOVA | `statsmodels.stats.anova.AnovaRM` |
| 양적변수 간의 상관관계 | $\beta_0, \beta_1$ <br> $(y=\beta_0+\beta_1 x + \epsilon)$ | $\hat{\beta}_0, \hat{\beta}_1$ | 반응변수와 설명변수 간 선형성 <br> 설명변수 간 독립성 <br> 오차의 등분산성 <br> 오차의 정규성 | $H_0: \beta_i=0$ | Regression | `statsmodels.api.OLS` |

### 범주형 변수의 비율에 대한 추론

| 문제 | 관심모수 | 점추정량 | 가정체크 | 검정가설 | 검정방법 | Python Module |
|---|---|---|---|---|---|---|
| 단일 집단의 비율 | $\pi$ | $p$ | $np>5$ <br> $n(1-p)>5$ | $H_0: \pi=\pi_0$ | Z-test | `statsmodels.stats.proportion.proportions_ztest` |
| 두 집단 간 비율 비교 | $\pi_1 - \pi_2$ | $p_1 - p_2$ | $n_i p_i > 5$ <br> $n_i (1-p_i)>5$ | $H_0: \pi_1-\pi_2=0$ | Z-test | `statsmodels.stats.proportion.proportions_ztest` |
| 적합성 검정 | $\pi_1, \cdots, \pi_m$ | $p_1, \cdots, p_m$ | $n_i p_i > 5$ <br> $n_i (1-p_i)>5$ | $H_0: \pi_1=p_{0}^{(1)}, \cdots, \pi_m=p_{0}^{(m)}$ | Chi-square test | `scipy.stats.chisquare` |
| 독립성 검정 | | | $n_i p_i > 5$ <br> $n_i (1-p_i)>5$ | $H_0:$ 두 범주형 변수가 독립 | Chi-square test | `scipy.stats.chi2_contingency` |
| 양적변수와의 상관관계 | $\beta_0, \beta_1$ <br> $(\pi=\beta_0+\beta_1 x)$ | $\hat{\beta}_0, \hat{\beta}_1$ | $Y \sim B$ | $H_0: \beta_i=0$ | Logistic regression | `sklearn.linear_models.LogisticRegression` |
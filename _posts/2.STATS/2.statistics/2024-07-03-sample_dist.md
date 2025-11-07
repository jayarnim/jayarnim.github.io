---
order: 3
title: Sample Dist.
date: 2024-07-03
categories: [2.STATISTICAL TECHS, 2.statistics]
tags: [statistics, sample, sample distribution]
math: true
description: >-
    Based on the following lectures <br>
    (1) “Statistics (2018-1)” by Prof. Sang Ah Lee, Dept. of Economics, College of Economics & Commerce, Kookmin Univ. <br>
    (2) "Statistical Models and Application (2024-1)" by Prof. Yeo Jin Chung, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
    path: /_post_refer_img/2.STATS/2.statistics/Thumbnail.png
---

## Sample Analysis
-----

- **표본 분석(Sample Analysis)** : 전체 모집단에서 일부 표본을 추출하여 분석하고, 이를 통해 전체 모집단의 특성(모수)을 추론하는 통계적 방법
    - 표본의 평균 $\overline{X}$ 이 모집단의 평균 $\mu$ 를 얼마나 잘 추정하는가
    - 확률변수 $\overline{X}$ 의 기대값 $\mathbb{E}\left[\overline{X}\right]$ 은 상수 $\mu$ 에 가까운가
    - 추정량 $\overline{X}$ 의 기대값 $\mathbb{E}\left[\overline{X}\right]$ 과 모수 $\mu$ 사이에는 얼마나 큰 추정오차가 존재하는가

- **모수 추정량과 추정치**

    > 모수는 그 값이 알려져 있지 않은 고정된 수이다. 이 값을 추정하기 위하여 표본의 통계량을 사용하므로, 통계량은 모수의 추정량이라 할 수 있다. 그런데 모집단에서 어떤 표본을 추출하느냐에 따라 통계량의 실현값이 달라진다. 따라서 **모수는 상수(Constant), 통계량은 확률변수(Random Variable)** 라고 볼 수 있다.

    - **추정량(Estimator)** : 모수를 추정하는 값으로서 표본의 통계량(Statistics)

        $$\begin{aligned}
        \hat{\mu}
        = \overline{X}
        = \frac{1}{n}\sum_{i=1}^{n}{X_{i}}
        \end{aligned}$$

    - **추정치(Estimate)** : 특정 표본에서 얻어진 추정량의 실현값(Realized Value)

        $$\begin{aligned}
        \hat{\mu}_{k}
        = \overline{x}_{k}
        = \frac{1}{\vert \Omega_{k} \vert}\sum_{i \in \Omega_{k}}{x_{i}}
        \end{aligned}$$

## Sampling Distribution
-----

- **표본분포(Sampling Distribution)** : 모수 추정량의 확률분포로서 주로 모평균 $\mu$ 의 추정량 $\overline{X}$ 의 분포에 관하여 논의함

$$\begin{aligned}
\overline{X} \sim \mathcal{N}(\mu,\frac{\sigma^{2}}{n}) \quad \text{s.t.} \quad n>30
\end{aligned}$$

- 표본평균 $\overline{X}$ 의 기대값:

    $$\begin{aligned}
    \mathbb{E}\left[\overline{X}\right]
    &= \mathbb{E}\left[\frac{1}{n}(X_{1}+X_{2}+\cdots+X_{n})\right]\\
    &=\frac{1}{n}\left(\mathbb{E}\left[X_{1}+X_{2}+\cdots+X_{n}\right]\right)\\
    &=\frac{1}{n}\left(\mathbb{E}\left[X_{1}\right]+\mathbb{E}\left[X_{2}\right]+\cdots+\mathbb{E}\left[X_{n}\right]\right)\\
    &=\frac{1}{n}\left(\mu + \mu + \cdots + \mu \right)\\
    &=\mu
    \end{aligned}$$

- 표본평균 $\overline{X}$ 의 분산:

    $$\begin{aligned}
    \mathrm{Var}\left[\overline{X}\right]
    &= \mathrm{Var}\left[\frac{1}{n}(X_{1}+X_{2}+\cdots+X_{n})\right]\\
    &=\mathrm{Var}\left[\frac{1}{n}X_{1}\right]+\mathrm{Var}\left[\frac{1}{n}X_{2}\right]+\cdots+\mathrm{Var}\left[\frac{1}{n}X_{n}\right] 
    \quad \because \mathrm{Cov}\left[\overline{x}_i, \overline{x}_j\right]=0\\
    &=\frac{1}{n^2}\mathrm{Var}\left[X_{1}\right]+\frac{1}{n^2}\mathrm{Var}\left[X_{2}\right]+\cdots+\frac{1}{n^2}\mathrm{Var}\left[X_{n}\right]\\
    &=\frac{1}{n^2}\sigma^2 + \frac{1}{n^2}\sigma^2 + \cdots + \frac{1}{n^2}\sigma^2\\
    &=\frac{1}{n^2}(\sigma^2 + \cdots + \sigma^2)\\
    &=\frac{\sigma^2}{n}
    \end{aligned}$$

- **표준오차(Standard Error)** : $\overline{X}$ 의 표준편차

    $$\begin{aligned}
    \mathrm{SE}
    =\sqrt{\frac{\sigma^2}{n}}
    =\mathbb{E}\left[\vert\overline{X}-\mu\vert\right]
    \end{aligned}$$

## Central Limit Theorem
-----

- **큰 수의 법칙(`L`aw of `L`arge `N`umbers)**: 표본의 수가 증가할수록, 그 표본의 평균은 모집단의 기댓값에 수렴한다는 법칙

    > 무작위 표본 $X_{1},X_{2},\cdots,X_{n}$ 이 동일한 분포를 따르고, 그 기대값 $\mathbb{E}\left[X_{i}\right]=\mu$ 일 때, 표본평균 $\overline{X}$ 은 모평균 $\mu$ 에 수렴함

    $$\begin{aligned}
    \overline{X}_{n}=\frac{1}{n}\sum_{i=1}^{n}{X_{i}} \to \mu \quad (n \to \infty)
    \end{aligned}$$

- **중심극한정리(`C`entral `L`imit `T`heorem)**: 표본의 수가 증가할수록, 그 표본의 평균의 분포가 가우시안 분포에 근사한다는 정리

    > 평균이 $\mu$ 이고, 분산이 $\sigma^2$ 인 모집단에서 크기가 $n$ 인 표본을 추출하는 경우 $n$ 이 증가할수록 표본평균 $\overline{X}$ 의 분포는 가우시안 분포 $\mathcal{N}(\mu,\sigma^{2}/n)$ 에 근사함

    $$\begin{aligned}
    \overline{X} \sim \mathcal{N}(\mu, \frac{\sigma^2}{n}) \quad \text{s.t.} \quad n > 30
    \end{aligned}$$
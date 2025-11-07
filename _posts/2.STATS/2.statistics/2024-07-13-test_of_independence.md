---
order: 13
title: Test of Independence
date: 2024-07-13
categories: [2.STATISTICAL TECHS, 2.statistics]
tags: [statistics, design of experiments, a/b test, chi-squared test, test of independence, chi-squared distribution]
math: true
description: >-
    Based on the following lectures <br>
    (1) “Statistics (2018-1)” by Prof. Sang Ah Lee, Dept. of Economics, College of Economics & Commerce, Kookmin Univ. <br>
    (2) "Statistical Models and Application (2024-1)" by Prof. Yeo Jin Chung, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
    path: /_post_refer_img/2.STATS/2.statistics/Thumbnail.png
---

## Test of Independence
-----

- **독립성 검정(Test of Independence)** : 두 범주형 자료가 통계적으로 독립인지 검정하는 방법

    > 맥주 회사 Alber's 에서는 라이트 맥주, 일반 맥주, 흑 맥주를 생산하여 유통한다. 이 기업의 시장조사팀은 성별에 따라 선호하는 맥주에 차이가 있는지 알아보고자 한다. 만약 맥주의 품종별 선호도가 성별에 독립적이라면 맥주광고는 모든 고객에 대해 획일적으로 이루어질 것이다. 반면, 품종별 선호도가 성별에 의존적이라면 세분 시장의 목표 고객에 따라 상이한 촉진 전략을 수행해야 할 것이다. 아래 분할표는 무작위 추출된 $150$ 명이 각 맥주에 대해 시음한 후 응답한 품종별 선호도이다. 맥주의 품종별 선호도는 성별에 대하여 독립적이라 볼 수 있는가?

- 가설(Hypothesis) 설정:
    - $H_{0}:\quad$ 품종별 선호도($Y$)는 성별 선호도($X$)에 대하여 독립적이다.
    - $H_{1}:\quad$ 품종별 선호도($Y$)는 성별 선호도($X$)에 대하여 독립적이라 볼 수 없다.

- 검정통계량(Test Statistic):

    $$\begin{aligned}
    X \sim \chi^{2}(\nu)
    \end{aligned}$$

    - $\nu=(k-1)(l-1)$
    - $k$ : 변수 $X$ 의 카테고리 갯수
    - $l$ : 변수 $Y$ 의 카테고리 갯수

## Test Statistic
-----

$$\begin{aligned}
X
&= \sum_{i=1}^{k}\sum_{j=1}^{l}{Z_{i,j}^2}
\end{aligned}$$

- $Z_{i,j}$ : 각 셀에 대하여 관측 빈도와 기대 빈도의 표준화된 차이

    $$\begin{aligned}
    Z_{i,j}=\frac{\Omega_{i,j} - e_{i,j}}{\sqrt{e_{i,j}}} \sim N(0,1)
    \end{aligned}$$

- $\Omega_{i,j}$ : 변수 $X$ 의 $i$ 번째 카테고리와 변수 $Y$ 의 $j$ 번째 카테고리에 해당하는 관측치의 관측 빈도

    | 품종 | 라이트 | 일반 | 흑 | 계 |
    |:-:|:-:|:-:|:-:|:-:|
    | 남성 | 20 | 40 | 20 | 80 |
    | 여성 | 30 | 30 | 10 | 70 |
    | 계 | 50 | 70 | 10 | 150 |

- $e_{i,j}$ : $\Omega_{i,j}$ 의 기대값으로서 귀무가설이 참일 때 기대되는 빈도

    | 품종 | 라이트 | 일반 | 흑 |
    |:-:|:-:|:-:|:-:|
    | 남성 | 26.67 | 37.33 | 16.00 |
    | 여성 | 23.33 | 32.67 | 14.00 |

    $$\begin{aligned}
    e_{i,j}
    &= \mathbb{E}\left[\Omega_{i,j} \right]\\
    &=n \cdot p_{i,j}\\
    &=n \cdot P(X_{i} \cap Y_{j})\\
    &=n \cdot P(X_{i})P(Y_{j}) \quad \left(\because P(Y_{j} \mid X_{i})=P(Y_{j})\right)
    \end{aligned}$$

- $\sqrt{e_{i,j}}$ : $\Omega_{i,j}$ 에 대한 표준편차의 근사값

    $$\begin{aligned}
    \mathrm{Var}\left[\Omega_{i,j}\right]
    &= n \cdot p_{i,j} \cdot (1-p_{i,j})\\
    &= e_{i,j} \cdot (1-p_{i,j})\\
    &\approx e_{i,j} \cdot 1
    \end{aligned}$$
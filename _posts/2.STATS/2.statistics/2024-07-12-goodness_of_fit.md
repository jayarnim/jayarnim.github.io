---
order: 12
title: Goodness of Fit Test
date: 2024-07-12
categories: [2.STATISTICAL TECHS, 2.statistics]
tags: [statistics, design of experiments, a/b test, chi-squared test, goodness-of-fit test, chi-squared distribution]
math: true
description: >-
    Based on the following lectures <br>
    (1) “Statistics (2018-1)” by Prof. Sang Ah Lee, Dept. of Economics, College of Economics & Commerce, Kookmin Univ. <br>
    (2) "Statistical Models and Application (2024-1)" by Prof. Yeo Jin Chung, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
    path: /_post_refer_img/2.STATS/2.statistics/Thumbnail.png
---

## Goodness-of-Fit Test
-----

- **적합성 검정(Goodness-of-Fit Test)** : 범주형 자료에 대하여 관찰된 비율이 기대되는 비율과 통계적으로 유의한 차이가 있는지 검정하는 방법

    > 마케팅 조사 기관 Scott 가 수행한 시장 점유율에 대한 조사에서, 몇 년동안 시장점유율은 A사 $30\%$, B사 $50\%$, C사 $20\%$ 수준을 보이며 안정적이었다. 최근에 C사는 기능이 향상된 제품을 출시하였다. 이에 신제품의 출시가 시장점유율의 변화에 영향을 미치고 있는지 파악하고자 한다. Scott 가 $200$ 명의 고객을 소비자 패널로 활용하여 조사를 수행한 결과, 아래의 표와 같은 구매 선호도를 얻었다. 신제품 출시에 따라 시장점유율이 변화했다고 볼 수 있는가?

- 모수(Parameter) 정의:

    $$\begin{aligned}
    \pi_{A},\quad \pi_{B},\quad \pi_{C}
    \end{aligned}$$

- 점 추정량(Point Estimator) 도출:

    $$\begin{aligned}
    p_{A},\quad p_{B},\quad p_{C}
    \end{aligned}$$

- 가설(Hypothesis) 설정:
    - $H_{0}:\quad \pi_{A}=0.3 \; \text{and} \; \pi_{B}=0.5 \; \text{and} \; \pi_{C}=0.2$
    - $H_{1}:\quad \pi_{A} \ne 0.3 \; \text{or} \; \pi_{B} \ne 0.5 \; \text{or} \; \pi_{C} \ne 0.2$

- 검정통계량(Test Statistic):

    $$\begin{aligned}
    X \sim \chi^2{(\nu)}
    \end{aligned}$$

    - $\nu=k-1$
    - $k$: 카테고리 갯수

## Test Statistic
-----

$$\begin{aligned}
X
&= \sum_{i=1}^{k}{Z_{i}^{2}}
\end{aligned}$$

- $Z_{i}$ : 각 셀에 대하여 관측 빈도와 기대 빈도의 표준화된 차이

    $$\begin{aligned}
    Z_{i}
    =\frac{\Omega_{i} - e_{i}}{\sqrt{e_{i}}}
    \sim \mathcal{N}(0,1)
    \end{aligned}$$

- $\Omega_{i}$ : $i$ 번째 카테고리에 해당하는 관측치의 관측 빈도

    | 회사 | A | B | C | 계 |
    |:-:|:-:|:-:|:-:|:-:|
    | 관측 빈도 | 48 | 98 | 54 | 200 |

- $e_{i}$: $\Omega_{i}$ 의 기대값으로서 귀무가설이 참일 때 기대되는 빈도

    | 회사 | A | B | C |
    |:-:|:-:|:-:|:-:|
    | 기대 빈도 | 60 | 100 | 40 |

    $$\begin{aligned}
    e_{i}
    =\mathbb{E}\left[\Omega_{i} \right]
    = n \cdot p_{i}
    \end{aligned}$$

- $\sqrt{e_{i}}$: $\Omega_{i}$ 에 대한 표준편차의 근사값

    $$\begin{aligned}
    \mathrm{Var}\left[\Omega_{i}\right]
    &= n \cdot p_{i} \cdot (1-p_{i})\\
    &= e_{i} \cdot (1-p_{i})\\
    &\approx e_{i} \cdot 1
    \end{aligned}$$
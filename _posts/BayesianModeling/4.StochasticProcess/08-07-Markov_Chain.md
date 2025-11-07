---
order: 7
title: Markov Chain
date: 2025-08-07
categories: [BAYES, 4.stochastic process]
tags: [Stochastic Process, Time Series, Markov Chain, Hidden Markov Model]
math: true
image:
    path: /_post_refer_img/BayesianModeling/4.StochasticProcess/Thumbnail.jpg
---

## Markov Chain
-----

- **마르코프 체인(`M`arkov `C`hain)** : 어떤 시스템에 대하여 해당 시스템이 상태 공간 $S$ 에서 이산적인 시점($t=0,1,2,\cdots$)에서만 상태 전이가 발생한다고 했을 때, 이 시스템이 마르코프 성질을 만족한다면, 이 시스템은 마르코프 체인이라고 볼 수 있음

    - **마르코프 성질** : 미래의 상태가 현재 상태에만 의존하며 과거의 상태는 고려하지 않는 성질

        $$\begin{aligned}
        P(X_{n+1}=j \mid X_{n}=i,X_{n-1}=i_{n-1},\cdots,X_{0}=i_{0}) = P(X_{n+1}=j \mid X_{n}=i)
        \end{aligned}$$

        - $X_{n}$ : 시점 $n$ 에서 시스템이 취하는 상태
        - $i,j \in S$ : 특정 상태

- **전이확률행렬(Transition Probability Matrix)** : 각 상태에서 다른 상태로의 전이 확률을 나타내는 행렬

    $$
    \mathbf{P}_{n \times n} = \{p_{i,j} \mid i,j \in n, p_{i,j} \in S\}
    $$

    - $p_{i,j} \in S$ : 상태 $i$ 에서 $j$ 로의 전이확률

        - $0 \le p_{i,j} \le 1$
        - $\sum_{j}{p_{i,j}}=1$ : 상태 $i$ 에서 다른 상태로 전이될 확률의 합은 1임

- **정상확률(Steady-State Probability; $\pi_{j}$)** : 마르코프 체인이 장기적으로 상태 $j$ 를 취할 확률

    $$
    \pi_{j}=\sum_{i}{\pi_{i}\cdot p_{i,j}}
    $$

    - 상태 $j$ 의 정상확률 $\pi_{j}$ 는 상태 $i$ 에서 $j$ 로 전이할 확률의 기대값($E(x)=\sum{x\cdot P(x)}$)임

- **정상확률분포(Steady-State Probability Distribution; $\Pi$)** : 마르코프 체인이 각 상태를 취할 확률이 시간에 따라 변하지 않고 일정하게 유지되는, 장기적인 확률 분포

    $$
    \Pi=\Pi\cdot\mathbf{P}
    $$
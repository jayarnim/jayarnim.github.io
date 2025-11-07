---
order: 1
title: Uncertainty and Probability
date: 2025-07-01
categories: [2.STATISTICAL TECHS, 1.probability]
tags: [statistics, uncertainty, probability, distribution]
math: true
description: >-
    Based on the following lectures <br>
    (1) “Statistics (2018-1)” by Prof. Sang Ah Lee, Dept. of Economics, College of Economics & Commerce, Kookmin Univ. <br>
    (2) "Statistical Models and Application (2024-1)" by Prof. Yeo Jin Chung, Dept. of Data Science, The Grad. School, Kookmin Univ. <br>
    (3) “Bayesian Modeling (2024-1)” by Prof. Yeo Jin Chung, Dept. of AI, Big Data & Management, College of Business Administration, Kookmin Univ.
image:
  path: /_post_refer_img/2.STATS/1.probability/Thumbnail.jpg
---


## uncertainty
-----

- **불확실성(Uncertainty)**: 어떠한 사건의 결과에 대하여 사전에 확신할 수 없는 상태
    - **우발적 불확실성(Aleatoric Uncertainty)**: 관측치에 내재된 잡음 혹은 무작위성으로 인해 발생하는 불확실성

- **인식적 불확실성(Epistemic Uncertainty)**: 정보 불완전성으로 인하여 발생하는 불확실성
    - **정보 불완전성(Data Uncertainty)**: 관측 데이터가 불완전하거나(Incomplete), 불충분하거나(Insufficient), 왜곡된(Distorted) 상황
    - **파라미터 불확실성(Parameter Uncertainty)**: 주어진 모형 안에서 최적 파라미터를 유일하게 식별할 수 없는 문제
    - **구조적 불확실성(Structural Uncertainty)**: 데이터 생성 메커니즘을 기술하는 함수 구조를 확신할 수 없어 특정 모형을 가정할 수 없는 문제
    - **표현의 불확실성(Latent Representation Uncertainty)**: 잠재공간의 비식별성으로 인해 치역(관측값)만으로 정의역(잠재요인)을 유일하게 결정하여 표현할 수 없는 문제

- **존재론적 불확실성(Ontic Uncertainty)**: 모형이 모사하고자 하는 실제 메커니즘이 본질적으로 불확실하여 정보가 증가하더라도 제거될 수 없는 불확실성

## probability
-----

- **확률실험(Random Experiment)** : 사건의 불확실성을 가진 프로세스
    - **표본공간(Sample Space)** : 확률실험에서 발생 가능한 모든 결과의 집합 (e.g. 동전 던지기)

        $$
        \Omega=\{H,T\}
        $$

    - **사건(Event)** : 표본공간의 부분집합으로서 발생 가능한 결과의 일부 (e.g. 동전을 한 번 던졌을 때 앞면이 나오는 사건)

        $$
        A=\{H\}\in\mathcal{F}
        $$

    - **확률(Probability)**: 사건의 불확실성을 정량화하기 위한 도구로서, 표본공간 $\Omega$ 위에 정의된 시그마대수 $\mathcal{F}:=\sigma(\Omega)$ 에 대하여 그 원소 $A$, 즉 사건이 발생할 상대적 가능성

        $$
        P(A)\quad\text{s.t.}\quad 0 \le P(A) \le 1
        $$

- **확률의 고전적 접근법** : 확률실험의 대칭성(Symmetric Nature)을 이용하여 각 결과가 발생할 가능성을 논리적으로 추론하는 방법
    - 어떤 확률실험이 발생 가능성이 동일한(Equally Likely) $n$ 개의 결과를 가질 때, 단순 사건이 발생할 확률은 $1/n$ 임
    - $n$ 개의 결과 중 $n_A$ 개 결과를 취하는 복합 사건이 발생할 확률은 $n_{A}/n$ 임

- **확률의 경험적 접근법** : 반복 실험 결과를 근거로 확률을 부여하는 방법으로서 빈도적 접근법
    - 어떤 확률실험을 $n$ 번 반복했을 때, 어떤 결과가 $k \le n$ 번 발생했다면 그 결과가 발생할 확률은 $k/n$ 임
    - 실험 횟수가 매우 크고, 모든 실험이 동일한 환경에서 이루어졌을 때 정당성을 가짐

- **확률의 주관적 접근법** : 고전적 접근법, 경험적 접근법에 의해 확률을 부여하는 것이 불가능한 경우 개인적인 판단에 의해 확률을 부여하는 방법

## axioms and laws
-----

- **확률의 공리(Axioms of Probability)**:
    - 비음성 공리(non-negativity):

        $$
        P(A) \ge 0
        $$

    - 정규화 공리(normalization):

        $$
        P(\Omega)=1
        $$

    - 가산성 공리(countable additivity / σ-additivity):

        $$
        A_i \cap A_j=\emptyset\Rightarrow P\left(\bigcup_{i=1}^{n}{A_{i}}\right)=\sum_{i=1}^{n}{A_{i}}
        $$

- **확률 법칙(Laws of Probability)**:
    - 여집합 법칙(complement rule):

        $$
        P(A^{C})=1-P(A)
        $$

    - 단조성 법칙(monotonicity):

        $$
        A\subseteq B\Rightarrow P(A)\le P(B)
        $$

    - 차집합 법칙:

        $$
        P(B\setminus A)=P(B)-P(A\cap B)
        $$

    - 포함-배제 법칙(inclusion–exclusion):

        $$
        P(A\cup B)=P(A)+P(B)-P(A\cap B)
        $$

    - 유한 가법성 법칙(finite additivity):

        $$
        A\cap B=\emptyset\Rightarrow P(A\cup B)=P(A)+P(B)
        $$

    - 증가열의 연속성 법칙(continuity of increasing sequence):

        $$
        A_{1}\subseteq A_{2}\subseteq\cdots,\quad\bigcup_{n=1}^{\infty}{A_{n}}=A\Rightarrow\lim_{n\to\infty}{P(A_{n})}=P(A)
        $$

    - 감소열의 연속성 법칙(continuity of decreasing sequence):

        $$
        A_{1}\supseteq A_{2}\supseteq\cdots,\quad\bigcap_{n=1}^{\infty}{A_{n}}=A\Rightarrow\lim_{n\to\infty}{P(A_{n})}=P(A)
        $$

    - 전체 확률 법칙(total probability):

        $$
        P(A)=\sum_{i}{P(A\mid B_{i})P(B_{i})}
        $$

    - 베이즈 법칙(bayes):

        $$
        P(A\mid B)=\frac{P(B\mid A)P(A)}{P(B)}
        $$

## statistical independence
-----

- **결합 확률(Joint Probability)**: 확률 변수 $A, B$ 에 대하여 그 실현값 $A_i \in A$ 와 $B_j \in B$ 가 동시에 발생할 확률

    $$
    P(A_i \cap B_j)
    $$

- **결합확률표**: 상호배타적이고($$X_{i}\cap X_{j}=\emptyset$$) 집단전체적인($$\bigcup_{i}{X_{i}}=\Omega$$) 사건들에 대한 확률 변수 $$A,B$$ 에 대하여 사건 $$A_{i},B_{j}$$ 가 동시에 발생할 결합 확률을 요약한 표

    | | $B_1$ | $B_2$ | $\cdots$ | $B_m$ | $\sum_{j=1}^{m}P(A_i \cap B_j)$ |
    |---|---|---|---|---|---|
    | $A_1$ | $P(A_1 \cap B_1)$ | $P(A_1 \cap B_2)$ | $\cdots$ | $P(A_1 \cap B_m)$ | $P(A_1)$ |
    | $A_2$ | $P(A_2 \cap B_1)$ | $P(A_2 \cap B_2)$ | $\cdots$ | $P(A_2 \cap B_m)$ | $P(A_2)$ |
    | $\vdots$ | $\vdots$ | $\vdots$ | $\ddots$ | $\vdots$ | $\vdots$ |
    | $A_n$ | $P(A_n \cap B_1)$ | $P(A_n \cap B_2)$ | $\cdots$ | $P(A_n \cap B_m)$ | $P(A_n)$ |
    | $\sum_{i=1}^{n}P(A_i \cap B_j)$ | $P(B_1)$ | $P(B_2)$ | $\cdots$ | $P(B_m)$ | $1$ |

- **조건부 확률(Conditional Probability)**: 사건 $B$ 가 발생했을 때 사건 $A$ 가 발생할 확률

    $$
    P(A\mid B)=\frac{P(A\cap B)}{P(B)}
    $$

- **통계적 독립성(Statistical Independence)**: 한 사건의 발생 여부가 다른 사건이 발생할 가능성에 아무런 영향을 끼치지 못하는 경우 혹은 한 사건에 관한 정보가 다른 사건에 관한 정보를 추가적으로 제공하지 못하는 경우

    $$
    P(A\mid B)=P(A)\Rightarrow A\perp B
    $$
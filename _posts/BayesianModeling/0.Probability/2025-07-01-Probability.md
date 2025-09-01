---
order: 1
title: Probability
date: 2025-07-01
categories: [BAYES, 0.probability]
tags: [Statistics]
math: true
description: >-
    Based on the following lectures <br>
    (1) “Statistics (2018-1)” by Prof. Sang Ah Lee, Dept. of Economics, College of Economics & Commerce, Kookmin Univ. <br>
    (2) "Statistical Models and Application (2024-1)" by Prof. Yeo Jin Chung, Dept. of Data Science, The Grad. School, Kookmin Univ. <br>
    (3) “Bayesian Modeling (2024-1)” by Prof. Yeo Jin Chung, Dept. of AI, Big Data & Management, College of Business Administration, Kookmin Univ.
image:
  path: /_post_refer_img/BayesianModeling/0.Probability/Thumbnail.jpg
---

## Probability
-----

### Random Experiment

- **확률실험(Random Experiment)** : 사건의 불확실성을 가진 프로세스
    - **사건의 불확실성** : **결과(Outcome)**를 사전에 알 수 없는 성질

- **표본공간(Sample Space)** : 확률실험에서 발생 가능한 모든 결과의 집합
    - 동전 던지기
        
        $$
        S = \{H, T\}
        $$
    
    - 주사위 던지기

        $$
        S = \{1, 2, 3, 4, 5, 6\}
        $$

    - 전구의 수명

        $$
        S = \{x \in R \,|\, x \ge 0\}
        $$
    
    - 올해 순 이익

        $$
        S = R
        $$

- **사건(Event)** : 표본공간의 부분집합으로서 발생 가능한 결과의 일부
    - **단순 사건(Simple Event)** : 어떤 결과 하나만으로 이루어진 사건
        - 동전을 한 번 던졌을 때 앞면이 나오는 사건

            $$
            E=\{H\}
            $$

        - 주사위를 한 번 던졌을 때 3이 나오는 사건

            $$
            E=\{3\}
            $$
    
    - **복합 사건(Compound Event)** : 두 개 이상의 결과로 이루어진 사건
        - 동전을 두 번 던졌을 때 서로 다른 면이 나오는 사건

            $$
            E=\{HT, TH\}
            $$
        
        - 주사위를 한 번 던졌을 때 짝수가 나오는 사건

            $$
            E=\{2,4,6\}
            $$

### Probability

- **확률(Probability)** : 주어진 표본공간 $S$ 에 대하여 그 사건 $A$ 가 발생할 상대적 가능성
    
    $$
    P(A),\quad \text{s.t.}\;0 \le P(A) \le 1
    $$

- **확률 부여 방법**
    - **고전적 접근법** : 확률실험의 대칭성(Symmetric Nature)을 이용하여 각 결과가 발생할 가능성을 논리적으로 추론하는 방법
        - 어떤 확률실험이 발생 가능성이 동일한(Equally Likely) $n$ 개의 결과를 가질 때, 단순 사건이 발생할 확률은 $\displaystyle\frac{1}{n}$ 임
        - $n$ 개의 결과 중 $n_A$ 개 결과를 취하는 복합 사건이 발생할 확률은 $\displaystyle\frac{n_A}{n}$ 임
    
    - **상대 빈도 접근법** : 반복되는 경험에 따라 확률을 부여하는 방법으로서 경험적 접근법
        - 어떤 확률실험을 $n$ 번 반복했을 때, 어떤 결과가 $k \le n$ 번 발생했다면 그 결과가 발생할 확률은 $\displaystyle\frac{k}{n}$ 임
        - 실험 횟수가 증가할수록 정확도가 높아짐
        - 실험 횟수가 매우 크고, 모든 실험이 동일한 환경에서 이루어졌을 때 정당성을 가짐
    
    - **주관적 접근법** : 고전적 접근법, 상대 빈도 접근법에 의해 확률을 부여하는 것이 불가능한 경우 개인적인 판단에 의해 확률을 부여하는 방법

- **확률의 공리(Axioms of Probability)**

    > 주어진 표본공간 $S$ 에 대하여 그 사건 $A_i\,(i=1,2,\cdots n)$ 는 다음을 만족해야 함

    - $P(S)=1$
    - $0 \le P(A_i) \le 1$
    - $A_1, A_2, \cdots, A_n$ 이 상호배타적이라면 $P(A_1 \cup A_2 \cup A_3 \cup \cdots \cup A_n)=P(A_1)+P(A_2)+P(A_3)+\cdots +P(A_n)$
        - **상호배타성(Mutually Exclusive or Disjoint)**
            
            $$
            A_i \cap A_j = \phi
            $$

- **확률 법칙**

    > 주어진 표본공간 $S$ 에 대하여 그 사건 $A_i\,(i=1,2,\cdots n)$ 는 다음을 만족함
        
    - $P(\phi)=0$
    - $$P(A_i')=1-P(A_i)$$, $$A_i'=\{x \in S \vert x \notin A_i \}$$
    - $A_i\subseteq A_j \Rightarrow P(A_i) \le P(A_j)$
    - $P(A_i \cup A_j)=P(A_i) + P(A_j) - P(A_i \cap A_j)$
    - $A_1, A_2, \cdots, A_n$ 이 집단전체적이라면 $P(A_1 \cup A_2 \cup A_3 \cup \cdots \cup A_n)=1$
        - **집단전체성(Collectively Exhaustive)**

            $$
            A_1 \cup A_2 \cup A_3 \cup \cdots \cup A_n = S
            $$

### Joint Probability

- **결합 확률(Joint Probability)** : 확률변수 $A, B$ 에 대하여 그 값 $A_i \in A$ 와 $B_j \in B$ 가 동시에 발생할 확률

    $$
    P(A_i \cap B_j)
    $$

- **결합확률표**

    > 표본공간 $S$ 에 대하여 확률변수 $A=\{A_1, A_2, A_3, \cdots, A_i, \cdots, A_n\}$ 를 상호배타적이고 집단전체적인 사건들의 집합이라고 하자. 또한 확률변수 $B=\{B_1, B_2, B_3, \cdots, B_j, \cdots, B_m\}$ 를 또 다른 상호배타적이고 집단전체적인 사건들의 집합이라고 하자. 이때 사건 $A_i, B_j$ 가 동시에 발생할 결합 확률 $P(A_i \cap B_j)$ 는 다음의 표와 같다.

    | | $B_1$ | $B_2$ | $\cdots$ | $B_m$ | $\sum_{j=1}^{m}P(A_i \cap B_j)$ |
    |---|---|---|---|---|---|
    | $A_1$ | $P(A_1 \cap B_1)$ | $P(A_1 \cap B_2)$ | $\cdots$ | $P(A_1 \cap B_m)$ | $P(A_1)$ |
    | $A_2$ | $P(A_2 \cap B_1)$ | $P(A_2 \cap B_2)$ | $\cdots$ | $P(A_2 \cap B_m)$ | $P(A_2)$ |
    | $\vdots$ | $\vdots$ | $\vdots$ | $\ddots$ | $\vdots$ | $\vdots$ |
    | $A_n$ | $P(A_n \cap B_1)$ | $P(A_n \cap B_2)$ | $\cdots$ | $P(A_n \cap B_m)$ | $P(A_n)$ |
    | $\sum_{i=1}^{n}P(A_i \cap B_j)$ | $P(B_1)$ | $P(B_2)$ | $\cdots$ | $P(B_m)$ | $1$ |

### Statistical Independence

- **조건부 확률(Conditional Probability)** : 사건 $A_1$ 이 발생했을 때 사건 $A_2$ 가 발생할 확률

    $$
    P(A_2 \vert A_1) = \frac{P(A_2 \cap A_1)}{P(A_1)} \quad (\text{s.t.}\, P(A_1)>0)
    $$

- **베이즈 정리(Bayes Theorem)**

    $$\begin{aligned}
    P(B \vert A)
    &= \frac{P(B)P(A \vert B)}{P(A)}\\
    &= \frac{P(B) \times \frac{P(A \cap B)}{P(B)}}{P(A)}\\
    &= \frac{P(B \cap A)}{P(A)}
    \end{aligned}$$

    - **일반화**

        > 사건 $B_1, B_2, B_3, \cdots, B_m$ 이 상호배타적이고 집단전체적이라면, 사건 $A$ 와 $B_j\,(j=1,2,3,\cdots,m)$ 에 대하여 다음이 성립함

        $$\begin{aligned}
        P(B_j \vert A)
        &= \frac{P(A \vert B_j) \times P(B_j)}{\displaystyle\sum_{i=1}^{m}P(A \vert B_i)P(B_i)}
        \end{aligned}$$

- **통계적 독립성(Statistical Independence)** : 한 사건의 발생 여부가 다른 사건이 발생할 가능성에 아무런 영향을 끼치지 못하는 경우

    $$
    P(A_2 \vert A_1) = P(A_2) \quad \text{or} \quad P(A_1 \vert A_2) = P(A_1)
    $$

    - 사건 $A_1$ 과 $A_2$ 가 통계적으로 독립적이면 다음을 만족함

        $$
        P(A_1 \cap A_2) = P(A_1)P(A_2)
        $$
    
    - 사건 $A_1$ 과 $A_2$ 가 상호배타적이라고 해서 통계적으로 독립이라고 볼 수는 없음
        - 사건 $A_1$ 과 $A_2$ 가 상호배타적인 경우

            $$
            P(A_1 \cap A_2) = 0 \quad (\text{s.t.} \, P(A_1)>0, P(A_2)>0)
            $$
        
        - 사건 $A_1$ 과 $A_2$ 가 통계적으로 독립인 경우

            $$\begin{aligned}
            P(A_2 \vert A_1)
            &=\frac{P(A_2 \cap A_1)}{P(A_1)} \\
            &=P(A_2) \quad (\text{s.t.} \, P(A_1)>0, P(A_2)>0)
            \end{aligned}$$

## Random Variables
-----

### What? Random Variable

- **확률변수(Random Variable)** : 표본공간 $S$ 에 대하여 그 결과에 숫자를 배정하는 규칙으로서, 그 값이 확률실험 결과에 의해 결정되는 변수

- **확률 분포(Probability Distribution)** : 확률변수의 값 $x \in X$ 에 대하여 각각에 대응하는 확률 값 $P(x)$ 의 분포

- **확률분포함수** : 확률변수를 정의역으로, 그 분포를 치역으로 가지는 함수

    $$\begin{aligned}
    f(x)=P(X=x)
    \end{aligned}$$

- **누적분포함수(Cumulative Distribution Function)** : 확률변수 $X$ 에 대하여 그 값이 특정한 값 $k$ 이하일 확률에 대한 함수

    $$\begin{aligned}
    F(k)
    &=P(X \le k)
    \end{aligned}$$

### Example

#### Probability Experiment of Tossing a Coin Twice

- **표본공간 $S$ 정의**
    
    $$
    S=\{HH,HT,TH,TT\}
    $$

- **결과 $outcome \in S$ 의 확률 정의**

    | $outcome \in S$ | $P(outcome)$ |
    |---|---|
    | $HH$ | $0.25$ |
    | $HT$ | $0.25$ |
    | $TH$ | $0.25$ |
    | $TT$ | $0.25$ |

#### `규칙1` 같은 면이면 1, 다른 면이면 0

- **확률변수 $X$ 정의** : $X = \{0, 1\}$

    | $outcome \in S$ | $x \in X$ |
    |---|---|
    | $HH$ | $1$ |
    | $HT$ | $0$ |
    | $TH$ | $0$ |
    | $TT$ | $1$ |

- **확률변수 $x \in X$ 의 확률분포**

    | $x \in X_1$ | $P(x)$ |
    |---|---|
    | $1$ | $0.5$ |
    | $0$ | $0.5$ |

#### `규칙2` 앞면의 갯수

- **확률변수 $X$ 정의** : $X = \{0, 1, 2\}$

    | $outcome \in S$ | $x \in X$ |
    |---|---|
    | $HH$ | $2$ |
    | $HT$ | $1$ |
    | $TH$ | $1$ |
    | $TT$ | $0$ |

- **확률변수 $x \in X$ 의 확률분포**

    | $x \in X$ | $P(x)$ |
    |---|---|
    | $2$ | $0.25$ |
    | $1$ | $0.5$ |
    | $0$ | $0.25$ |

## Discrete Random Variable
-----

### What? Discrete Random Variable

- **이산확률변수(Discrete Random Variable)** : 변수가 취할 수 있는 값의 수를 셀 수 있는 확률변수

    $$
    X=\{x_i\,|\,i=1,2,3,\cdots,n\}
    $$

    - 동전 앞면의 수
    - 주사위 눈의 수
    - 자녀의 수
    - 한 시간 동안 방문한 고객의 수

- **이산확률분포(Discrete Probability Distribution)** : 이산확률변수 $X$ 가 취할 수 있는 값 $x \in X$ 에 대하여 그 값이 발생할 확률 $P(x)$ 의 분포

    $$
    P(X)
    $$

- **확률질량함수(Probability Mass Function; $pmf$)** : 이산확률변수를 정의역으로, 그 확률분포를 치역으로 가지는 함수

    $$\begin{aligned}
    f:\,X\rightarrow P(X)
    \end{aligned}$$

    - 이산확률변수 $X=\{x_1, x_2, x_3, \cdots, x_n\}$ 에 대하여 그 확률질량함수는 다음의 조건을 만족해야 함
        - $0 \le P(x) \le 1, \; x^{\forall} \in X$
        - $\displaystyle\sum_{i=1}^{n}P(x_i)=1$

- **누적분포함수(Cumulative Distribution Function; $cdf$)** : 이산확률변수 $X$ 에 대하여 그 값이 특정한 값 $k$ 이하일 확률에 대한 함수

    $$\begin{aligned}
    F(k)
    &=P(X \le k) \\
    &=\sum_{x=1}^{k}f(x)
    \end{aligned}$$

### Descriptive Statistic

- **기대값(Expected Value; $E$)** : 각 값이 발생할 확률에 따라 가중평균된 값

    > 이산확률변수 $X$ 가 값 $x_i (i=1,2,3,\cdots,n)$ 을 가질 확률이 $P(x_i)$ 일 때, $X$ 의 기대값 $E\left[X\right]$ 를 다음과 같이 정의함

    $$\begin{aligned}
    E\left[X\right]
    &= \mu \\
    &= \displaystyle\sum_{i=1}^{n}x_iP(x_i)
    \end{aligned}$$

    - **성질**

        > 이산확률변수 $X, Y$ 와 상수 $\alpha, \beta$ 에 대하여 다음이 성립함

        - $E\left[\alpha \right]=\alpha$
        - $E\left[\alpha X \right]=\alpha E\left[X \right]$
        - $E\left[\alpha X \pm \beta Y \right] = \alpha E\left[X \right] \pm \beta E\left[Y \right]$
        - $X, Y$ 가 독립이면 $E \left[XY \right]=E \left[X \right]E \left[Y \right]$

- **분산(Variance; $Var$)**

    > 이산확률변수 $X$ 가 값 $x_i (i=1,2,3,\cdots,n)$ 을 가질 확률이 $P(x_i)$ 일 때, $X$ 의 분산 $Var(X)$ 를 다음과 같이 정의함

    $$\begin{aligned}
    Var \left[X \right]
    &=\sigma^2\\
    &=\displaystyle\sum_{i=1}^{n}(x_i-\mu)^2P(x_i)\\
    &=E \left[(X-\mu)^2 \right]\\
    &=E \left[X^2 \right]-E \left[X \right]^2
    \end{aligned}$$
    
    - **성질**
        
        > 이산확률변수 $X, Y$ 와 상수 $\alpha, \beta$ 에 대하여 다음이 성립함

        - $Var\left[\alpha \right]=0$
        - $Var\left[\alpha X \right]=\alpha^2Var\left[X \right]$
        - $Var\left[\alpha + X \right]=Var\left[X \right]$
        - $Var\left[\alpha X \pm \beta Y \right] = \alpha^2Var\left[X \right] + \beta^2Var\left[Y \right] \pm 2\alpha\beta Cov\left[X, Y \right]$

### Statistical Independence

- **이산확률변수의 결합확률분포(Joint Probability Distribution)**

    > 이산확률변수 $x \in X, y \in Y$ 에 대하여 그 결합확률분포 $P(x, y)$ 는 $X=x, Y=y$ 일 확률을 추정한 분포로 정의함

    $$
    P(X=x_i, Y=y_j)=P(x_i \cap y_j)
    $$

    $$\begin{aligned}
    for\; X&=\{x_i\,|\,i=1,2,\cdots,n\},\\
    Y&=\{y_j\,|\,j=1,2,\cdots,m\}
    \end{aligned}$$
    
    - **공리**
        - $0 \le P(x_i,y_j) \le 1$
        - $\displaystyle\sum_{i=1}^{n} \displaystyle\sum_{j=1}^{m} P(x_i,y_j)=1$
    
    - **규칙**
        - $P_X(x_i)=\displaystyle\sum_{j=1}^{m}P(x_i,y_j)$
        - $P_Y(y_j)=\displaystyle\sum_{i=1}^{n}P(x_i,y_j)$

- **이산확률변수의 공분산**

    $$\begin{aligned}
    Cov\left[X,Y\right]
    &=\sigma_{XY}\\
    &=E\left[(X-\mu_{X})(Y-\mu_{Y})\right]\\
    &=E\left[XY\right]-\mu_{X}\mu_{Y}\\
    &=\displaystyle\sum_{i=1}^{n} \displaystyle\sum_{j=1}^{m} P(x_i,y_j)-\mu_{X}\mu_{Y}
    \end{aligned}$$

    - **성질**

        > 이산확률변수 $X, Y, Z$ 와 상수 $\alpha, \beta$ 에 대하여 다음이 성립함

        - $Cov\left[X, \alpha \right]=0$
        - $Cov\left[X+\alpha, Y+\beta \right]=Cov\left[X,Y \right]$
        - $Cov\left[\alpha X, \beta Y \right]=\alpha\beta Cov\left[X,Y \right]$
        - $Cov\left[X+Y,Z \right]=Cov\left[X,Z \right]+Cov\left[Y,Z \right]$

- **이산확률변수 간 통계적 독립**
    - 모든 $(x_i, y_j)$ 에 대하여 다음을 만족하는 경우 이산확률변수 $X, Y$ 는 통계적으로 독립임

        $$
        P(x_i \vert y_j)=P_X(x_i) \quad \text{or} \quad P(y_j \vert x_i)=P_Y(y_j)
        $$

    - 이산확률변수 $X, Y$ 가 통계적으로 독립이면 다음이 성립함
        - $ P(x_{i}, y_{j})=P_X(x_{i})P_Y(y_{j}) $
        - $ Cov\left[X,Y \right]=0 $

    - 위 명제에 근거하여 다음이 성립함

        $$\begin{aligned}
        Cov\left[X,Y \right]
        &=\displaystyle\sum_{i=1}^{n} \displaystyle\sum_{j=1}^{m} P(x_i,y_j)-\mu_{X}\mu_{Y}\\
        &=0\\
        \therefore \mu_{X}\mu_{Y}
        &=\displaystyle\sum_{i=1}^{n} \displaystyle\sum_{j=1}^{m} x_iy_jP_X(x_i)P_Y(y_j)
        \end{aligned}$$

## Continuous Random Variable
-----

### What? Continuous Random Variable

- **연속확률변수(Continuous Random Variable)** : 변수가 취할 수 있는 값이 연속적이어서 그 수를 셀 수 없는 확률변수

    $$
    X=(l,u) \quad \text{or} \quad X=[l,u]
    $$

    - 길이
    - 무게
    - 시간
    - 기온

- **연속확률분포(Continuous Probability Distribution)** : 연속확률변수 $X$ 가 취할 수 있는 값 $x \in X$ 에 대하여 그 값이 발생할 확률 $P(x)$ 의 분포

    $$
    P(X)
    $$

- **확률밀도함수(Probability Density Function; $pdf$)** : 연속확률변수를 정의역으로, 그 확률분포를 치역으로 가지는 함수

    $$\begin{aligned}
    f:\,X\rightarrow P(X)
    \end{aligned}$$

    - 구간 $X=(l, u)$ 혹은 $X=[l,u]$ 에서 정의된 연속확률변수 $x \in X$ 에 대하여 그 확률밀도함수는 다음의 조건을 만족해야 함
        - $\displaystyle\int_{l}^{u}f(x)dx=1$
            - $f(x \in [a, b])=P(a \le x \le b)=\displaystyle\int_{a}^{b}f(x)dx$
            - $f(k)=P(k \le x \le k)=\displaystyle\int_{k}^{k}f(x)dx=0$

        - $f(x) \ge 0 \quad \text{for} \; x^{\forall} \in X$

- **누적분포함수(Cumulative Distribution Function; $cdf$)** : 연속확률변수 $X$ 에 대하여 그 값이 특정한 값 $k$ 이하일 확률에 대한 함수

    $$\begin{aligned}
    F(k)
    &=P(X \le k) \\
    &=\displaystyle\int_{x=1}^{k}f(x)dx
    \end{aligned}$$

### Continuous Statistic

- **기대값(Expected Value; $E$)**

    $$\begin{aligned}
    E \left[X \right]
    &=\mu\\
    &=\displaystyle\int_{x=l}^{u}xf(x)dx
    \end{aligned}$$

- **분산(Variance; $Var$)**

    $$\begin{aligned}
    Var \left[X \right]
    &=\sigma^2\\
    &=E \left[(X-\mu)^2 \right]\\
    &=\displaystyle\int_{x=l}^{u}(x-\mu)^2f(x)dx
    \end{aligned}$$
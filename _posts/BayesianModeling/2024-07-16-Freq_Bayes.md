---
order: 2
title: Frequentist vs. Bayesian
date: 2024-07-16
categories: [Data Mining Techs, Bayesian Modeling]
tags: [Bayesian, Optimization, MLE, Bayes' Theorem]
math: true
description: >-
    Based on the lecture “Bayesian Modeling (2024-1)” by Prof. Yeo Jin Chung, Dept. of AI, Big Data & Management, College of Business Administration, Kookmin Univ.
image:
    path: /_post_refer_img/BayesianModeling/Thumbnail.jpeg
---

## Uncertainty

- **불확실성(Uncertainty)** : 어떠한 사건(Outcome)에 대하여 확신할 수 없는 상태

- **우발적 불확실성(Aleatoric Uncertainty)** : 시스템이 본질적으로 확률적이기에 발생하는 불확실성
    - **확률적 시스템(Stochastic System)** : 동일한 조건에서 실험을 반복하더라도 결과가 동일하지 않고 일정한 확률 분포를 따르는 시스템
    - 표본 변동성(Sample Variability), 데이터 생성 과정상의 우연성(Randomness)으로 인해 발생함
    - 시스템에 내재된 불확실성이므로 줄일 수 없음

- **인식 불확실성(Epistemic Uncertainty)** : 연구자가 충분한 정보를 확보하지 못했기에 발생하는 불확실성
    - 모형의 구조적 불완전성, 모형 가정의 부적합, 데이터 희소성, 데이터 신호의 모호성, 데이터의 모집단 대표성 부족 등으로 인해 발생함
    - 적합한 모형을 선택하거나 데이터를 추가 확보함으로써 줄일 수 있음

- **확률 모형(Probability Model)** : 불확실한 현상에 대하여 설명하거나 예측하기 위하여 수학적으로 정의된 체계
    - **확률(Probability)** : 불확실성을 정량적으로 표현하는 도구로서, 사건이 발생할 가능성을 나타냄
    - **모형(Model)** : 어떠한 현상을 설명하거나 예측하기 위하여 수학적으로 혹은 논리적으로 정의된 체계
    - **모수(Parameter)** : 모수 추정에서 확률 모형을 정의하는 요소로서, 확률 모형의 구조와 가정 하에서 사건 발생 원리를 제한적으로 설명함

## Frequentist vs. Bayesian
-----

- **모수(Parameter)** : 세계에 존재하는 고정된 사실

    | | 빈도주의 | 베이즈주의 |
    |---|---|---|
    | 불확실성 원천 | 모수 추정 과정 | 모수에 대한 무지 |
    | 우발적 불확실성 | 표본추출의 변동 | 데이터 생성 과정 |
    | 인식 불확실성 | X | 신념도 |
    | 모델링 대상 | 모수 추정량 $\hat{\theta} \sim F$ | 모수의 사후 확률 분포 $\theta \mid \mathcal{D} \sim F$ |

### Frequentist

- **빈도주의(Frequentist)**

    - `PERSPECTIVE`
        - **실증주의(Positivism)** : 사건들의 결과의 집합에 대하여 정의
        - **확률의 빈도적 해석(Frequentist interpretation)** : 무한 반복 실험에서 사건이 발생하는 **상대 빈도(Relative Frequency)**

    - `TARGET` 모수(Parameter)
 
    - `QUESTION` *모수는 무엇인가?*

    - `GOAL` *모수의 정체를 실증적으로 규명하겠다.*

    - `ASSUMPTION` *실험을 반복하면 그 결과는 장기적으로 모수로 수렴할 것이다.*

    - `REASON` 대수의 법칙(Law of Large Numbers)

- **최우추정(`M`aximum `L`ikelihood `E`stimation)** : 우도를 최대화하는 모수의 추정치를 탐색하는 방법

    $$\begin{aligned}
    \max_{\theta}{p\left(\mathcal{D} \mid \theta \right)}
    \end{aligned}$$

    - **우도(Likelihood)** : 모수 조건부 데이터 발생 가능성으로서, 특정 모수 하에서 사건이 관찰되는 상대 빈도로 해석되며, 해당 모수 하에서의 우발적 불확실성을 반영함
    - **신뢰 구간(Confidence Interval)** : 구간 추정에서의 추정치로서, 모수를 포함할 것으로 기대되는 구간
    - **신뢰 수준(Confidence Level)** : 무한 반복 실험에서 생성된 여러 신뢰 구간 중, 모수를 포함하는 신뢰 구간의 비율

### Bayesianism

- **베이즈주의(Bayesianism)**

    - `PERSPECTIVE`
        - **인식론(Epistemology)** : 단일 사건들의 진술에 대하여 정의
        - **확률의 주관적 해석(Subjective interpretation)** : 주어진 정보에 근거했을 때 사건이 발생할 것이라는 **신념도(Degree of Belief)**

    - `TARGET` 모수의 정체를 규명하는 명제에 대한 신념도(Degree of Belief)

    - `QUESTION` *모수에 대하여 얼마나 알고 있는가?*

    - `GOAL` *모수의 정체에 대한 신념을 참인 앎으로서 정당화하겠다.*

    - `ASSUMPTION` *신념을 확률로써 표현하고 이를 정보 갱신으로써 정당화할 수 있다.*

    - `REASON`
        - **기대 효용 이론(Expected Utility Theory)** : 신념의 측정 가능성 정당화
        - **더치북 논증(Dutch Book Argument)** : 신념의 확률적 정합성 강제화
        - **마틴게일 수렴 정리(Doob’s Martingale Convergence Theorem)** : 조건부 정보 갱신의 진리 접근성 정당화

- **베이즈 정리(Bayes' Theorem)** : 모수의 사후 확률 분포를 추정하는 방법

    $$\begin{aligned}
    \underbrace{p\left(\theta \mid \mathcal{D} \right)}_{\text{Posterior}}
    = \underbrace{\frac{p\left(\mathcal{D} \cap \theta\right)}{p\left(\mathcal{D}\right)}}_{\begin{array}{c} \text{Conditional}\\ \text{Probability} \end{array}}
    = \frac{\overbrace{p\left(\mathcal{D} \mid \theta \right)}^{\text{Likelihood}} \cdot \overbrace{p\left(\theta\right)}^{\text{Prior}}}{\underbrace{p\left(\mathcal{D}\right)}_{\text{Evidence}}}
    \end{aligned}$$

    - **사후 확률 분포(Posterior Probability Distribution)** : 모수의 불확실성을 나타냄
    - **우도(Likelihood)** :  모수 조건부 데이터 발생 가능성으로서, 데이터에 대한 모수의 상대적 적합성으로 해석되며, 표본 변동성에서 비롯한 특정 모수 하에서의 우발적 불확실성을 반영함
    - **사전 확률 분포(Prior Probability Distribution)** : 주어진 정보의 한계에서 비롯한 모수에 대한 인식 불확실성을 반영함
    - **증거(Evidence)** : 데이터가 관찰될 확률로서, 모수에 대한 신념을 뒷받침하는 증거로 해석됨

        > 베이지안에서는 모수에 대하여 주장함에 있어 사전 지식이나 관찰된 데이터 등 현재 주어진 정보를 기반으로 함. 는 따라서 현재까지 관찰된 데이터가 실현될 가능성은 모수에 대한 주장의 증거(Evidence)임.

## Sample Size: The Necessity for Bayesian
-----

- **대수의 법칙과 작은 수의 혼란**

    > 표본의 크기는 결코 크지 않다. 만일 N이 충분한 추정을 얻기에 부족하다면 더 많은 데이터(또는 더 많은 가정)을 확보해야 한다. 그러나 일단 N이 충분히 크다면 데이터를 나눠 더 많은 것(가령 여론조사에서 전국적으로 훌륭한 추정을 얻었다면 남과 여, 지역별, 연령대별 그룹 등으로 나눠 추정할 수 있다)을 얻을 수 있다. N은 충분하지 않다. 만약 충분하더라도 여러분은 이미 더 많은 데이터가 필요한 다음 문제에 직면하기 때문이다. (Andrew Gelman)

    - **대수의 법칙(Law of Large Numbers)** : 무작위 실험을 반복해서 수행할수록 관측된 상대적 빈도(추정치)가 이론적 확률(모수)에 가까워진다는 법칙
    - **작은 수의 혼란(Law of Small Numbers)** : 적은 표본에서도 대수의 법칙이 적용될 것이라고 잘못 가정하거나 소규모 데이터로 도출된 결과를 일반화하려는 오류

- **If the sample size is sufficient,**

    > 모수가 특정 값으로 발생할 것이라는 믿음은 신규 관측치에 의해 끊임없이 갱신되어 참값을 중심으로 집중됨. 이는 빈도주의 추론과 베이지안 추론의 결과가 장기적으로 일치함을 의미함.

    $$
    \lim_{n \to \infty} P(\theta \mid X_{1}, X_{2}, \cdots, X_{n}) \to \mathcal{N}(\theta_{\text{true}}, \frac{\sigma^2}{n})
    $$

- **If the sample size is not large enough,**
    - **빈도주의자(Frequentist)** : 신뢰수준을 상향 조정하여 표본의 변동성에 따른 모수 추정 과정상의 불확실성을 나타냄

        $$
        \text{CI}_{\theta}=\bar{X}\pm Z\cdot\frac{\sigma}{\sqrt{n}}
        $$

    - **베이지안(Bayesian)** : 모수의 불확실성을 확률로써 표현함

        $$
        p\left(\theta \mid \mathcal{D}\right)=\frac{p\left(\mathcal{D} \mid \theta\right) \cdot p\left(\theta\right)}{p\left(\mathcal{D}\right)}
        $$

## `[example]` 동전 던지기
-----

> 동전을 던졌을 때 앞면이 나올 확률을 $\theta$ 라고 하자. $\theta$ 에 대한 정보가 아무것도 없다고 가정하자. 즉, $\theta$ 는 0과 1 사이의 무작위수일 것이라고 믿어지고 있다. 동전을 두 번 던졌는데 두 번 다 앞면이 나왔다. 그렇다면 $\theta$ 에 대한 믿음은 어떻게 변화할까?

![01](/_post_refer_img/BayesianModeling/02-01.png){: width="100%"}


- **Prior Prob. Dist.**:

    $$\begin{aligned}
    p(\theta)
    =1 \quad \because \theta \sim \text{Uniform}(0,1)
    \end{aligned}$$

- **Likelihood**:

    $$\begin{aligned}
    p\left(X \mid \theta\right)
    =\frac{n!}{X!(n-X)!} \cdot \theta^{X} \cdot (1-\theta)^{n-X} \quad \because X \mid \theta \sim \text{Bin}(n,\theta)
    \end{aligned}$$

- **Evidence**:

    $$\begin{aligned}
    p(X)
    &= \int_{0}^{1}{p\left(X \mid \theta\right)}\text{d}\theta\\
    &= \int_{0}^{1}{\frac{n!}{X!(n-X)!} \cdot \theta^{X} \cdot (1-\theta)^{n-X}}\text{d}\theta\\
    &= \frac{n!}{X!(n-X)!} \cdot \int_{0}^{1}{\theta^{X} \cdot (1-\theta)^{n-X}}\text{d}\theta\\
    &= \frac{n!}{X!(n-X)!} \cdot \text{B}(X+1,n-X+1)\\
    &= \frac{n!}{X!(n-X)!} \cdot \frac{\Gamma(X+1)\Gamma(n-X+1)}{\Gamma(n+2)} \quad \because (X+1),(n-X+1) \in \mathbf{R}^{+}\\
    &= \frac{n!}{X!(n-X)!} \cdot \frac{X!(n-X)!}{(n+1)!} \quad \because (X+1),(n-X+1) \in \mathbf{Z}^{+}\\
    &= \frac{1}{n+1}
    \end{aligned}$$

    - $\text{B}(\alpha,\beta)$ : 베타 함수

        $$\begin{aligned}
        \text{B}(\alpha,\beta)
        &= \int_{0}^{1}{t^{\alpha-1}(1-t)^{\beta-1}}\text{d}t\\
        &= \frac{\Gamma(\alpha)\Gamma(\beta)}{\Gamma(\alpha+\beta)} \quad \text{where}\; \alpha,\beta \in \mathbb{R}^{+}
        \end{aligned}$$

    - $\Gamma(n)$ : 감마 함수

        $$\begin{aligned}
        \Gamma(n)
        &= \int_{0}^{\infty}{t^{(n-1)}e^{-t}}\text{d}t\\
        &= (n-1)! \quad \text{where}\; n \in \mathbb{Z}^{+}
        \end{aligned}$$

- **Posterior Prob. Dist.**:

    $$\begin{aligned}
    p\left(\theta \mid X\right)
    &\propto p\left(X \mid \theta\right) \cdot p\left(\theta\right)\\
    &= \frac{n!}{X!(n-X)!} \cdot \theta^{X} \cdot (1-\theta)^{n-X}\\
    \\
    \therefore \theta \mid X
    &\sim \text{Beta}(X+1,n-X+1)
    \end{aligned}$$

    - $\text{Beta}(\alpha,\beta)$ : 베타분포

        $$
        f(x)
        = \frac{x^{\alpha-1}(1-x)^{\beta-1}}{\text{B}(\alpha,\beta)}
        \sim \text{Beta}(\alpha,\beta)
        $$
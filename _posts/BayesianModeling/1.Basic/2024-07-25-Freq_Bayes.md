---
order: 4
title: Frequentist vs. Bayesian
date: 2024-07-25
categories: [BAYES, 1.bayes basic]
tags: [Bayesian, Optimization, MLE, Bayes' Theorem]
math: true
description: >-
    Based on the lecture “Bayesian Modeling (2024-1)” by Prof. Yeo Jin Chung, Dept. of AI, Big Data & Management, College of Business Administration, Kookmin Univ.
image:
    path: /_post_refer_img/BayesianModeling/1.Basic/Thumbnail.jpeg
---

## Probability
-----

- **귀납법(Induction)**: 관측된 데이터로부터 일반화된 진술(혹은 모형)을 도출하는 방법

    | 관점 | 진리 | 설명 |
    |---|---|---|
    | 존재론<br>(Ontology) | 사실적 진리<br>(Factual Truth) | 실제 세계에서 어떤 일이 일어났는가? |
    | 실증론<br>(Positivism) | 빈도적 진리<br>(Frequentist Truth) | 반복된 시행에서 수렴하는 비율 |
    | 인식론<br>(Epistemology) | 인식적 진리<br>(Epistemic Truth) | 정보에 따라 믿음이 수렴해가는 대상 |

    - **결정론적 귀납화(Determinism)**: 일반화된 진술의 불확실성을 고려하지 않는 귀납법
        - *동전을 던지면 앞면이 나온다.*

    - **확률론적 귀납화(Probability Theory)**: 일반화된 진술의 불확실성을 확률 분포로써 정량화하는 귀납법
        - *반복 실험 결과, $0.5$ 의 비율로 동전을 던지면 앞면이 나왔다.*
        - *동전을 던지면 앞면이 나온다는 진술을 $0.5$ 수준으로 신뢰할 수 있다.*

- **불확실성(Uncertainty)**: 어떠한 사건에 대하여 확신할 수 없는 상태
    - **우발적 불확실성(Aleatoric Uncertainty)**: 시스템이 본질적으로 확률적이기에 발생하는 불확실성
        - 표본 추출의 우발성(Frequentist)
        - 데이터 생성 과정 상의 무작위성(Bayesianism)
    
    - **인식적 불확실성(Epistemic Uncertainty)**: 연구자가 충분한 정보를 확보하지 못했기에 발생하는 불확실성
        - 모형의 구조적 불완전성
        - 모형 가정의 부적합
        - 데이터 희소성
        - 데이터 신호의 모호성
        - 데이터의 모집단 대표성 부족 등

- **확률(Probability)**: 불확실성을 정량적으로 표현하는 도구
    - **빈도주의(Frequentist)**: 확률의 빈도적 해석

        > *반복 실험 결과, $0.5$ 의 비율로 동전을 던지면 앞면이 나왔다.*

        - **목표**: `실증론(Positivism)`적 관점에서 `모수의 정체`를 규명하는 것
        - **준거 집합(Reference Set)**: 무한 반복 실험 결과들의 집합
        - **확률 해석(Probability Interpretation)**: 사건이 발생하는 장기 상대 빈도
        - **불확실성(Uncertainty)**: 모수 추정 과정 상의 불확실성으로서 표본 추출의 우발성
        - **표현**: 신뢰구간(모수를 포함하는 구간)과 신뢰수준(반복 실험에서 모수를 포함하는 상대 빈도)

    - **베이즈주의(Bayesianism)**: 확률의 주관적 해석

        > *동전을 던지면 앞면이 나온다는 진술을 $0.5$ 수준으로 신뢰할 수 있다.*

        - **목표**: `인식론(Epistemology)`적 관점에서 `모수에 대한 인지 수준`을 향상시키는 것
        - **준거 집합(Reference Set)**: 단일 사건에 대한 진술 집합
        - **확률 해석(Probability Interpretation)**: 사건이 발생할 것이라는 진술의 신념도
        - **불확실성(Uncertainty)**: 모수 자체의 불확실성으로서 인식적 제약으로 인한 모수에 대한 무지
        - **표현**: 사후 확률 분포(모수에 대한 진술과 그 신념도의 집합)

## Optimization Methods
-----

- **최우추정(`M`aximum `L`ikelihood `E`stimation)** : 우도를 최대화하는 모수의 추정치를 탐색하는 방법

    $$\begin{aligned}
    \max_{\theta}{p\left(\mathcal{D} \mid \theta \right)}
    \end{aligned}$$

    - **우도(Likelihood)**: 특정 모수 하에서 사건이 관찰되는 상대 빈도
    - **신뢰 구간(Confidence Interval)**: 모수를 포함할 것으로 기대되는 구간
    - **신뢰 수준(Confidence Level)**: 여러 신뢰 구간 중 모수를 포함하는 신뢰 구간의 비율

- **베이즈 정리(Bayes' Theorem)** : 모수의 사후 확률 분포를 추정하는 방법

    $$\begin{aligned}
    \underbrace{p\left(\theta \mid \mathcal{D} \right)}_{\text{Posterior}}
    = \underbrace{\frac{p\left(\mathcal{D} \cap \theta\right)}{p\left(\mathcal{D}\right)}}_{\begin{array}{c} \text{Conditional}\\ \text{Probability} \end{array}}
    = \frac{\overbrace{p\left(\mathcal{D} \mid \theta \right)}^{\text{Likelihood}} \cdot \overbrace{p\left(\theta\right)}^{\text{Prior}}}{\underbrace{p\left(\mathcal{D}\right)}_{\text{Evidence}}}
    \end{aligned}$$

    - **사후 확률 분포(Posterior Probability Distribution)**: 모수에 대한 인식적 불확실성
    - **우도(Likelihood)**:  데이터에 대한 모수의 상대적 적합성
    - **사전 확률 분포(Prior Probability Distribution)**: 모수에 대한 사전 정보
    - **증거(Evidence)**: 데이터가 관찰될 확률

## Sample Size: The Necessity for Bayesian
-----

> 표본의 크기는 결코 크지 않다. 만일 N이 충분한 추정을 얻기에 부족하다면 더 많은 데이터(또는 더 많은 가정)을 확보해야 한다. 그러나 일단 N이 충분히 크다면 데이터를 나눠 더 많은 것(가령 여론조사에서 전국적으로 훌륭한 추정을 얻었다면 남과 여, 지역별, 연령대별 그룹 등으로 나눠 추정할 수 있다)을 얻을 수 있다. N은 충분하지 않다. 만약 충분하더라도 여러분은 이미 더 많은 데이터가 필요한 다음 문제에 직면하기 때문이다. (Andrew Gelman)

- **대수의 법칙(Law of Large Numbers)**: 무작위 실험을 반복해서 수행할수록 관측된 상대적 빈도(추정치)가 이론적 확률(모수)에 가까워진다는 법칙

- **작은 수의 혼란(Law of Small Numbers)**: 적은 표본에서도 대수의 법칙이 적용될 것이라고 잘못 가정하거나 소규모 데이터로 도출된 결과를 일반화하려는 오류

- **If the sample size is sufficient,**

    > 모수가 특정 값으로 발생할 것이라는 믿음은 신규 관측치에 의해 끊임없이 갱신되어 참값을 중심으로 집중됨. 이는 빈도주의 추론과 베이지안 추론의 결과가 장기적으로 일치함을 의미함.

    $$
    \lim_{n \to \infty} P(\theta \mid X_{1}, X_{2}, \cdots, X_{n}) \to \mathcal{N}(\theta_{\text{true}}, \frac{\sigma^2}{n})
    $$

- **If the sample size is not large enough,**
    - **빈도주의(Frequentist)**: 신뢰 수준을 상향 조정하여 모수 추정 과정상의 불확실성을 줄이고자 함

        $$
        \text{CI}_{\theta}=\bar{X}\pm Z\cdot\frac{\sigma}{\sqrt{n}}
        $$

    - **베이즈주의(Bayesianism)**: 모수의 불확실성을 확률로써 표현함

        $$
        p\left(\theta \mid \mathcal{D}\right)=\frac{p\left(\mathcal{D} \mid \theta\right) \cdot p\left(\theta\right)}{p\left(\mathcal{D}\right)}
        $$
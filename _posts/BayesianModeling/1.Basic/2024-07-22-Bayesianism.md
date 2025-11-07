---
order: 1
title: Bayesianism
date: 2024-07-22
categories: [BAYES, 1.bayes basic]
tags: [Epistemology, Bayesian, Bayes' Theorem]
math: true
description: >-
    Based on the lecture “Bayesian Modeling (2024-1)” by Prof. Yeo Jin Chung, Dept. of AI, Big Data & Management, College of Business Administration, Kookmin Univ.
image:
    path: /_post_refer_img/BayesianModeling/1.Basic/Thumbnail.jpeg
---

## Epistemology
-----

- **인식론(Epistemology)**: 믿음이 어떻게 정당화되어 앎이 되는가에 대한 철학적 논의

    > 앎은 정당화된 참된 믿음(Knowledge is `J`ustified `T`rue `B`elief)

    - **믿음(Belief)**: *해당 명제가 참임을 믿고 있다.*
    - **사실(Truth)**: *해당 명제가 사실이어야 한다.*
    - **정당화(Justification)**: *믿음에는 근거가 있어야 한다.*

- **베이즈주의(Bayesianism)**: 수량화된 인식론

    > 확률적 귀납 개념에 따르면 과학 이론은 절대적 확실성을 가질 수 없지만 확실한 참과 확실한 거짓이라는 양극단 사이에 존재하는 인식적 값을 가질 수 있으며, 그 값은 새로운 증거에 의해 변경될 수 있다. (이영의, 2015, p.19)

    - **형식 체계(Formalism)**: 베이즈 정리(Bayes' Theorem)
    - **해석 체계(Interpretation)**: 확률의 주관적 해석(Subjective interpretation)

- **베이지안 프레임워크(Bayesian Framework)**

    | Formalism | Bayes Module | Interpretation |
    |---|---|---|
    | $$p(\theta)$$ | 사전 확률 분포(Prior) | 신념(Belief) |
    | $$p(\mathcal{D}\mid\theta)$$ | 우도(Likelihood) | 참(Truth) |
    | $$p(\mathcal{D})$$ | 증거(Evidence) | 근거(Reason) |
    | $$p(\theta\mid\mathcal{D})$$ | 사후 확률 분포(Posterior) | 앎(Knowledge) |
    | $$p(\theta\mid\mathcal{D})=\displaystyle\frac{p(\mathcal{D}\mid\theta)p(\theta)}{p(\mathcal{D})}$$ | 베이즈 정리(Bayes' Theorem) | 정당화(Justification) |

## Formalism
-----

- 콜모고로프의 확률 공리(Kolmogorov Probability Axiom)

    > 확률 공간(Probability Space) $[\Omega, F, P]$ 는 다음을 이른다. 즉, $F$ 는 공집합이 아닌 집합 $\Omega$ 에 대하여 그 시그마 대수($\sigma$-Algebra)이다. 이때 확률함수(Probability Function) $P$ 는 $F$ 로부터 다음을 만족하는 실수로의 함수이다.

    - `K1` 모든 $A \in F$ 에 대하여 $P(A) \ge 0$
    - `K2` $P(\Omega)=1$
    - `K3` $A \cap B = \emptyset$ 인 모든 $A,B \in F$ 에 대하여 $P(A \vee B) = P(A) + P(B)$

- 베이즈주의 확률 공리(Bayesian Probability Axiom)
    - `B1` $A,B \in S$ 에 대하여 $0 \le P(B \mid A) \le 1$
    - `B2` $A$ 가 $B$ 를 논리적으로 함축하면 $P(B \mid A) = 1$
    - `B3` $B,C$ 가 상호 배타적이면 $P(B \vee C\mid A) = P(B \mid A) + P(C \mid A)$
    - `B4` $P(A) \ne 0$ 인 경우 $P(B \mid A) = \displaystyle\frac{P(A \wedge B)}{P(A)}$

- 성질(Property)
    - `T1` $B,C$ 가 독립적이면 $P(B \wedge C \mid A) = P(B \mid A) \cdot P(C \mid A)$
    - `T2` $P(\neg B \mid A) = 1 - P(B \mid A)$
    - `T3` $P(B \vee C \mid A) = P(B \mid A) + P(C \mid A) - P(B \wedge C \mid A)$
    - `T4` $P(C \mid A) = P(B \mid A) \cdot P(C \mid A \wedge B) + P(\neg B \mid A) \cdot P(C \mid A \wedge \neg B)$

- 베이즈 정리(Bayes' Theorem)
    - `BT1` $P(\theta), P(\mathcal{D}) > 0$ 이면 $P(\theta \mid \mathcal{D}) = \displaystyle\frac{P(\mathcal{D} \mid \theta) \cdot P(\theta)}{P(\mathcal{D})}$
    - `BT2` $P(\theta_{1} \vee \cdots \vee \theta_{n})=1$ 이고 $\theta_{i} \vdash \neg \theta_{j}(i \ne j)$ 이면 $P(\theta_{k} \mid \mathcal{D}) = \displaystyle\frac{P(\mathcal{D} \mid \theta_{k}) \cdot P(\theta_{k})}{\sum_{i}{P(\mathcal{D} \mid \theta_{i}) \cdot P(\theta_{i})}}$
    - `BT3` $P(\theta \mid \mathcal{D}) = \displaystyle\frac{P(\theta)}{P(\theta) + P(\mathcal{D} \mid \neg \theta) \cdot P(\neg \theta)/P(\mathcal{D} \mid \theta)}$

## Interpretation
-----

- **확률 해석(Probability Interpretation)**: 확률함수 $P$ 의 의미를 규명하는 해석 체계

    > 해석은 술어 논리, 리만 기하학, 양자역학과 같은 형식체계를 구성하는 공리들과 정의들에 등장하는 미정의된(Undefined) 또는 원초적(Primitive) 용어들에 일상적 의미를 부여하여 그런 공리들과 정리들이 준거 세계에 대해 참이 되도록 하는 작업을 의미한다. (이영의, 2015, p.19)

    - 고전적 해석(Classical interpretation)
    - 논리적 해석(Logical interpretation)
    - 빈도적 해석(Frequentist interpretation)
    - 성향적 해석(Propensity interpretation)
    - **주관적 해석(Subjective interpretation)**

- 주관적 해석(Subjective interpretation) (이영의, 2015, p.34)

    > 베이즈주의는 이처럼 특정 진술에 대한 우리의 믿음, 즉 신념도에 양의 실수를 부여하는 것은 전형적인 확률 판단에 속한다고 보고, 그런 판단을 확률함수 $P$(Probability Function)로 표현한다. 확률함수 $P$ 는 특정 진술을 일정한 수치에 대응시킨다. (이영의, 2015, p.2)

    - `s1` *확률은 특정 명제에 대한 행위자의 신념도이다.*
    - `s2` *확률은 행위, 특히 내기 행위를 조사함으로써 가장 잘 확립될 수 있다.*
    - `s3` *객관적인 확률은 없다. 만약 객관적 확률이 존재한다면 그것은 이차적 확률이다.*
    - `s4` *사건은 고유한 확률을 갖지 않는다. 개인은 자신의 확률을 논리적으로 자유롭게 결정할 수 있다.*
    - `s5` *합리적 개인의 신념은 확률론의 계산법과 무모순적이어야 하고, 동시에 그것에 의해 규제되어야 한다.*

-----

## Reference

- [베이즈주의; 합리성으로부터 객관성으로의 여정](https://product.kyobobook.co.kr/detail/S000001052837)<br>이영의. (2015). 한국연구재단 저술총서 4. 한국문화사
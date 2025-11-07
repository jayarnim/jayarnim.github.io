---
order: 2
title: Justification of Bayesianism
date: 2024-07-23
categories: [BAYES, 1.bayes basic]
tags: [Epistemology, Bayesian, Bayes' Theorem]
math: true
description: >-
    Based on the lecture “Bayesian Modeling (2024-1)” by Prof. Yeo Jin Chung, Dept. of AI, Big Data & Management, College of Business Administration, Kookmin Univ.
image:
    path: /_post_refer_img/BayesianModeling/1.Basic/Thumbnail.jpeg
---

## Condition
-----

> 윤리적으로 중립인 명제에 대하여 그것의 참 여부에 따라 $0-1$ 사이의 서수적 효용을 획득하거나 상실할 수 있는 내기 상황을 가정함으로써, 베이즈주의는 개인의 신념도를 행위의 자발성과 동일시하는 행동주의적 접근을 취한다(이영의, 2015, p.35). 즉, 내기 상황 하에서 신념과 선호를 기대 효용의 형태로 연결하고, 이를 최적화 혹은 효용 극대화라는 선택으로써 측정 가능한 형태로 이끌어낸다.

### Measurement Condition

- 측정 조건(Measurement Condition)

    > 신념도는 측정될 방법을 규정할 수 있을 경우에만 완전한 의미를 가진다(이영의, 2015, p.35).

- 램지 가정(Ramsey's Assumption)

    > 행위의 집합이 주어지면 합리적 행위자는 최대 기대값을 갖는 행위를 선택한다(이영의, 2015, p.35).

- 기대 효용 이론(Expected Utility Theory)

    > $X$ 에 대한 행위자의 신념도가 $p$ 이라는 것은 그 행위자는 $X$ 이면 단위 $1$ 을 지불하고 그렇지 않은 경우에는 $0$ 을 지불하는 도박에 대해 $p$ 를 지불할 용의가 있다는 것이다(de Finetti, 1937, p.62).

### Consistency Condition

- 정합성 조건(Consistency Condition)

    > 여러 가지 명제에 대한 개인의 신념도 집합은 일정한 방식으로 상호 간 일치하거나 입증되어야만 한다(이영의, 2015, p.35).

- 베이즈주의 공준(Bayesianism Postulate)

    > 이상적으로 합리적인 행위자의 신념도는 확률론의 공리체계를 준수한다(이영의, 2015, p.19).

- 더치북 논증(Dutch Book Argument) \| 실용적 정합화

    > 특정인의 확률함수가 공리체계를 만족시키지 못할 경우에, 하나의 내기 전략이 있고 판돈의 집합이 있는 내기 상황에서 그는 결과에 상관없이 항상 일정한 액수를 잃게 된다(이영의, 2015, p.58).

- 콕스 정리(Cox's Theorem) \| 논리적 정합화

    > 함수 $G,H$ 가 실수 전체에 대하여 연속이고, 한 개인의 신념 함수 $b$ 가 논리 집합 $\mathcal{L}$ 에 대하여 $b:\mathcal{L} \times \mathcal{L} \to \mathbb{R}$ 인 단조 함수라고 하자. 아래 조건을 만족하는 신념 함수 $b$ 는 존재론적으로 유일한 확률 함수 $P$ 와 엄격히 증가하는 실수 함수 $F$ 에 대하여 $b(A \mid B) = F(P(A \mid B))$ 임을 만족한다. 즉, 신념 함수 $b$ 는 확률 함수 $P$ 와 동형이다.

    - **논리 연산의 일관성(Associativity & Consistency)**: 이변수 함수 $G$ 가 논리 연산 $\wedge$ 의 구조적 결합성과 일치하기 위해서는 형태가 곱셈형이거나 이와 동형이어야 함

        $$\begin{aligned}
        b(A \wedge B \mid C)
        &= G(b(A \mid C), b(B \mid A \wedge C))
        \end{aligned}$$

    - **부정의 일관성(Negation)**: 일변수 함수 $H$ 가 부정을 나타내기 위해서는 확률의 여사건 법칙 $1-p$ 에 대응하는 형태를 만족해야 함

        $$\begin{aligned}
        b(\neg A \mid B)
        &= H(b(A \mid B))
        \end{aligned}$$

    - **존재 가능성(Non-Triviality)**: 전적으로 확신하는 신념과 완전히 부정하는 신념은 서로 다른 값이어야 함

## Constraining Priors
-----

- **사전 확률 제약하기(Constraining Priors)**: 베이즈주의적 합리성이 주관적 신념의 형식적 정합화를 넘어선 정당화를 제공하기 위해서는 사전 확률 분포가 논리적(Logical), 경험적(Empirical), 또는 규범적(Objective) 제약 하에 형성되어야 함

- 주관적 베이즈주의(Subjective Bayes) \| Belief

    > 나는 진심으로 그러한 절대적 의미에서의 모든 확률 개념을 반대한다. (중략) 확률은 우리가 그에 대해 정신적으로 또는 본능적으로 내리는 평가와 독립적으로 존재하지 않는다는 의미에서 "확률은 존재하지 않는다(de Finetti, 1977, p.199)."

- 경험적 베이즈주의(Empirical Bayes) \| Utility

    > 그러므로 하나의 의견이 주어지면, 우리는 진위에 근거하여 그것을 칭찬하거나 책망할 수 있을 뿐이다. 특정한 형태의 습관이 주어지면 우리는 습관이 산출하는 신념도가 그것이 진리로 이끄는 실제 비율에 근접하거나 멀어지는가에 따라서 칭찬하거나 책망할 수 있다. 그렇다면 우리는 의견을 산출하는 습관들을 칭찬하거나 책망하는 것으로부터 파생적으로 의견들을 칭찬하거나 책망할 수 있다(Ramsey, 1926, p.51).

- 객관적 베이즈주의(Objective Bayes) \| Background, Non-Information

    > 무차별의 원리가 주장하는 것은 만약 우리의 관심의 대상이 여러 가지 대안 중 어느 것보다 더 예측할 만한 어떠한 알려진 이유가 없다면 그러한 지식에 상대적으로 이러한 대안 각각에 대한 주장들은 동일한 확률을 갖는다는 점이다(Keynes, 1921, p.42).

## Washing Out Priors
-----

- 객관성(Objectivity)

    > 절차의 합리성과 결과의 합리성이 대응하지 않을 경우는 어떻게 해야 하는가? (중략) 이 부분에서 우리의 논의에서 처음으로 합리성의 문제가 객관성의 문제와 관련된다. 진리성과 관련하여 어느 사회에서나 통용되는 기준들이 있으며 우리는 그것들이 객관적이라고 부른다. (중략) 베이즈주의적 객관성은 확실하지 않은 의견들 간 성립하는 간주관적 일치이다(이영의, 2015, p.41).

- 사전 확률 씻겨내기(Washing Out Priors)

    > 동전의 미래 행위에 대한 당신의 견해가 이웃 사람의 견해와 크게 다르더라도, 당신의 견해와 이웃 사람의 견해는 일상적으로 실험적인 던지기의 긴 연속에 베이즈의 정리를 적용하여 변형되어 거의 구별할 수 없게 될 것이다(Edwards, Lindman, and Savage, 1963, p.197). 즉, 다양한 신념들은 충분한 근거가 주어지면 간주관적으로 수렴하며, 이 일치를 객관적 신념 상태로 해석할 수 있다.

- 두브의 마틴게일 수렴 정리(Doob's Martingale Convergence Theorem)

    > 일반적 환경에서 조건화에 의한 확률 변화는 장기적으로 안정화된다(이영의, 2015, p.54). <br> $$\mathbb{E}\left[\theta \mid \mathcal{D}_{n}\right] \to \mathbb{E}\left[\theta \mid \mathcal{D}_{\infty}\right]$$

    - **마틴게일(Martingale)**: 현재까지의 모든 정보를 알고 있을 때($$\mathcal{F}_{n}$$), 다음 단계에서 확률변수 $$X_{n+1}$$ 의 조건부 기대값 $$\mathbb{E}\left[X_{n+1} \mid \mathcal{F}_{n}\right]$$ 이 현재 값 $$X_{n}$$ 과 같은 확률 과정

        $$\begin{aligned}
        \mathbb{E}\left[X_{n+1} \mid \mathcal{F}_{n}\right]
        &= X_{n}
        \end{aligned}$$

        - $\mathcal{F}_{n}$: $n$ 번째 시점까지 보유하고 있는 모든 정보를 나타내는 시그마 필드

- **조건화 규칙(Rule of Conditionalization)**: 인식적 불확실성 하에서의 합리적인 정보 갱신 원칙으로서, $n$ 시점에서 새로운 증거에 의해 형성된 사후 신념을 $n+1$ 시점에서의 사전 정보로서 수용하는 규칙

    - 엄밀 조건화 규칙(Rule of Strict Conditionalization):

        $$\begin{aligned}
        \Pi\left(\Theta\right)
        &= P\left(\Theta \mid \mathcal{D}\right)
        \end{aligned}$$

    - 제프리 조건화 규칙(Jeffrey's Conditionalization):

        $$\begin{aligned}
        \Pi\left(\Theta\right)
        &= Q\left(\mathcal{D}\right) \cdot P\left(\Theta \mid \mathcal{D}\right) + Q\left(\neg\mathcal{D}\right) \cdot p\left(\Theta \mid \neg\mathcal{D}\right)
        \end{aligned}$$

        - $Q\left(\mathcal{D}\right)$: 새로운 증거에 대한 인지 수준

## Problem of Induction
-----

- 귀납의 문제(Problem of Induction)

    > 특정 사례들로부터 보편 결론을 이끌어낼 수 없다.

- 후험 일치성(Posterior Consistency)

    > 확률 계산법을 준수하고 조건화 규칙에 따라 개정이 이루어진다면, 그리고 그러한 개정의 결과가 궁극적으로 참으로 수렴한다는 점이 보증된다면, 베이즈주의 추리에서는 귀납의 문제가 성립될 수 없다(이영의, 2015, p.55).

- 슈바르츠 정리(Schwartz’s Theorem)

    > 관측치 $$X \sim P(\theta)$$, 모수 $$\theta \in \Theta$$, 사전 확률 분포 $$\Pi$$, 참 모수 $$\theta^{*}$$ 에 대하여, $$\theta^{*}$$ 의 근방에 위치한 $$\theta$$ 가 사전 확률 분포에서 양의 질량을 가진다고 하자. 즉, $$\Pi\left(\{\theta : D_{KL}\left[P_{\theta^{*}} \Vert P_{\theta}\right] < \epsilon\}\right) > 0$$ 이다. 이때 사후 확률 분포는 장기적으로 $$\theta^{*}$$ 에 집중된다. 즉, $$\Pi\left(\theta^{*} \mid X_{1}, \cdots, X_{n}\right) \xrightarrow{n \to \infty} 1$$ 이다.

-----

## Reference

- [베이즈주의; 합리성으로부터 객관성으로의 여정](https://product.kyobobook.co.kr/detail/S000001052837)<br>이영의. (2015). 한국연구재단 저술총서 4. 한국문화사
---
order: 2
title: Space (2) Measure Space
date: 2025-02-04
categories: [MATHEMATICAL TECHS, 3.etc]
tags: [Mathematics]
math: true
image:
    path: /_post_refer_img/MathematicalTechs/3.etc/Thumbnail.jpg
---

## Space
-----

- **공간(Space)**: 어떤 종류의 수학적 대상을 모은 집합에 대하여, 그 집합 위에 고유의 연산 법칙을 제공하는 연산 구조가 부여되어 그 구조적 성질을 정의하고, 이로부터 유도 가능한 각종 성질들을 논의할 수 있는 수학적 시스템
    - **위상 공간(Topological Space)**: 어떤 종류의 수학적 대상에 `열림`을, 그 대상을 다루는 연산자에 `연속성`을 부여하기 위한 연산 구조
    - **측도 공간(Measure Space)**: 어떤 종류의 수학적 대상에 `크기`의 `측정 가능성`을 부여하기 위한 연산 구조

- **연산자(Operator)**: 어떠한 구조가 부여된 공간 내부 대상의 성질이나 관계 등을 수학적으로 다루는 행위자
    - **연산 법칙(Operation Law)**: 연산이 작동하는 방식과 규칙을 규정하는 공리
        - **공리(Axiom)**: 그 구조를 정의하기 위하여 기초적으로 받아들이는 명제

    - **연산 구조(Structure)**: 연산이 작동하는 방식이 공리적으로 고정된 시스템

    - **구조적 성질(Structural Property)**: 구조로 인하여 필연적으로 성립되는 전제적 성질

## Measure Space
-----

- **측도 공간(Measure Space)**: 원시 집합(underlying set) $\Omega$ 위에 정의된 시그마 대수(sigma-algebra)에 수치적 `크기` 개념을 부여하는 공간

    $$\begin{aligned}
    (\Omega, \mathcal{F}, \mu)
    \end{aligned}$$

    - **시그마 대수(Sigma-Algebra)**: 원시 집합(underlying set) $\Omega$ 의 멱집합(power set) $\mathcal{F} \subseteq 2^{\Omega}$ 으로서, $\Omega$ 의 부분집합 $A \subseteq \Omega$ 들의 집합

        $$\begin{aligned}
        \mathcal{F} \subseteq 2^{\Omega}
        \end{aligned}$$

        - $\Omega \in \mathcal{F}$
        - $A \in \mathcal{F} \Rightarrow A^{C} \in \mathcal{F}$
        - $A_{1}, A_{2}, \cdots \in \mathcal{F} \Rightarrow \bigcup_{i=1}^{\infty}{A_{i}} \in \mathcal{F}$

    - **측도(Measure)**: 측정 단위로서 시그마 대수 $\forall A \in \mathcal{F}$ 에 대하여 비음수성, 영집합, 가산 가법성을 만족하는 함수

        $$\begin{aligned}
        \mu : \mathcal{F} \rightarrow [0,\infty]
        \end{aligned}$$

        - 비음수성(Non-Negativity): $\mu(A) \ge 0$
        - 영집합(Null Empty Set): $\mu(\emptyset) = 0$
        - 가산 가법성(Countable Additivity): $A_{i} \in \mathcal{F}, A_{i} \cap A_{j \ne i} = \emptyset \Rightarrow \mu\left(\bigcup_{i=1}^{\infty}{A_{i}}\right) = \sum_{i=1}^{\infty}{\mu(A_{i})}$

- **푸시포워드 측도 공간(Pushforward Measure Space)**: 시그마 대수 간의 구조를 보존하는 사상 함수 $X$ 를 통해 원래의 측도 공간 $(\Omega, \mathcal{F}, \mu)$ 으로부터 유도된 새로운 측도 공간 $(\mathcal{X}, \mathcal{B}, \mu_{X})$

    $$\begin{aligned}
    (\Omega, \mathcal{F}, \mu) \rightarrow (\mathcal{X}, \mathcal{B}, \mu_{X})
    \end{aligned}$$

    - **사상 함수(Mapping Function)**: 실험 공간(Sampling Space) $\omega \in \Omega$ 을 관측 공간(Observation Space) 혹은 이미지 공간(Image Space) $x \in \mathcal{X}$ 에 대응시키는 함수

        $$\begin{aligned}
        X: \Omega \rightarrow \mathcal{X}
        \end{aligned}$$

    - **보렐 시그마 대수(Borel Sigma-Algebra)**: 이미지 공간(Image Space) $\mathcal{X}$ 위 열린 구간 $(a,b)$ 들로 생성되는 최소의 시그마 대수

        $$\begin{aligned}
        \mathcal{B}(\mathcal{X})
        := \sigma(\{(a,b) \subset \mathcal{X}\})
        \end{aligned}$$

        - $\forall B \in \mathcal{B}(\mathcal{X}) \Rightarrow X^{-1}(B) \in \mathcal{F}(\Omega)$
        - $\mu_{X}(B):=\mu(X^{-1}(B))$

- **L-p 공간(Lebesgue p-integrable space)**: 절대값을 $p$ 제곱한 후 르베그 적분(Lebesgue integral)한 값이 유한한 함수들로 구성된 공간

    $$\begin{aligned}
    L^{p}(\mathcal{X}, \mu) := \left\{f:\mathcal{X} \to \mathbb{R} \mid \int_{\mathcal{X}}{\vert f(x) \vert^{p} \text{d} \mu(x)} < \infty \right\}
    \end{aligned}$$

    - **르베그 측도(Lebesgue Measure)**: 실수 공간 $\mathbb{R}^{N}$ 위에서 각종 개념의 직관적 크기를 정의한 측도

        $$\begin{aligned}
        \text{d}\mu(x) := \text{d}x, \quad \forall x \in \mathbb{R}^{N}
        \end{aligned}$$

    - **르베그 적분(Lebesgue Integral)**: 사상 함수 $X: \Omega \to \mathcal{X}$ 를 통해 실수 공간 $\mathcal{X}$ 위에 정의된 보렐 시그마 대수 $\forall B \in \mathcal{B}$ 에 대하여 정의되는 르베그 측도 $x \in B$ 를 기준으로 함수 $f: \mathcal{X} \to \mathbb{R}$ 값의 누적 크기를 계산하는 도구로서, 원시 집합 $\Omega$ 에 크기를 부여하고자 하는 `개념`을 `함수`로 전환하는 장치

        $$\begin{aligned}
        \underbrace{M(f)}_{\text{area}}
        &:=\int_{x \in B}{\overbrace{f(x)}^{\text{height}}}\underbrace{\text{d}x}_{\text{width}}
        \end{aligned}$$

- **밀도(Density)**: 원 측도(Measure)의 기준 측도(Reference Measure) 기준 어떠한 개념의 단위당 크기

    > **밀도 존재 정리(Randon-Nickodym Theorem)** <br> 두 측도 $\nu, \mu$ 가 주어졌을 때, $\nu$ 가 $\mu$ 에 대하여 절대 연속(absolute continuity)이면($\nu \ll \mu$) $\forall A \in \mathcal{F}$ 에 대하여 $\nu(A) = \int_{A}{f\text{d}\mu}$ 을 만족하는 $f: \Omega \to [0,\infty]$ 가 존재한다. 이때 함수 $f:=\text{d}\nu / \text{d} \mu$ 를 $\mu$ 에 대한 $\nu$ 의 밀도 함수라고 한다. 또한 측도 $\mu$ 를 원 측도 $\nu$ 의 기준 측도(Reference Measure)라고 한다.

    $$\begin{aligned}
    \nu(x \in B)
    = \int_{x \in B}{\text{d}\nu(x)}
    = \int_{x \in B}{\frac{\text{d}\nu(x)}{\text{d}\mu(x)}}\text{d}\mu(x)
    \end{aligned}$$

## Probability Space
-----

- **확률 공간(Probability Space)**: 결과(outcome) $\omega$ 의 전체 집합 $\Omega$ 위에 정의된 사건(event) $\omega \in A$ 의 집합 $A \in \mathcal{F} \subseteq 2^{\Omega}$ 에 대하여 확률을 부여하는 공간

    $$\begin{aligned}
    (\Omega, \mathcal{F}, P)
    \end{aligned}$$

    - **확률 변수(Random Variable)**: 결과 $\omega \in \Omega$ 를 실수 공간 $x \in \mathcal{X}$ 에 대응시키는 사상 함수

        $$\begin{aligned}
        X: \Omega \rightarrow \mathcal{X}
        \end{aligned}$$

    - **확률 측도(Probability Measure)**: $P_{X}(\mathcal{X})=1$ 인 특수한 측도

        $$\begin{aligned}
        P_{X} : \mathcal{B}(\mathcal{X}) \rightarrow [0,1]
        \end{aligned}$$

    - **확률 밀도(Probability Density)**: 확률 측도 $P_{X}$ 의 기준 측도 $x$ 단위당 확률의 상대량

        $$\begin{aligned}
        P_{X}(x \in B)
        = \int_{x \in B}{p(x)}\text{d}x
        \end{aligned}$$

- **`example` Gaussian Prob. Dist.**
    - Random Variable:

        $$\begin{aligned}
        X: \Omega \rightarrow \mathbb{R}
        \end{aligned}$$

    - Probability Measure:

        $$\begin{aligned}
        P_{X}
        &= \mathcal{N}(\mu, \sigma^{2})
        \end{aligned}$$

    - Probability Density Function:

        $$\begin{aligned}
        p(x)
        &= \frac{1}{\sqrt{2 \pi \sigma^{2}}}\exp\left[-\frac{(x-\mu)^{2}}{2 \sigma^{2}}\right]
        \end{aligned}$$
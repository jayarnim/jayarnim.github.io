---
order: 1
title: Space (1) Topological Space
date: 2025-02-03
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

## Topological Space
-----

- **위상 공간(Topological Space)**: 원시 집합(underlying set) 위에 열린 집합(open set)들의 체계를 부여한 공간

    $$\begin{aligned}
    (X, \tau)
    \end{aligned}$$

    - **위상(Topology)**: 원시 집합(underlying set) $X$ 의 멱집합(power set) $\tau \subseteq 2^{X}$ 으로서, $X$ 의 열린 부분집합들의 모임

        $$\begin{aligned}
        \tau \subseteq 2^{X}
        \end{aligned}$$

        - $\emptyset,X \in \tau$
        - $U_{1},U_{2},\cdots \in \tau \Rightarrow \bigcup_{i=1}^{\infty}{U_{i}} \in \tau$
        - $U_{1},U_{2},\cdots \in \tau \Rightarrow \bigcap_{i=1}^{\infty}{U_{i}} \in \tau$

    - **기저(Base, Basis for Topology)**: 생성자(generator)로서 위상 공간 $(X, \tau)$ 에서 $\tau$ 를 생성할 수 있는 위상의 모음 $\mathcal{B}$

        $$\begin{aligned}
        \tau
        &= \left\{\bigcup_{i \in I}{B_{i}} \mid B_{i} \in \mathcal{B} \right\}
        \end{aligned}$$

        - $\forall x \in X, \exists B \in \mathcal{B} \quad \text{such that} \quad x \in B$
        - $x \in B_{1} \cap B_{2} \Rightarrow \exists B_{3} \in \mathcal{B} \quad \text{such that} \quad x \in B_{3} \subseteq B_{1} \cap B_{2}$

- **내부성(Interior)**: 어떤 원소가 집합의 진정한 일부임을 보장하는 성질로서, 어떤 집합 $A$ 의 원소 $x$ 가 $x \in A$ 임이 그 근방의 열린 집합만으로 충분히 결정되는 성질

    $$\begin{aligned}
    \text{int}(A)
    := \{x \in A \mid \exists U \in \tau \ \text{such that}\ x \in U \subseteq A\}
    \end{aligned}$$

- **열림(Open)**: 내부점의 근방에 내부점만 존재하는 성질로서, 집합 $A$ 의 모든 원소 $\forall x \in A$ 에 대하여, 원소마다 해당 원소를 포함하는 동시에 $A$ 에 완전히 포함되는 열린 부분집합 $x \in U \subseteq A$ 이 존재하는 성질

    $$\begin{aligned}
    \text{int}(A)
    = A
    \end{aligned}$$

- **연속성(Continuity)**: 연산자 $f: (X, \tau_{X}) \to (Y, \tau_{Y})$ 에 대하여 입력에 작은 변화를 주었을 때 그 출력 정보가 끊기거나 갑작스런 변화 없이 부드럽게 이어짐을 보장하는 성질로서, 즉, 출력 공간에서의 연속적인 변화가 입력 공간에서도 연속적으로 대응되는 성질

    $$\begin{aligned}
    f^{-1}(V) \in \tau_{X} \quad \text{for} \quad \forall V \in \tau_{Y}
    \end{aligned}$$

## Special Cases
-----

- **거리 공간(Metric Space)**: 어떤 집합 $X$ 에 대하여 수치적 `거리` 개념이 정의되어 일부 개념들을 정량적으로 `측정`할 수 있는 위상 공간

    $$\begin{aligned}
    (X,d)
    \end{aligned}$$

    - **거리(Metric)**: 비음수성, 동일성, 대칭성, 삼각 부등식을 만족하는 연산자

        $$\begin{aligned}
        d:X \times X \to \mathbb{R}
        \end{aligned}$$

        - 비음수성(Non-Negativity): $d(x,y) \ge 0$
        - 동일성(Identity of indiscernibles): $d(x,y)=0 \Leftrightarrow x=y$
        - 대칭성(Symmetry): $d(x,y)=d(y,x)$
        - 삼각 부등식(Triangle Inequality): $d(x,z) \le d(x,y) + d(y,z)$

- **노름 공간(Normed Space)**: 벡터 공간 $V$ 에 대하여 `노름` 개념이 정의되어 이를 통해 벡터의 `크기`와 `길이`를 측정할 수 있는 거리 공간

    $$\begin{aligned}
    (V, \Vert \cdot \Vert)
    \end{aligned}$$

    - **노름(Norm)**: $\forall \mathbf{x},\mathbf{y} \in V$, $\forall \alpha \in \mathbb{R}$ 에 대하여 양의 정부호성, 동차성, 삼각 부등식을 만족하는 연산자

        $$\begin{aligned}
        \Vert \cdot \Vert: V \to \mathbb{R}
        \end{aligned}$$

        - 양의 정부호성(Positive Definiteness): $\Vert \mathbf{x} \Vert \ge 0, \Vert \mathbf{x} \Vert = 0 \Leftrightarrow \mathbf{x} = \mathbf{0}$
        - 동차성(Homogeneity): $\Vert \alpha \mathbf{x} \Vert = \vert \alpha \vert \cdot \Vert \mathbf{x} \Vert$
        - 삼각 부등식(Triangle Inequality): $\Vert \mathbf{x} + \mathbf{y} \Vert \le \Vert \mathbf{x} \Vert + \Vert \mathbf{y} \Vert$

- **내적 공간(Inner Product Space)**: 벡터 공간 $V$ 에 대하여 `내적` 개념이 정의되어 이를 통해 `방향`과 `정렬`을 측정할 수 있는 노름 공간

    $$\begin{aligned}
    (V, \left<\cdot,\cdot\right>)
    \end{aligned}$$

    - **내적(Inner Product)**: $\forall \mathbf{x},\mathbf{y},\mathbf{z} \in V$, $\forall \alpha \in \mathbb{R}$ 에 대하여 선형성, 대칭성, 양의 정부호성, 내적 유도 노름의 일관성을 만족하는 연산자

        $$\begin{aligned}
        \left<\cdot,\cdot\right>: V \times V \to \mathbb{R}
        \end{aligned}$$

        - 선형성(Linear in First Argument): $\left<\alpha\mathbf{x}+\mathbf{y},\mathbf{z}\right>=\alpha\left<\mathbf{x},\mathbf{z}\right>+\left<\mathbf{y},\mathbf{z}\right>$
        - 대칭성(Symmetry): $\left<\mathbf{x},\mathbf{y}\right>=\left<\mathbf{y},\mathbf{x}\right>$
        - 양의 정부호성(Positive-definiteness): $\left<\mathbf{x},\mathbf{x}\right> \ge 0, \left<\mathbf{x},\mathbf{x}\right> = 0 \Leftrightarrow \mathbf{x}=\mathbf{0}$
        - 내적 유도 노름의 일관성: $\Vert \mathbf{x} \Vert :=\sqrt{\left<\mathbf{x},\mathbf{x}\right>}$

## Applications
-----

- **바나흐 공간(Banach Space)**: 완비 노름 공간

    $$\begin{aligned}
    (V, \Vert \cdot \Vert)
    \end{aligned}$$

    - **코시 수열(Cauchy Sequence)**: 집합 $X$에 거리 함수 $d$가 정의되어 있을 때, 다음을 만족하는 수열 $(x_{i})$

        $$\begin{aligned}
        \forall \epsilon >0, \ \exists N \in \mathbb{N}, \ \forall i,j > N \Rightarrow d(x_{i}, x_{j}) < \epsilon
        \end{aligned}$$

    - **완비성(Completeness)**: (정의된 거리에 따라) 모든 코시 수열 $(x_{n})$ 이 수렴하는 성질

        $$\begin{aligned}
        \lim_{n \to \infty}{d(x_{n},x)} = 0
        \end{aligned}$$

- **힐베르트 공간(Hilbert Space)**: 완비 내적 공간

    $$\begin{aligned}
    (V, \left<\cdot, \cdot \right>)
    \end{aligned}$$

    - **리즈의 표현 정리(Riesz Representation Theorem)**

        >힐베르트 공간 $\mathcal{H}$ 위에 정의된 선형성과 연속성을 만족하는 연산자 $\phi: \mathcal{H} \to \mathbb{R}$ 와 임의의 벡터 $u \in \mathcal{H}$ 에 대하여, $\phi(u):=\left<u,v\right>$ 를 성립시키는 고유한 벡터 $v \in \mathcal{H}$ 가 존재함

        $$\begin{aligned}
        \exists v \in \mathcal{H} \quad \text{such that} \quad \phi(u):=\left<u,v\right>, \quad \forall u \in \mathcal{H}
        \end{aligned}$$

## RKHS
-----

- **Moore-Aronzajin Theorem**

    >대칭성(Symmetry)과 양의 정부호성(Positive Definiteness)을 만족하는 임의의 커널 함수(Kernel Function) $K:\mathcal{X} \times \mathcal{X} \to \mathbb{R}$ 에 대하여, 그로부터 유일하게 구성되는 무한 차원 힐베르트 공간 $\mathcal{H}_{K}$ 이 존재한다.

    $$\begin{aligned}
    \mathcal{H}_{K}
    &:= \overline{\mathcal{H}_{0}}\\
    \mathcal{H}_{0}
    &:= \text{Span}\left\{K(x,\cdot) \mid x \in \mathcal{X}\right\}
    \end{aligned}$$

    - 기저(Basis):

        $$\begin{aligned}
        \mathcal{B}
        &= \left\{K(x_{i}, \cdot) \mid i=1,2,\cdots,\infty \right\}
        \end{aligned}$$

    - Each element $\forall f \in \mathcal{H}_{K}$ is expressed as a `linear combination` of the basis elements:

        $$\begin{aligned}
        f(x)
        &= \sum_{i}{\alpha_{i} \cdot K(x_{i}, x)}
        \end{aligned}$$

- **재생 커널(Reproducing Kernel)**:

    | Name | Function |
    |---|---|
    | Linear | $$X \cdot X^{\prime}$$ |
    | Polynomial | $$\left(X \cdot X^{\prime} + \beta\right)^{d}$$ |
    | RBF | $$\exp{\left[-\displaystyle\frac{\Vert X-X^{\prime} \Vert^{2}}{2\ell^{2}}\right]}$$ |
    | Matern | $$\displaystyle\frac{2^{1-\nu}}{\Gamma\left(\nu\right)} \cdot \left(\displaystyle\frac{\sqrt{2\nu} \Vert X-X^{\prime} \Vert}{\ell}\right)^{\nu} \cdot K_{\nu}\left(\displaystyle\frac{\sqrt{2\nu} \Vert X-X^{\prime} \Vert}{\ell}\right)$$ |

    - 대칭성(Symmetry):

        $$\begin{aligned}
        K(x, x^{\prime})
        &= K(x^{\prime}, x)
        \end{aligned}$$

    - 양의 정부호성(Positive Definiteness):

        $$\begin{aligned}
        \sum_{i,j}{\alpha_{i}\alpha_{j}K(x_{i},x_{j})} \ge 0
        \end{aligned}$$

- **RKHS(`R`eproducing `K`ernel `H`ilbert `S`pace)**: $\forall f \in \mathcal{H}_{K}$ 에 대하여 `평가` 개념이 정의되어 정의역 $x \in \mathcal{X}$ 에 대한 함수 값 $f(x) \in \mathbb{R}$ 을 측정할 수 있는 힐베르트 공간

    $$\begin{aligned}
    (\mathcal{H}_{K}, \delta_{X})
    \end{aligned}$$

    - **평가(Evaluation Functional)**: 주어진 점 $x \in \mathcal{X}$ 에 대하여 해당 점에서 함수 $f \in \mathcal{H}_{K}$ 의 값 $f(x) \in \mathbb{R}$ 을 반환하는 연산자

        $$\begin{aligned}
        \delta_{X}:\mathcal{H}_{K} \to \mathbb{R},f \mapsto f(x)
        \end{aligned}$$

- **재생(Reproducing)** : $f:\mathcal{X} \to \mathbb{R}$ 를 직접 계산하지 않고도 재생 커널 $K:\mathcal{X} \times \mathcal{X} \to \mathbb{R}$ 을 통해 함수 값 $f(x)$ 을 재생할 수 있는 성질

    - $\because f,g \in \mathcal{H}_{K}$:

        $$\begin{aligned}
        f(\cdot)
        &= \sum_{i}{\alpha_{i}K(x_{i},\cdot)}\\
        g(\cdot)
        &= \sum_{j}{\beta_{j}K(x_{j},\cdot)}
        \end{aligned}$$

    - inner product:

        $$\begin{aligned}

        \left<f,g\right>
        &:= \sum_{i,j}{\alpha_{i}\beta_{j}K(x_{i},x_{j})}
        \end{aligned}$$

    - $\because$ Riesz Representation Theorem:

        $$\begin{aligned}
        \exists g \in \mathcal{H}_{K} \quad \text{such that} \quad \delta_{X}(f):=\left<f,g\right>, \quad \forall f \in \mathcal{H}_{K}
        \end{aligned}$$
 
    - therefore:

        $$\begin{aligned}
        \delta_{X}(f)
        = f(x)
        = \left<f, K(\cdot, x)\right>, \quad \forall f \in \mathcal{H}_{K}
        \end{aligned}$$
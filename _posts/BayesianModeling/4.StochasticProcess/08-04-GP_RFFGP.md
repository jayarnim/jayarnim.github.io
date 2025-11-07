---
order: 4
title: GP (3) Random Fourier Features Gaussian Process
date: 2025-08-04
categories: [BAYES, 4.stochastic process]
tags: [Bayesian, Stochastic Process, Time Series, Nonparametric Estimation, Gaussian Process, Multi-Variate Gaussian Dist., Fourier]
math: true
image:
    path: /_post_refer_img/BayesianModeling/4.StochasticProcess/Thumbnail.jpg
---

## GP
-----

- **가우시안 프로세스(`G`aussian `P`rocess)**:

    > 순차 입력 $x_{1},x_{2},\cdots \in \ell^{2}$ 에 대한 출력 $f(x_{1}),f(x_{2}),\cdots \in \ell^{2}$ 이 입력 공간 $\ell^{2}$ 전체에 대하여 확률 분포를 가지는 확률 과정으로서, 함수 자체를 확률변수로 취하는 함수 분포

    $$\begin{aligned}
    f(\cdot) \sim \mathcal{GP}(\mu(\cdot), K(\cdot, \cdot))
    \end{aligned}$$

- $f(x) \sim \mathcal{N}(\mu(x),K(x,x))$: 입력값 $x$ 에 대한 출력값

    $$\begin{aligned}
    f(x) \in \ell^{2}
    \end{aligned}$$

- $\mathbf{f} \sim \mathcal{N}(\mu,\Sigma)$: 입력값 $x_{1},x_{2},\cdots$ 에 대한 출력값 $f(x_{1}),f(x_{2}),\cdots$ 벡터

    $$\begin{aligned}
    \mathbf{f}
    := \begin{bmatrix}
    f(x_{1})\\
    f(x_{2})\\
    \vdots
    \end{bmatrix}
    \in \ell^{2}
    \end{aligned}$$

    - $\mu$: 입력값 $x_{1},x_{2},\cdots$ 에 대한 출력값 $f(x_{1}),f(x_{2}),\cdots$ 의 평균 벡터

        $$\begin{aligned}
        \mu
        =\begin{bmatrix}
        \mu(x_{1}) \\
        \mu(x_{2}) \\
        \vdots
        \end{bmatrix}
        \end{aligned}$$

    - $\Sigma$: 입력값 $x_{1},x_{2},\cdots$ 에 대한 출력값 $f(x_{1}),f(x_{2}),\cdots$ 의 공분산 행렬

        $$\begin{aligned}
        \Sigma
        &=\begin{bmatrix}
        K(x_{1},x_{1}) & K(x_{1},x_{2}) & \cdots \\
        K(x_{2},x_{1}) & K(x_{2},x_{2}) & \cdots \\
        \vdots & \vdots & \ddots
        \end{bmatrix}
        \end{aligned}$$

- $f(\cdot) \sim \mathcal{GP}(\mu(\cdot), K(\cdot, \cdot))$: $\forall x$ 에 대하여 $f(\forall x)$ 를 정의하는 규칙

    $$\begin{aligned}
    f(\cdot) \in \mathcal{H}_{K}
    \end{aligned}$$

## RKHS
-----

- **RKHS(`R`eproducing `K`ernel `H`ilbert `S`pace)**: 특정한 재생 커널(Reproducing Kernel)에 의해 정의된 힐베르트 공간으로서, 이 함수 공간에서 모든 함수는 커널 함수의 선형 조합으로 표현됨

    $$\begin{aligned}
    f(x)
    &= \sum_{i=1}^{n}{\alpha_{i} \cdot K(x, x_{i})}
    \end{aligned}$$

- **힐베르트 공간(Hilbert Space)** : 유클리드 공간을 일반화한 개념으로서, 내적과 거리가 정의된 완비 공간

    $$\begin{aligned}
    \langle f, g \rangle _{\mathcal{H}}:=\sum_{i=1}^{n}\sum_{j=1}^{m}{\alpha_{i}\beta_{j}K(x_{i}, x_{j})}, \quad \Vert f \Vert _{\mathcal{H}} := \sqrt{\langle f, f \rangle _{\mathcal{H}}}
    \end{aligned}$$

    - $f(x)=\sum_{i=1}^{n}{\alpha_{i} \cdot K(x, x_{i})}$
    - $g(x)=\sum_{j=1}^{m}{\beta_{j} \cdot K(x, x_{j})}$

- **재생(Reproducing)** : 모든 함수 $f(x)$ 가 커널 함수의 선형 조합으로 표현됨에 따라 $f(x)$ 를 직접 계산하지 않고도 커널 함수를 통해 함수 값을 재생할 수 있는 성질

    $$\begin{aligned}
    f(x)
    = \langle f, K(\cdot, x) \rangle _{\mathcal{H}}
    = \left\langle \sum_{i=1}^{n}{\alpha_{i} \cdot K(\cdot, x_{i})}, K(\cdot, x) \right\rangle _{\mathcal{H}}
    \end{aligned}$$

## RFF
-----

- **`R`andom `F`ourier `F`eatures**:

    >임의의 조건을 만족하는 커널은 푸리에 변환을 통해 어떤 확률 밀도 함수의 기대값으로 표현 가능하다. 그리고 이 커널에 의해 정의되는 무한 차원의 함수 공간 $RKHS$ 는 해당 커널의 스펙트럼 밀도 $p(w)$ 로부터 샘플링된 $w$ 에 대하여 정의되는 유한 개 무작위 기저 함수 $\phi_{W \sim P}(x) \in RKHS$ 들의 선형 결합(혹은 내적)의 기대값으로써 근사될 수 있다.

    $$\begin{aligned}
    K(x,x^{\prime})
    &= \left<K(\cdot, x), K(\cdot, x^{\prime})\right>_{\mathcal{H}}\\
    &\approx \left<\phi(x), \phi(x^{\prime})\right>_{\mathbb{R}^{K}}\\
    &= \mathbb{E}_{W \sim P}\left[\phi_{w}(x) \cdot \phi_{w}(x^{\prime})\right]
    \end{aligned}$$
    
    - $\phi(x) = \sqrt{2/K} \cdot \begin{bmatrix}\cos{(w_{1}^{T}x+b_{1})} & \cos{(w_{2}^{T}x+b_{2})} & \cdots & \cos{(w_{K}^{T}x+b_{K})}\end{bmatrix}$

- **푸리에 변환(fourier transform)**: 임의의 조건을 만족하는 함수는 주기 함수의 기대값으로 표현될 수 있음

    $$\begin{aligned}
    f(x)
    &= \int_{\mathbb{R}^{K}}{\exp{\left[i \cdot w^{T}x\right]} \cdot p(w)}\text{d}w
    \end{aligned}$$

    - $f(x)$:
        - $f \in L^{1}(\mathbb{R}^d)$: 적분 가능 함수
        - $f \in L^{2}(\mathbb{R}^d)$: 제곱 적분 가능 함수

    - $p(w)$: 확률 밀도 함수로서 함수 $f(x)$ 의 스펙트럼 밀도(Spectrum Density)

    - $\exp{[i \cdot w^{T}x]}$: 복소 지수 함수(complex exponential function)

        - $i$: 허수
        - $\theta= w^{T}x$: 운동 주기에서 입력값의 위치
        - $w$: 주파수로서 운동의 방향 및 속도
        - $x$: 입력값

- **보흐너 정리(Bochner’s theorem)**: 임의의 조건을 만족하는 커널 $K: \mathbb{R}^{d} \times \mathbb{R}^{d} \rightarrow \mathbb{R}$ 은 어떤 확률 밀도 함수 $p(w)$ 의 푸리에 쌍임

    $$\begin{aligned}
    K(x,x^{\prime})
    &= \int_{\mathbb{R}^{K}}{\exp{\left[i \cdot w^{T}(x-x^{\prime})\right]} \cdot p(w)}\text{d}w
    \end{aligned}$$

    - 연속성(continuous):

        $$
        \begin{aligned}
        \Vert x - a \Vert &< \delta\\
        \Vert x^{\prime} - b \Vert &< \delta
        \end{aligned} \quad
        \Rightarrow \quad
        \vert K(x,x^{\prime}) - K(a,b) \vert < \epsilon
        \quad \text{for} \quad 
        \begin{aligned}
        \forall \epsilon &> 0\\
        \exists \delta &> 0
        \end{aligned}
        $$

    - 이동 불변성(shift-invariant):

        $$\begin{aligned}
        K(x,x^{\prime})
        &=K(x-x^{\prime})
        \end{aligned}$$

    - 양의 정부호성(positive definite):

        $$
        \sum_{i=1}^{n}{\sum_{j=1}^{n}{c_{i} \cdot c_{j} \cdot K(x_{i},x_{j})}}>0 \quad \text{for} \quad
        \begin{aligned}
        \forall n &\in \mathbb{N}\\
        \forall x_{1},x_{2},\cdots,x_{n} &\in \mathbb{R}^{d}\\
        \forall \mathbf{c} &\in \mathbb{R}^{n} \setminus \{\mathbb{0}\}
        \end{aligned}$$

- **오일러 공식(Euler's formula)**: 복소 지수 함수는 주기 함수(사인과 코사인)의 조합으로 분해될 수 있음

    $$\begin{aligned}
    \exp{[i \cdot \theta]}
    &=\cos{\theta} + i \cdot \sin{\theta}
    \end{aligned}$$

    - $\because$ fourier transform:

        $$\begin{aligned}
        K(x-x^{\prime})
        &= \mathbb{E}_{W \sim P}[\exp(i \cdot w^{T}(x-x^{\prime}))]
        \end{aligned}$$

    - segmentation:

        $$\begin{aligned}
        \exp[i \cdot w^{T}(x-x^{\prime})]
        &= \exp[i \cdot w^{T}x] \cdot \exp[-i \cdot w^{T}x^{\prime}]\\
        &= \big[\cos{(w^{T}x)}+i\sin{(w^{T}x)}\big]\cdot\big[\cos{(w^{T}x^{\prime})}-i\sin{(w^{T}x^{\prime})}\big]\\
        &= \underbrace{\cos{(w^{T}x)} \cdot \cos{(w^{T}x^{\prime})} + \sin{(w^{T}x)} \cdot \sin{(w^{T}x^{\prime})}}_{\text{real part}} - i(\cdots)
        \end{aligned}$$

    - only take the real part:

        $$\begin{aligned}
        \exp[i \cdot w^{T}(x-x^{\prime})]
        &\approx \cos{w^{T}(x-x^{\prime})}
        \end{aligned}$$

        - $\because \cos{(a-b)} = \cos{a} \cdot \cos{b} + \sin{a} \cdot \sin{b}$

- **무작위 푸리에 기저 함수(`R`andom `F`ourier `F`eatures)**: 유한 차원의 선형 함수 공간을 정의하는 기저 함수

    $$\begin{aligned}
    \phi(x)
    &= \sqrt{2}\cos{(w^{T}x + b)} \quad \text{for} \quad b \sim \text{Uniform}(0,2\pi)
    \end{aligned}$$

    - assumption:

        $$\begin{aligned}
        \frac{1}{2}\cos{w^{T}(x-x^{\prime})}
        &=\mathbb{E}_{b}[\cos{(w^{T}x + b)} \cdot \cos{(w^{T}x^{\prime} + b)}]
        \end{aligned}$$

    - expression expansion:

        $$\begin{aligned}
        \cos{(w^{T}x + b)} \cdot \cos{(w^{T}x^{\prime} + b)}
        &=\frac{1}{2}\left[\cos{w^{T}(x-x^{\prime})} + \cos{(w^{T}(x+x^{\prime})+2b)}\right]
        \end{aligned}$$

        - $\because \cos{a}\cdot\cos{b} = \displaystyle\frac{1}{2}[\cos{(a-b)} + \cos{(a+b)}]$

    - expected value:

        $$\begin{aligned}
        &\mathbb{E}_{b}\left[\cos{(w^{T}x + b)} \cdot \cos{(w^{T}x^{\prime} + b)}\right]\\
        &= \frac{1}{2}\Big(\cos{w^{T}(x-x^{\prime})} + \mathbb{E}_{b}[\cos{(w^{T}(x+x^{\prime})+2b)}]\Big)\\
        &= \frac{1}{2}\cos{w^{T}(x-x^{\prime})}
        \end{aligned}$$

        - $\because \int_{0}^{2\pi}{\cos{(2b + \cdots)}}\text{d}b=0$

- **Therefore**:

    $$\begin{aligned}
    K(x,x^{\prime})
    &\approx \mathbb{E}_{W \sim P}\left[\exp{i \cdot w^{T}(x-x^{\prime})}\right]\\
    &\approx \mathbb{E}_{W \sim P}\left[\cos{w^{T}(x-x^{\prime})}\right]\\
    &\approx \mathbb{E}_{W \sim P}\Big(\mathbb{E}_{b \sim \text{Uniform}(0,2\pi)}\left[\left<\phi_{w,b}(x), \phi_{w,b}(x^{\prime})\right>\right]\Big)
    \end{aligned}$$

## RFF-GP
-----

- **RFF-GP(`R`andom `F`ourier `F`eatres `G`aussian `P`rocess)**:

    >커널 함수 $K(\cdot,\cdot)$ 에 대하여 정의되는 무한 차원의 재생 커널 힐베르트 공간 $$f \in \mathcal{H}_{K}$$ 을 무작위 푸리에 기저 함수(Random Fourier Features) $\phi(\cdot)$ 에 대하여 정의되는 유한 차원 선형 함수 공간 $$f \in \mathcal{H}_{RFF} \subset \mathcal{H}_{K}$$ 으로 근사함으로써(Subspace Approximation), 가우시안 프로세스 $$f(\cdot) \sim \mathcal{GP}(\mu(\cdot),K(\cdot,\cdot))$$ 를 선형 회귀 모형 $$\phi(\cdot)^{T}\theta \sim \mathcal{GP}(0,\left<\phi(\cdot),\phi(\cdot)\right>)$$ 의 형태로 근사하는 방법론

    $$\begin{aligned}
    f(x) \mid \theta
    &\sim \mathcal{N}(0,\left<\phi(x),\phi(x^{\prime})\right>)
    \end{aligned}$$

- RFF Summary:

    $$\begin{aligned}
    K(x,x^{\prime})
    \approx \phi(x)^{T}\phi(x^{\prime})
    \end{aligned}$$

- original $f(\cdot)$ be approximated linear combination of basis function:

    $$\begin{aligned}
    f(x)
    &= \sum_{i=1}^{n}{\alpha_{i} \cdot K(x,x_{i})}\\
    &\approx \sum_{i=1}^{n}{\alpha_{i} \cdot \phi(x)^{T}\phi(x_{i})}\\
    &= \phi(x)^{T}\underbrace{\sum_{i=1}^{n}{\alpha_{i}\phi(x_{i})}}_{=:\theta}
    \end{aligned}$$

    - $\phi(x)$ is chosen randomly, but fixed once drawn
    - to give probability to $f(x)$, $\theta$ must be set as a probabilistic variable

- `Prior` of $f(x)$:

    $$\begin{aligned}
    \theta \sim \mathcal{N}(0,\mathbf{I})
    \end{aligned}$$

- `Posterior` of $f(x) \mid \theta$:

    $$\begin{aligned}
    f(x) \mid \theta
    &\sim \mathcal{N}(0,\left<\phi(x),\phi(x^{\prime})\right>)
    \end{aligned}$$

    - `Mean` of $f(x) \mid \theta$:

        $$\begin{aligned}
        \mathbb{E}[f(x)]
        &=\mathbb{E}[\phi(x)^{T}\theta]\\
        &=\phi(x)^{T}\mathbb{E}[\theta]\\
        &=0
        \end{aligned}$$

    - `Covariance` of $f(x) \mid \theta$:

        $$\begin{aligned}
        \mathbb{E}[f(x)],\mathbb{E}[f(x^{\prime})]
        &=0\\
        \\
        \mathbb{E}[f(x) \cdot f(x^{\prime})]
        &=\mathbb{E}[\phi(x)^{T}\theta\theta^{T}\phi(x^{\prime})]\\
        &=\phi(x)^{T}\mathbb{E}[\theta\theta^{T}]\phi(x^{\prime})\\
        &=\phi(x)^{T}\mathbf{I}\phi(x^{\prime}) \quad \because \Sigma=\mathbb{E}[(\theta-\mu)(\theta-\mu)^{T}]\\
        &=\left<\phi(x),\phi(x^{\prime})\right>\\
        \\
        \therefore \text{Cov}[f(x), f(x^{\prime})]
        &= \mathbb{E}[f(x) \cdot f(x^{\prime})]-\mathbb{E}[f(x)]\cdot\mathbb{E}[f(x^{\prime})]\\
        &= \left<\phi(x),\phi(x^{\prime})\right>\\
        \end{aligned}$$
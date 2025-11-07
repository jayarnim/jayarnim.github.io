---
order: 8
title: Categorical and Extension
date: 2025-07-08
categories: [2.STATISTICAL TECHS, 1.probability]
tags: [statistics, uncertainty, probability, random variable, probability distribution, discrete random variable, categorical data analysis, categorical distribution, multinomial distribution]
math: true
description: >-
    Based on the following lectures <br>
    (1) “Statistics (2018-1)” by Prof. Sang Ah Lee, Dept. of Economics, College of Economics & Commerce, Kookmin Univ. <br>
    (2) "Statistical Models and Application (2024-1)" by Prof. Yeo Jin Chung, Dept. of Data Science, The Grad. School, Kookmin Univ. <br>
    (3) “Bayesian Modeling (2024-1)” by Prof. Yeo Jin Chung, Dept. of AI, Big Data & Management, College of Business Administration, Kookmin Univ.
image:
    path: /_post_refer_img/2.STATS/1.probability/Thumbnail.jpg
---

## Categorical
-----

- **카테고리 분포(Categorical Distribution)**: 베르누이 분포의 실현 가능한 범주를 일반화한 분포로서, $K$ 개 범주 중 하나가 실현되는 단일 시행에서 특정 범주의 실현 여부를 나타내는 분포

    $$
    X\sim\mathrm{Categorical}(\Pi)
    $$

    - $$X$$: 단일 시행에서 발생할 수 있는 결과를 $$K$$ 차원 단위 기저 집합 $$\{\mathbf{e}_{1},\cdots,\mathbf{e}_{K}\}$$ 으로 표현하였을 때 그 중 하나를 실현값으로 가지는 벡터 확률변수

        $$
        X\in\left\{\mathbf{e}_{1},\cdots,\mathbf{e}_{K}\right\} \subset \mathbb{R}^{K}\quad\mathrm{for}\quad\mathbf{e}_{k}=\{\delta_{i,k}\}_{i=1}^{K}
        $$

    - $\Pi$: 단일 시행에서 각 범주가 실현될 가능성을 나타내는 확률 파라미터

        $$
        \Pi=\begin{pmatrix}\pi_{1}&\cdots&\pi_{K}\end{pmatrix}^{T}\quad\mathrm{for}\quad\pi_{k}:=P(X=\mathbf{e}_{k})
        $$

- probability mass function:

    $$\begin{aligned}
    p(X=\mathbf{e}_{k}\mid\Pi)
    =\prod_{k=1}^{K}{\pi_{k}^{x_{k}}}
    \quad\mathrm{for}\quad
    \begin{cases}\mathbf{x}=\begin{pmatrix}x_{1}&\cdots&x_{K}\end{pmatrix}^{T}\in\{0,1\}^{K}\\
    \sum_{k=1}^{K}{x_{k}}=1
    \end{cases}
    \end{aligned}$$

- moment generating function:

    $$\begin{aligned}
    M_{X}(\mathbf{t})
    &=\mathbb{E}_{p(x)}\left[\exp{\mathbf{t}^{T}X}\right]\\
    &=\sum_{X}{\exp{\mathbf{t}^{T}X}\cdot p(x)}\\
    &=\sum_{k=1}^{K}{\exp{\mathbf{t}^{T}\mathbf{e}_{k}}\cdot P(X=\mathbf{e}_{k})}\\
    &=\sum_{k=1}^{K}{\exp{t_{k}}\cdot\pi_{k}}
    \end{aligned}$$

    - $\mathbb{E}\left[X\right]=\nabla_{t}M_{X}(t)\vert_{t=0}=\Pi$
    - $\mathbb{E}\left[XX^{T}\right]=\nabla_{t}^{2}M_{X}(t)\vert_{t=0}=\mathrm{diag}(\Pi)$
    - $\mathrm{Cov}\left[X,X^{\prime}\right]=\mathbb{E}\left[XX^{T}\right]-\mathbb{E}\left[X\right]\mathbb{E}\left[X\right]^{T}=\mathrm{diag}(\Pi)-\Pi\Pi^{T}$

- canonical form:

    $$\begin{aligned}
    p(\mathbf{x})
    &=\prod_{k=1}^{K}{\pi_{k}^{x_{k}}}\\
    &=\exp{\left[\sum_{k=1}^{K}{x_{k}\log{\pi_{k}}}\right]}\\
    \\
    \sum_{k=1}^{K}{x_{k}\log{\pi_{k}}}
    &=\sum_{k=1}^{K-1}{x_{k}\log{\pi_{k}}}+x_{K}\log{\pi_{K}}\\
    &=\sum_{k=1}^{K-1}{x_{k}\log{\pi_{k}}}+\left(1-\sum_{k=1}^{K-1}{x_{k}}\right)\log{\pi_{K}}\\
    &=\sum_{k=1}^{K-1}{x_{k}\left(\log{\pi_{k}}-\log{\pi_{K}}\right)}+\log{\pi_{K}}\\
    &=\sum_{k=1}^{K-1}{x_{k}\cdot\log{\frac{\pi_{k}}{\pi_{K}}}}+\log{\pi_{K}}\\
    \\
    \therefore p(\mathbf{x})
    &=\exp{\left[\sum_{k=1}^{K-1}{x_{k}\cdot\log{\frac{\pi_{k}}{\pi_{K}}}}+\log{\pi_{K}}\right]}\\
    &=1\cdot\exp{\left[\sum_{k=1}^{K-1}{x_{k}\cdot\log{\frac{\pi_{k}}{\pi_{K}}}}-\log{\frac{1}{\pi_{K}}}\right]}
    \end{aligned}$$

    - $T(\mathbf{x})=x_{k}$
    - $\eta(\theta)=\log{(\pi_{k}/\pi_{K})}$
    - $A(\eta)=\log{(1/\pi_{K})}$
    - $h(\mathbf{x})=1$

## conjugate prior
-----

- categorical model:

    $$
    X\mid\Pi\sim\mathrm{Categorical}(\Pi)
    $$

- canonical form:

    $$
    p(x\mid\Pi)
    =1\cdot\exp{\left[\sum_{k=1}^{K-1}{x_{k}\log{\frac{\pi_{k}}{\pi_{K}}}}-\log{\frac{1}{\pi_{K}}}\right]}
    $$

    - $T(x)=x_{k}$
    - $\eta(\theta)=\log{(\pi_{k}/\pi_{K})}$
    - $A(\eta)=\log{(1/\pi_{k})}$
    - $h(x)=1$

- prior of $\eta$:

    $$\begin{aligned}
    p(\eta)
    &\propto\exp{\left[\alpha\cdot\eta(\theta)-\beta\cdot A(\eta)\right]}\\
    &=\exp{\left[\alpha\cdot\sum_{k=1}^{K-1}{\eta_{k}}-\beta\cdot \log{\left(1+\sum_{k=1}^{K-1}{\exp{\eta_{k}}}\right)}\right]}
    \end{aligned}$$

- change of variables $\eta\to\pi$:

    $$\begin{aligned}
    p_{\Pi}(\Pi)\mathrm{\partial}\Pi
    &=p_{\mathrm{H}}(\mathrm{H})\mathrm{\partial}\mathrm{H}\\
    \therefore p_{\Pi}(\Pi)
    &=p_{\mathrm{H}}\left(\sum_{k=1}^{K-1}{\log{\frac{\pi_{k}}{\pi_{K}}}}\right)\left\vert\frac{\mathrm{\partial}\mathrm{H}}{\mathrm{\partial}\Pi}\right\vert\\
    &\propto\exp{\left[\alpha\cdot\sum_{k=1}^{K-1}{\eta_{k}}-\beta\cdot \log{\left(1+\sum_{k=1}^{K-1}{\exp{\eta_{k}}}\right)}\right]}\cdot\left\vert\frac{\mathrm{\partial}\mathrm{H}}{\mathrm{\partial}\Pi}\right\vert\\
    &=\exp{\left[\alpha\cdot\sum_{k=1}^{K-1}{\log{\pi_{k}}}-\alpha(K-1)\log{\pi_{K}}+\beta\log{\pi_{K}}\right]}\cdot\frac{1}{\prod_{k=1}^{K}{\pi_{k}}}\\
    &=\exp{\left[\alpha\cdot\sum_{k=1}^{K-1}{\log{\pi_{k}}}\right]}\exp{\left[\beta\log{\pi_{K}}-\alpha(K-1)\log{\pi_{K}}\right]}\cdot\frac{1}{\prod_{k=1}^{K}{\pi_{k}}}\\
    &=\left(\prod_{k=1}^{K-1}{\pi_{k}^{\alpha}}\right)\cdot\pi_{K}^{\beta-\alpha(K-1)}\cdot\frac{1}{\prod_{k=1}^{K}{\pi_{k}}}\\
    &=\left(\prod_{k=1}^{K-1}{\pi_{k}^{\alpha-1}}\right)\cdot\pi_{K}^{\beta-\alpha(K-1)-1}\\
    &=\prod_{k=1}^{K}{\pi_{k}^{\alpha_{k}-1}}
    \quad\mathrm{for}\quad\alpha_{k}
    =\begin{cases}
    \alpha,\quad &k\ne K\\
    \beta-\alpha(K-1),\quad &k=K\\
    \end{cases}\\
    &\approx\mathrm{Dirichlet}(\mathbf{a})
    \end{aligned}$$

- Therefore, the realization probability of the Categorical distribution $\Pi$ follows a Dirichlet distribution.

    $$
    \Pi\sim\mathrm{Dirichlet}(\mathbf{a})
    $$

## Multinomial
-----

- **다항 분포(Multinomial Distribution)**: 카테고리 분포의 시행 횟수를 일반화한 분포로서, $K$ 개 범주 중 하나가 실현되는 시행을 $n$ 번 반복했을 때, 각 범주가 실현될 조합을 나타내는 분포

    $$\begin{gathered}
    X:=\sum_{i=1}^{n}{Z_{i}}\quad\mathrm{for}\quad Z_{i}\overset{\mathrm{i.i.d}}{\sim}\mathrm{Categorical}(\Pi)\\
    \Downarrow\\
    X\sim\mathrm{Multinomial}(n,\Pi)
    \end{gathered}$$

- probability mass function:

    $$
    p(X=\mathbf{x}\mid\Pi)
    =\frac{n!}{x_{1}!\cdots x_{K}!}\prod_{k=1}^{K}{\pi_{k}^{x_{k}}}
    \quad\mathrm{for}\quad
    \begin{cases}\mathbf{x}=\begin{pmatrix}x_{1}&\cdots&x_{K}\end{pmatrix}^{T}\\
    \sum_{k=1}^{K}{x_{k}}=n
    \end{cases}
    $$

- moment generating function:

    $$\begin{aligned}
    M_{X}(\mathbf{t})
    &=\mathbb{E}_{p(\mathbf{x})}\left[\exp{\mathbf{t}^{T}X}\right]\\
    &=\mathbb{E}_{p(\mathbf{z})}\left[\exp{\left(\mathbf{t}^{T}\sum_{i=1}^{n}{Z_{i}}\right)}\right]\\
    &=\mathbb{E}_{p(\mathbf{z})}\left[\exp{\left(\sum_{i=1}^{n}{\mathbf{t}^{T}Z_{i}}\right)}\right]\\
    &=\mathbb{E}_{p(\mathbf{z})}\left[\prod_{i=1}^{n}{\exp{\mathbf{t}^{T}Z_{i}}}\right]\\
    &=\prod_{i=1}^{n}{\mathbb{E}_{p(\mathbf{z})}\left[\exp{\mathbf{t}^{T}Z_{i}}\right]}\quad(\because Z_{i}\perp Z_{j})\\
    &=\left(\mathbb{E}_{p(\mathbf{z})}\left[\exp{\mathbf{t}^{T}Z}\right]\right)^{n}\\
    &=\left(\sum_{k=1}^{K}{\exp{t_{k}}\cdot\pi_{k}}\right)^{n}
    \end{aligned}$$

    - $\mathbb{E}\left[X\right]=\nabla_{t}M_{X}(t)\vert_{t=0}=n\cdot\Pi$
    - $\mathbb{E}\left[XX^{T}\right]=\nabla_{t}^{2}M_{X}(t)\vert_{t=0}=n\cdot\mathrm{diag}(\Pi)$
    - $\mathrm{Cov}\left[X,X^{\prime}\right]=\mathbb{E}\left[XX^{T}\right]-\mathbb{E}\left[X\right]\mathbb{E}\left[X\right]^{T}=n\left(\mathrm{diag}(\Pi)-\Pi\Pi^{T}\right)$

- canonical form:

    $$\begin{aligned}
    p(\mathbf{x})
    &=\frac{n!}{x_{1}!\cdots x_{K}!}\prod_{k=1}^{K}{\pi_{k}^{x_{k}}}\\
    &=\frac{n!}{x_{1}!\cdots x_{K}!}\exp{\left[\sum_{k=1}^{K}{x_{k}\log{\pi_{k}}}\right]}\\
    &=\frac{n!}{x_{1}!\cdots x_{K}!}\cdot\exp{\left[\sum_{k=1}^{K-1}{x_{k}\cdot\log{\frac{\pi_{k}}{\pi_{K}}}}-n\cdot\log{\frac{1}{\pi_{K}}}\right]}
    \end{aligned}$$

    - $T(\mathbf{x})=x_{k}$
    - $\eta(\theta)=\log{(\pi_{k}/\pi_{K})}$
    - $A(\eta)=n\cdot\log{(1/\pi_{K})}$
    - $h(\mathbf{x})=n!/x_{1}!\cdots x_{K}!$
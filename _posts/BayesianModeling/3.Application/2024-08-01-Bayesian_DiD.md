---
order: 2
title: Bayesian DiD
date: 2024-08-01
categories: [BAYES, 3.bayes applications]
tags: [Bayesian, Design of Experiments, DiD]
math: true
image:
    path: /_post_refer_img/BayesianModeling/3.Application/Thumbnail.jpg
---

## DiD

- **이중차분법(`D`ifference-`i`n-`D`ifferences; DiD)**: 평행 추세 가정 하에 정책 시행에 따른 인과적 효과를 반사실과의 추세 차이로써 추정하는 준실험설계법(Quasi-Experimental)

- **평행 추세 가정(Parallel Trends Assumption)**: 관측 불가능한 반사실(counterfactual), 즉 실험군이 실제로 정책이 적용되지 않은 상태를 대리하는 논리적 장치로서, 정책이 없었더라면 실험군의 추세는 통제군과 동일했을 것이라는 가정

    $$\begin{aligned}
    \underbrace{\mathbb{E}\left[Y_{i,t}(0)-Y_{i,s}(0) \mid D_{i}=1\right]}_{\text{experimental group}}
    &\approx \underbrace{\mathbb{E}\left[Y_{i,t}(0)-Y_{i,s}(0) \mid D_{i}=0\right]}_{\text{control group}}\\
    \underbrace{\mathbb{E}\left[Y_{i,t}(0) \mid D_{i}=1\right]}_{\text{counterfactual}} - \underbrace{\mathbb{E}\left[Y_{i,s}(0) \mid D_{i}=1\right]}_{\text{factual}}
    &\approx \underbrace{\mathbb{E}\left[Y_{i,t}(0) \mid D_{i}=0\right] - \mathbb{E}\left[Y_{i,s}(0) \mid D_{i}=0\right]}_{\text{control group}}\\
    \therefore \underbrace{\mathbb{E}\left[Y_{i,t}(0) \mid D_{i}=1\right]}_{\text{counterfactual}}
    &\approx \underbrace{\mathbb{E}\left[Y_{i,s}(0) \mid D_{i}=1\right]}_{\text{factual}}\\
    &\quad + \underbrace{\mathbb{E}\left[Y_{i,t}(0) \mid D_{i}=0\right] - \mathbb{E}\left[Y_{i,s}(0) \mid D_{i}=0\right]}_{\text{control group}}
    \end{aligned}$$

- **정책의 인과적 효과(`A`verage `T`reatment effect on the `T`reated; ATT)**: 정책 시행에 따른 실제 결과와 정책 미시행에 따른 반사실적 결과 간 차이

    $$\begin{aligned}
    \delta
    &=\mathbb{E}\left[Y_{i,t}(1)-Y_{i,t}(0) \mid D_{i}=1\right]\\
    &=\underbrace{\mathbb{E}\left[Y_{i,t}(1)\mid D_{i}=1\right]}_{\text{factual}} - \underbrace{\mathbb{E}\left[Y_{i,t}(0)\mid D_{i}=1\right]}_{\text{counterfactual}}\\
    &\approx \underbrace{\mathbb{E}\left[Y_{i,t}(1)\mid D_{i}=1\right] - \mathbb{E}\left[Y_{i,s}(0) \mid D_{i}=1\right]}_{\text{experimental group}}\\
    &\quad+ \underbrace{\mathbb{E}\left[Y_{i,t}(0) \mid D_{i}=0\right] - \mathbb{E}\left[Y_{i,s}(0) \mid D_{i}=0\right]}_{\text{control group}}
    \end{aligned}$$



## Model

- 2시점 2단위 모형

    $$\begin{aligned}
    Y_{i,t}(D_{i} \times T_{t})
    &=\alpha + \beta D_{i} + \gamma T_{t} + \delta(D_{i} \times T_{t}) + \epsilon_{i,t}
    \end{aligned}$$

    - $t \in \{0,1\}$: 2시점(정책 시행 전과 후)
    - $i \in \{0,1\}$: 2단위(실험군과 통제군)
    - $Y_{i,t}$: 단위 $i$ 의 시점 $t$ 에서 결과
    - $\alpha$: 통제군의 사전 평균
    - $\beta$: 실험군과 통제군 간 고정 수준 차이
    - $D_{i} \in \{0,1\}$: 단위 $i$ 의 처리군 여부
    - $\gamma$: 사전-사후 공통 추세 변화
    - $T_{t} \in \{0,1\}$: 시점 $t$ 의 사후 여부
    - $\delta$: 정책의 인과적 효과(ATT)

- 다시점 다단위 모형(processing time per unit is the same)

    $$\begin{aligned}
    Y_{i,t}(D_{i} \times T_{t})
    &=\alpha_{i} + \gamma_{t} + \delta_{i}(D_{i} \times T_{t}) + \epsilon_{i,t}
    \end{aligned}$$

    - $t=1,2,\cdots,K$: 다시점
    - $i=1,2,\cdots,N$: 다단위
    - $Y_{i,t}$: 단위 $i$ 의 시점 $t$ 에서 결과
    - $\alpha_{i}$: 단위 $i$ 의 고정 효과
    - $\gamma_{t}$: 시점 $t$ 의 고정 효과
    - $D_{i} \in \{0,1\}$: 단위 $i$ 의 처리군 여부
    - $T_{t} \in \{0,1\}$: 시점 $t$ 의 사후 여부
    - $\delta_{i}$: 단위 $i$ 에 대하여 정책의 인과적 효과(ATT)

## Bayesian Method

### flat bayesian

- frequentist ols:

    $$
    Y_{i,t}
    =\alpha_{i}+\gamma_{t}+\delta_{i}(D_{i} \times T_{t})+\epsilon_{i,t}
    $$

- bayesian likelihood:

    $$\begin{aligned}
    Y_{i,t} \mid \alpha_{i},\gamma_{t},\delta_{i},\sigma
    &\sim \mathcal{N}(\mu_{i,t},\sigma^{2})\\
    \mu_{i,t}
    &= \alpha_{i} + \gamma_{t} + \delta_{i}(D_{i} \times T_{t})
    \end{aligned}$$

- prior of parameters:

    $$\begin{aligned}
    \alpha_{i} &\overset{\mathrm{i.i.d}}{\sim} \mathcal{N}(0,10^{2}) \quad i=1,\cdots,N\\
    \gamma_{t} &\overset{\mathrm{i.i.d}}{\sim} \mathcal{N}(0,10^{2}) \quad t=1,\cdots,T\\
    \delta_{i} &\overset{\mathrm{i.i.d}}{\sim} \mathcal{N}(0,10^{2}) \quad i=1,\cdots,N\\
    \sigma &\sim \mathrm{Half-cauchy}(2)
    \end{aligned}$$

- posterior estimation:

    $$\begin{aligned}
    \underbrace{p(\alpha_{i},\gamma_{t},\delta_{i},\sigma \mid Y_{i,t})}_{\text{posterior}} 
    &\propto \underbrace{p(Y_{i,t} \mid \alpha_{i},\gamma_{t},\delta_{i},\sigma)}_{\text{likelihood}}\\
    &\quad\times\underbrace{p(\alpha_{i})p(\gamma_{t})p(\delta_{i})p(\sigma)}_{\text{prior}} \quad \mathrm{s.t.} \quad \alpha_{i}\perp\gamma_{t}\perp\delta_{i}\perp\sigma
    \end{aligned}$$

- `refer.` cauchy distribution

  - $X \sim \mathrm{Cauchy}(x_{0},\gamma)$:

    $$
    f(x) = \frac{1}{\pi \gamma \left[1 + \left(\frac{x - x_{0}}{\gamma}\right)^{2} \right]}
    $$

  - $X \sim \mathrm{Half-Cauchy}(\gamma)$: absolute value distribution of cauchy

    $$
    f(x) = \frac{2}{\pi \gamma \left[1 + \left(x/\gamma\right)^{2} \right]}, \quad x>0
    $$

### hierarchical bayesian

- level 1:

    $$
    Y_{i,t} \mid \alpha_{i},\gamma_{t},\delta_{i},\sigma \sim \mathcal{N}(\mu_{i,t},\sigma^{2})
    $$

- level 2:

    $$\begin{aligned}
    \alpha_{i} \mid \mu_{\alpha},\tau_{\alpha} &\sim \mathcal{N}(\mu_{\alpha},\tau_{\alpha}^{2}) \quad i=1,\cdots,N\\
    \gamma_{t} \mid \mu_{\gamma},\tau_{\gamma} &\sim \mathcal{N}(\mu_{\gamma},\tau_{\gamma}^{2}) \quad t=1,\cdots,T\\
    \delta_{i} \mid \mu_{\delta},\tau_{\delta} &\sim \mathcal{N}(\mu_{\delta},\tau_{\delta}^{2}) \quad i=1,\cdots,N
    \end{aligned}$$

- level 3:

    $$\begin{aligned}
    \mu_{\alpha} &\sim \mathcal{N}(0,10^{2}), \quad \tau_{\alpha} \sim \mathrm{Half-cauchy}(2)\\
    \mu_{\gamma} &\sim \mathcal{N}(0,10^{2}), \quad \tau_{\gamma} \sim \mathrm{Half-cauchy}(2)\\
    \mu_{\delta} &\sim \mathcal{N}(0,10^{2}), \quad \tau_{\delta} \sim \mathrm{Half-cauchy}(2)
    \end{aligned}$$

- posterior estimation:

    $$\begin{aligned}
    \underbrace{p(\alpha_{i},\gamma_{t},\delta_{i},\sigma \mid Y_{i,t})}_{\text{posterior}} 
    &\propto \underbrace{p(Y_{i,t} \mid \alpha_{i},\gamma_{t},\delta_{i},\sigma)}_{\text{likelihood}}\\
    &\quad\times \underbrace{p(\alpha_{i} \mid \mu_{\alpha},\tau_{\alpha})p(\mu_{\alpha})p(\tau_{\alpha})}_{\propto p(\mu_{\alpha},\tau_{\alpha} \mid \alpha_{i})} \quad &\mathrm{s.t.} \quad \mu_{\alpha} \perp \tau_{\alpha}\\
    &\quad\times \underbrace{p(\gamma_{t} \mid \mu_{\gamma},\tau_{\gamma})p(\mu_{\gamma})p(\tau_{\gamma})}_{\propto p(\mu_{\gamma},\tau_{\gamma} \mid \gamma_{t})} \quad &\mathrm{s.t.} \quad \mu_{\gamma} \perp \tau_{\gamma}\\
    &\quad\times \underbrace{p(\delta_{i} \mid \mu_{\delta},\tau_{\delta})p(\mu_{\delta})p(\tau_{\delta})}_{\propto p(\mu_{\delta},\tau_{\delta} \mid \delta_{i})} \quad &\mathrm{s.t.} \quad \mu_{\delta} \perp \tau_{\delta}\\
    &\quad\times p(\sigma)
    \end{aligned}$$

### uncertainty in treatment assignment

- policy exposure uncertainty:

    $$\begin{aligned}
    D_{i} \mid \pi_{i} &\sim \mathrm{Bernoulli}(\pi_{i})\\
    \pi_{i} &\overset{\mathrm{i.i.d}}{\sim} \mathrm{Beta}(1,1)
    \end{aligned}$$

- parallel trends assumption:

    $$\begin{gathered}
    \mathbb{E}\left[Y_{i,t}(0)-Y_{i,s}(0) \mid \pi_{i}\right]
    = \mathbb{E}\left[Y_{i,t}(0)-Y_{i,s}(0)\right]\\
    \Updownarrow\\
    (Y_{i,t}(0)-Y_{i,s}(0))
    \perp D_{i} \mid \pi_{i}
    \end{gathered}$$

- posterior estimation:

    $$\begin{aligned}
    &p(\alpha_{i},\gamma_{t},\delta_{i},\sigma,\pi_{i} \mid Y_{i,t}, D_{i})\\
    &\propto \underbrace{p(Y_{i,t} \mid \alpha_{i},\gamma_{t},\delta_{i},\sigma) \cdot p(\alpha_{i})p(\gamma_{t})p(\delta_{i})p(\sigma)}_{\propto p(\alpha_{i},\gamma_{t},\delta_{i},\sigma \mid Y_{i,t})}\\
    &\quad\times \underbrace{p(D_{i}\mid\pi_{i})\cdot p(\pi_{i})}_{\propto p(\pi_{i}\mid D_{i})}
    \end{aligned}$$

- In frequentist inference, the expected causal effect is defined as follows:

    $$
    \mathbb{E}\left[\delta_{i}(D_{i} \times T_{t})\right]
    =\begin{cases}
    \delta_{i}T_{t} \quad &\mathrm{if}\quad D_{i}=1 \\
    0 \quad &\mathrm{otherwise}
    \end{cases}
    $$

- In Bayesian inference, the expected causal effect is given by:

    $$
    \mathbb{E}\left[\delta_{i}(D_{i} \times T_{t})\right]
    =\pi_{i}\delta_{i}T_{t}
    $$
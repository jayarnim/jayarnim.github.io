---
order: 2
title: Bayesian Attention Modules
date: 2024-09-05
categories: [Research Interest, Bayesian Deep Learning]
tags: [Deep Learning, Bayesian, Attention Mechanism]
math: true
description: >-
    <ul type="square">
    <li><strong>Title</strong>: <a href="https://arxiv.org/abs/2010.10604"><code>Bayesian Attention Modules</code></a></li>
    <li><strong>Publisher</strong>: <em>NeurlPS</em></li>
    <li><strong>Published</strong>: <em>2020</em></li>
    </ul>
image:
    path: /_post_refer_img/BayesianDeepLearning/Thumbnail.jpg
---

## Pilot Study; Attention Mechanism
-----

- **Attention Mechanism** : 주어진 입력에서 중요한 부분에 선택적으로 집중하기 위하여, 중요도에 따라 정보에 더 많은 확률적 가중치를 할당하는 방법론

- **Composition**

    | 항목 | 예시 | 구성 요소 | 
    |---|---|---|
    | 목표 | 사용자가 무엇에서 진정으로 "재미"를 느끼는가? | |
    | 질문 | 사용자가 정의하는 재미있는 소설 | 사용자의 선호 |
    | 키 | 소설의 메타 정보 | 장르, 작가, 출판사 등 |
    | 값 | 소설의 내용 정보 | 줄거리, 내용 전개 방식, 주제 의식 등 |

    - **질문(Query; $$\mathbf{Q}_{M \times d_{K}}$$)** : 특정 정보나 입력에 대해 집중하고자 하는 요소
    - **키(Key; $$\mathbf{K}_{N \times d_{K}}$$)** : 질문에 대하여 대응되는 입력 정보의 각 요소
    - **값(Value; $$\mathbf{V}_{M \times D}$$)** : 입력 정보

- **How to Modeling**

    $$\begin{aligned}
    \text{Attention}\left(\mathbf{Q}, \mathbf{K}, \mathbf{V}\right)
    &= \underbrace{\text{softmax}\overbrace{\left(\frac{\mathbf{Q} \cdot \mathbf{K}}{\sqrt{d_{K}}}\right)}^{\text{Attention Score}}}_{\text{Attention Weight}} \cdot \mathbf{V}\\
    &= \mathbf{X}
    \end{aligned}$$

    - **Attention Score** : $$\mathbf{q}_{i}, \mathbf{k}_{j}$$ 간 유사도를 통해 도출한 질문별 키에 대한 집중 점수

        $$
        \alpha_{(i,j)} \in \mathcal{A}_{M \times N} = \frac{\mathbf{Q} \cdot \mathbf{K}}{\sqrt{d_{K}}}
        $$

    - **Attention Weight** : 질문별 키에 대한 집중 점수의 확률화

        $$
        \omega_{(i,j)} \in \mathcal{W}_{M \times N}=\text{softmax}\left(\mathcal{A}\right)
        $$

    - $$\mathbf{X}_{M \times D}$$ : 질문 $j=1,2,\cdots,M$ 별 선택적으로 가중된 값의 정보 $d=1,2,\cdots,D$ 집합

        $$
        \mathbf{X}_{M \times D}=\mathcal{W}_{M \times N} \cdot \mathbf{V}_{N \times D}
        $$

## Bayesian Attention Modules
-----

- **Bayesian Attention Modules** : Attention Mechanism 에 실증적 베이지안 접근법을 적용하여 Attention Weight 의 불확실성을 반영하되, Probabilic Attention Mechanism 선행연구의 한계점을 보완하는 근사 분포를 적용하는 방법론

- **Probabilic Attention Mechanism 선행 연구의 한계점**
    - **Hard Attention** : 사후 분포의 근사 분포를 이산 확률 분포로 설정하는데, 이는 재매개변수화가 불가능하여 역전파 알고리즘을 통한 최적화 효율성을 도모할 수 없음
    - **Soft Attention** : 사후 분포의 근사 분포를 디리클레 분포, 정규 분포 등으로 설정하는데, 디리클레 분포는 마찬가지로 재매개변수가 불가능하고, 정규 분포는 확률변수의 범위를 양수로 제한하지 않아 샘플링된 Attention Weight 를 확률적으로 해석할 수 없음

- **Bayesian Attention Modules 의 해법** : 재매개변수화 가능하고 확률변수의 범위를 양수로 제한하는 확률 분포를 근사 분포로 설정함으로써 샘플링된 Attention Weight 의 역전파 학습 및 확률적 해석을 도모함

    - **와이블 분포(Weibull Distribution)** : 특정 사건이 발생하기까지의 대기 시간에 관한 확률 분포

        $$\begin{aligned}
        \mathcal{A} \sim \text{Weibull}\left(k, \lambda\right) \quad \text{for} \quad \mathcal{A} > 0
        \end{aligned}$$

        - **Shape Parameter($k$)** : 사건 발생 대기 시간에 따른 사건 발생 가능성의 증가 혹은 감소 패턴
        - **Scale Parameter($\lambda$)** : 사건 발생 대기 시간의 범위

    - **로그 정규 분포(Log Normal Distribution)** : 로그 값이 정규 분포를 따르는 확률변수에 관한 분포

        $$\begin{aligned}
        \mathcal{A} \sim \text{Log-Normal}\left(\mu, \sigma^{2}\right) \quad \text{for} \quad \mathcal{A} > 0
        \end{aligned}$$

        - **Shape Parameter($\mu$)**
        - **Scale Parameter($\sigma^{2}$)**

## Bayesian Framework
-----

- **Empirical Prior Dist. for Attention Score**

    $$\begin{aligned}
    \mathcal{A}
    &\sim \pi\left(\Theta, \eta\right)
    \end{aligned}$$

    - $\Theta$ : Shape Parameter is Trained by $\mathbf{K}$

        $$\begin{aligned}
        \overrightarrow{\Theta}_{N \times 1} \mid \mathbf{K}_{N \times d_{K}}
        &= \text{Softmax}\left[\mathcal{F}^{(2)}\left(\text{ReLU}\left[\mathcal{F}^{(1)}\left(\mathbf{K}_{N \times d_{K}}\right)\right]\right)\right]
        \end{aligned}$$

        - 선택지 $$\overrightarrow{\mathbf{v}}_{j} \in \mathbf{V}_{N \times D}$$ 의 중요성을 질문 $$\overrightarrow{\mathbf{q}}_{i} \in \mathbf{Q}_{M \times d_{K}}$$ 마다 맞춤으로 갱신하기 전, 질문과 비교 가능한, 선택지에 대한 정보 $$\overrightarrow{\mathbf{k}}_{j} \in \mathbf{K}_{N \times d_{K}}$$ 만을 활용하여 선택지의 전반적인 중요성을 사전 평가함

    - $\eta$ : Scale Parameter is Global Hyper Parameter

- **Liklehood**

    $$
    \mathcal{L}\left(\mathbf{Y} \mid \mathcal{A}, \mathbf{Q},\cdots\right)
    $$

- **Posterior Dist. Estimation**

    $$\begin{aligned}
    p\left(\mathcal{A} \mid \mathbf{Y}, \mathbf{Q}, \cdots\right)
    \propto \mathcal{L}\left(\mathbf{Y} \mid \mathcal{A}, \mathbf{Q}, \cdots\right) \cdot \pi\left(\mathcal{A} ; \Theta, \eta \right)
    \end{aligned}$$

## Approx. Dist. Determination
-----

- **Approx. Dist. of $\mathcal{A} \mid \mathbf{Y}, \mathbf{Q}, \cdots \sim P$**

    $$
    \mathcal{A} \sim \mathcal{Q}\left(\Phi\right)
    $$

### Weibull Dist.

- If Approx. Dist. $\mathcal{A} \sim \mathcal{Q}\left(\Phi\right)$ is set to $\text{Weibull}\left(k,\lambda\right)$

    $$\begin{aligned}
    \mathcal{Q}\left(\Phi\right) = \text{Weibull}\left(k, \lambda\right)
    \end{aligned}$$

- Reparameterization Trick

    $$\begin{aligned}
    \mathcal{A}
    &= \mathcal{G}(\epsilon ; k, \lambda)\\
    &= \lambda\left(\log{\frac{1}{1-\epsilon}}\right)^{1/k}, \quad \epsilon \sim \text{Uniform}\left(0,1\right)
    \end{aligned}$$

- Prior Dist. $\mathcal{A} \sim \pi\left(\Theta,\eta\right)$ is set to $\text{Gamma}\left(\alpha, \beta\right)$ because of Semi-interpretive Expression

    $$\begin{aligned}
    &D_{KL}\Big[\text{Weibull}\left(k,\lambda\right) \parallel \text{Gamma}\left(\alpha,\beta\right)\Big]\\
    &= \gamma \cdot \alpha \cdot \frac{1}{k} - \alpha \cdot \log{\lambda} + \log{k} + \beta \cdot \lambda \cdot \Gamma\left(1 + \frac{1}{k}\right) - \gamma - 1 - \alpha \cdot \log{\beta} + \log{\Gamma\left(\alpha\right)}
    \end{aligned}$$

    - $\gamma$ : Euler–Mascheroni constant

### Log-Normal Dist.

- If Approx. Dist. $\mathcal{A} \sim \mathcal{Q}\left(\Phi\right)$ is set to $\text{Log-Normal}\left(\mu, \sigma^{2}\right)$

    $$\begin{aligned}
    \mathcal{Q}\left(\Phi\right) = \text{Log-Normal}\left(\mu, \sigma^{2}\right)
    \end{aligned}$$

- Reparameterization Trick

    $$\begin{aligned}
    \mathcal{A}
    &= \mathcal{G}(\mathcal{Z} ; \mu, \sigma)\\
    &= \exp{\Big[\mu + \sigma \cdot \mathcal{Z} \Big]}, \quad \mathcal{Z} \sim \mathcal{N}\left(0,1\right)
    \end{aligned}$$

- Prior Dist. $\mathcal{A} \sim \pi\left(\Theta,\eta\right)$ is set to $\text{Log-Normal}\left(\mu,\sigma^{2}\right)$ because of Semi-interpretive Expression

    $$\begin{aligned}
    &D_{KL}\Big[\text{Log-Normal}\left(\mu_{\text{Approx}},\sigma^{2}_{\text{Approx}}\right) \parallel \text{Log-Normal}\left(\mu_{\text{Prior}},\sigma^{2}_{\text{Prior}}\right)\Big]\\
    &= \frac{\sigma_{\text{Approx}}}{\sigma_{\text{Prior}}} + \frac{\left(\mu_{\text{Approx}} - \mu_{\text{Prior}}\right)^{2}}{2 \cdot \sigma^{2}_{\text{Prior}}} - \frac{1}{2} + \log{\frac{\sigma_{\text{Prior}}}{\sigma_{\text{Approx}}}}
    \end{aligned}$$

## Variational Inference
-----

- ELBO

    $$\begin{aligned}
    \text{ELBO}
    &= \mathbb{E}_{\mathcal{A} \sim \mathcal{Q}\left(\Phi\right)}\Big[\log{\mathcal{L}\left(\mathbf{Y} \mid \mathcal{A}, \mathbf{Q}, \cdots\right)}\Big]
    - D_{KL}\Big[q\left(\mathcal{A};\Phi\right) \parallel \pi\left(\mathcal{A};\Theta,\eta\right)\Big]
    \end{aligned}$$

- Optimization

    $$
    \mathcal{A},\Theta,\Phi \mid \eta,\cdots
    = \text{arg}\min{-\text{ELBO}}
    $$
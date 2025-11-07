---
order: 4
title: Fourier Analysis (2) Fourier Transform
date: 2025-02-06
categories: [MATHEMATICAL TECHS, 3.etc]
tags: [Mathematics]
math: true
image:
    path: /_post_refer_img/MathematicalTechs/3.etc/Thumbnail.jpg
---

## Fourier Transform
-----

- **푸리에 변환(Fourier Transform)**: 푸리에 급수를 활용하여 시간 영역 $t \in T$ 에서 정의된 비주기 신호 함수 $X(t)$ 를 주파수 영역 $\omega \in \Omega$ 의 스펙트럼 밀도 함수 $\mathcal{X}(\omega)$ 로 재정의하는 기법

- **정변환(transform)**: 시간 영역의 비주기 신호를 주파수 영역의 스펙트럼 밀도로 변환

    $$\begin{aligned}
    \mathcal{F}(X)
    &= \mathcal{X}(\omega)\\
    &= \left<X(u),\phi_{\omega}(u)\right>\\
    &= \int_{-\infty}^{\infty}{X(u)\phi_{\omega}^{*}(u)\mathrm{d}u}
    \end{aligned}$$

- **역변환(inverse transform)**: 주파수 영역의 스펙트럼 밀도를 시간 영역의 비주기 신호로 복원

    $$\begin{aligned}
    \mathcal{F}^{-1}(X)
    &= X(u)\\
    &= \frac{1}{2\pi}\left<\mathcal{X}(\omega),\phi_{u}^{*}(\omega)\right>\\
    &= \frac{1}{2\pi}\int_{-\infty}^{\infty}{\mathcal{X}(\omega)\phi_{u}(\omega)\mathrm{d}\omega}
    \end{aligned}$$

## Discrete Frequency Lines
-----

- 푸리에 해석과 비주기 신호 $X(t)$ 를 매개하기 위한 함수 정의:

    $$\begin{aligned}
    S_{T}(t)
    &= \sum_{n \in \mathbb{Z}}{X(t-nT)}
    \end{aligned}$$

- $S_{T}(t)$ 는 주기 $T$ 인 주기 함수임:

    $$\begin{aligned}
    S_{T}(t+T)
    &= \sum_{n \in \mathbb{Z}}{X((t+T)-nT)}\\
    &= \sum_{n \in \mathbb{Z}}{X(t-(n-1)T)}\\
    &= \sum_{m \in \mathbb{Z}}{X(t-mT)}\\
    &= S_{T}(t)
    \end{aligned}$$

- $S_{T}(t)$ 의 푸리에 계수:

    $$\begin{aligned}
    a_{k}
    &= \frac{1}{T}\int_{0}^{T}{S_{T}(t)\phi_{\omega_{k}}^{*}(t)\mathrm{d}t}\\
    &= \frac{1}{T}\int_{0}^{T}{\sum_{n \in \mathbb{Z}}{X(t-nT)}\phi_{\omega_{k}}^{*}(t)\mathrm{d}t}\\
    &= \frac{1}{T}\sum_{n \in \mathbb{Z}}{\int_{0}^{T}{X(t-nT)\phi_{\omega_{k}}^{*}(t)\mathrm{d}t}}
    \end{aligned}$$

- $u=t-nT$:

    $$\begin{aligned}
    \int_{0}^{T}{X(t-nT)\phi_{\omega_{k}}^{*}(t)\mathrm{d}t}
    &= \int_{-nT}^{(1-n)T}{X(u)\phi_{\omega_{k}}^{*}(u+nT)\mathrm{d}u}\\
    &= \int_{-nT}^{(1-n)T}{X(u)\phi_{\omega_{k}}^{*}(u)\mathrm{d}u}\\
    \\
    \because \phi_{\omega_{k}}^{*}(u+nT)
    &= \exp{\left[-i\omega_{k}(u+nT)\right]}\\
    &= \exp{\left[-i\omega_{k}u\right]} \cdot \underbrace{\exp{\left[-i\omega_{k}nT\right]}}_{=1} \quad (\because k\omega_{0}T=2 \pi k)\\
    &= \phi_{\omega_{k}}^{*}(u)
    \end{aligned}$$

- 범위 조정:

    $$\begin{aligned}
    \bigcup_{n \in \mathbb{Z}}{[-nT,(1-n)T)}
    &= \mathbb{R}
    \end{aligned}$$

- 따라서:

    $$\begin{aligned}
    a_{k}
    &= \frac{1}{T}\sum_{n \in \mathbb{Z}}{\int_{-nT}^{(1-n)T}{X(u)\phi_{\omega_{k}}^{*}(u)\mathrm{d}u}}\\
    &= \frac{1}{T}\int_{-\infty}^{\infty}{X(u)\phi_{\omega_{k}}^{*}(u)\mathrm{d}u}\\
    &= \frac{1}{T}\left<X(u),\phi_{\omega_{k}}(u)\right>
    \end{aligned}$$

## Transform
-----

- 주기가 $T$ 인 신호에서 $k$ 번째 주파수의 평균 기여도를 구간 폭 $\Delta\omega=2\pi/T$ 에 해당하는 총 기여도로 재정의하자:

    $$\begin{aligned}
    \mathcal{X}_{T}(\omega_{k})
    := T \cdot a_{k}
    \end{aligned}$$

- 비주기 신호는 주기 $T \to \infty$ 인 주기 신호로 볼 수 있으며, 이는 이산 주파수 $\cdots,-2 \cdot \omega_{0}, -1 \cdot \omega_{0}, 0 \cdot \omega_{0}, 1 \cdot \omega_{0}, 2 \cdot \omega_{0}, \cdots$ 를 연속 주파수 $\omega \in \mathbb{R}$ 로 일반화한 형태로 볼 수 있음:

    $$\begin{gathered}
    T \to \infty \Leftrightarrow \Delta \omega \to 0
    \end{gathered}$$

- 이산 주파수 기저(Discrete Frequency Lines) $$\phi_{\omega_{k}}$$ 의 총 기여도 $$\mathcal{X}_{T}(\omega_{k})$$ 는 $$\Delta \omega \to 0$$ 에서 연속 주파수 기저(Continuous Frequency) $$\phi_{\omega}$$ 의 밀도(Density) $$\mathcal{X}(\omega)$$ 로 수렴함:

    $$\begin{aligned}
    \mathcal{X}(\omega)
    :=\lim_{\Delta \omega \to 0}{\mathcal{X}_{T}(\omega_{k})}
    = \left<X(u),\phi_{\omega}(u)\right>
    \end{aligned}$$

## Inverse Transform
-----

- 푸리에 급수:

    $$\begin{aligned}
    S_{T}(t)
    &= \sum_{k}{a_{k}\phi_{\omega_{k}}(t)}\\
    &= \frac{1}{T}\sum_{k}{\mathcal{X}_{T}(\omega_{k})\phi_{\omega_{k}}(t)}\\
    &= \frac{1}{T}\sum_{k}{\mathcal{X}_{T}(\omega_{k})\phi_{t}(\omega_{k})} \quad (\because \phi_{\omega_{k}}(t)=\phi_{t}(\omega_{k})=\exp{i\omega_{k}t})\\
    &= \frac{1}{2\pi}\sum_{k}{\mathcal{X}_{T}(\omega_{k})\phi_{t}(\omega_{k})\Delta \omega} \quad (\because \Delta \omega = \omega_{0} = \frac{2\pi}{T})
    \end{aligned}$$

- 주기 함수 $S_{T}(t)$ 는 비주기 신호 $X(t)$ 를 주기 $T$ 만큼 평행이동한 복제 신호 $X(t-nT)$ 의 합이고, 주기 $T \to \infty$ 라면 관찰 가능한 범위에서($t$ 가 유한한 범위일 때) $X(t-nT)$ 의 기여가 사라지므로 $X(t)$ 에 근사하게 됨:

    $$\begin{aligned}
    \lim_{T\to\infty}{S_{T}(t)}
    &= \cdots + X(t+ \infty) + X(t) + X(t-\infty) + \cdots\\
    &\approx X(t) \quad \mathrm{for} \quad X(t) \in L^{1}(\mathbb{R})
    \end{aligned}$$

    - $L^{1}(\mathbb{R})$: 르베그 적분 가능한 함수 공간

        > 함수 $f \in L^{1}(\mathbb{R})$ 는 실수 전체에서 절대값 적분이 유한해야 하므로 정의역의 절대값이 커질수록 함수 값이 평균적으로 작아저야 함. 즉, 정의역의 절대값이 무한히 커짐에도 함수 값이 일정한 크기를 유지하는 함수는 이 공간에 속할 수 없음.

        $$\begin{aligned}
        L^{1}(\mathbb{R})
        := \left\{f:\mathbb{R}\to\mathbb{C} \mid \int_{-\infty}^{\infty}{\vert f(t) \vert^{1} \mathrm{d}t} < \infty \right\}
        \end{aligned}$$

- 따라서:

    $$\begin{aligned}
    X(t)
    &\approx \lim_{\Delta \omega \to 0}{S_{T}(t)}\\
    &= \lim_{\Delta \omega \to 0}{\frac{1}{2\pi}\sum_{k}{\mathcal{X}_{T}(\omega_{k})\phi_{t}(\omega_{k})\Delta \omega}}\\
    &= \frac{1}{2\pi}\lim_{\Delta \omega \to 0}{\sum_{k}{\mathcal{X}_{T}(\omega_{k})\phi_{t}(\omega_{k})\Delta \omega}}\\
    &= \frac{1}{2\pi}\int_{-\infty}^{\infty}{\mathcal{X}(\omega)\phi_{t}(\omega)\mathrm{d}\omega}\\
    &= \frac{1}{2\pi}\left<\mathcal{X}(\omega),\phi_{t}(\omega)\right>
    \end{aligned}$$
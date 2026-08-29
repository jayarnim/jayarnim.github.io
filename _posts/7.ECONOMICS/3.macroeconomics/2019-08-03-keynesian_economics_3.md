---
order: 6
title: Keynesian Economics (3) IS-LM Model
date: 2019-08-03
categories: [7.ECONOMICS, 3.macroeconomics]
tags: [economics, macroeconomics, keynesian economics]
math: true
description: >-
    Based on the lecture "Macroeconomics (2017-1)" by Prof. Hyun Hak Kim, Dept. of Economics, College of Economics & Commerce, Kookmin Univ.
image:
    path: /assets/img/posts/7.ECONOMICS/3.macroeconomics/Thumbnail.jpg
---

## IS-LM 모형

![01](/assets/img/posts/7.ECONOMICS/3.macroeconomics/06-01.png){: width="100%"}

- **IS-LM 모형(`I`nvest-`S`aving-`L`iquidity-`M`onetary Model)**: 단기적으로 물가가 경직되어 있을 때, 실물 시장(Invest-Saving)의 균형과 화폐 시장(Liquidity-Monetary)의 균형이 동시에 이루어지는 국민소득과 실질이자율 조합을 분석하는 일반균형 모형

- 실물 시장 균형 (IS Curve):

    $$\begin{aligned}
    Y
    &=\overline{A}-\alpha r
    \end{aligned}$$

    - $\overline{A}$: 국민소득 혹은 실질이자율과 무관하게 고정적으로 지출되는 규모로서 **자율 지출(Autonomous Expenditure)**

        $$\begin{aligned}
        \overline{A}
        &\equiv\frac{C_{0}+I_{0}+G_{0}-MPC\cdot\overline{T}}{1-MPC}
        \end{aligned}$$

    - $\alpha$: 국민소득의 실질이자율탄력성

        $$\begin{aligned}
        \alpha
        &\equiv\frac{b}{1-MPC}
        \end{aligned}$$

- 화폐 시장 균형 (LM Curve):

    $$\begin{aligned}
    Y
    &=\frac{h}{k}r+\frac{1}{k}\cdot\frac{M}{\overline{P}}
    \end{aligned}$$

    - 단기적으로는 하방 경직성으로 인하여 물가가 고정되어 물가상승률이 $0$ 에 수렴하므로 피셔 방정식(Fisher Equation)에 근거하여 명목이자율을 실질이자율로 대체 가능함:

        $$
        i
        =r,
        \quad\because\pi^{e}=0
        \quad\text{where}\quad\mathrm{Short-Run}
        $$

- 실물 시장과 화폐 시장 간 균형점 도출:

    $$\begin{aligned}
    Y^{*}
    &=\frac{h}{h+\alpha k}\overline{A}+\frac{\alpha}{h+\alpha k}\cdot\frac{M}{\overline{P}}\\
    r^{*}
    &=\frac{k}{h+\alpha k}\overline{A}-\frac{1}{h+\alpha k}\cdot\frac{M}{\overline{P}}
    \end{aligned}$$

## 재정 정책의 유효성

![02](/assets/img/posts/7.ECONOMICS/3.macroeconomics/06-02.png){: width="100%"}

### 정부지출 확대 정책

- 정부지출 확대 정책 시행:

    $$
    G\to G+\Delta G
    \quad\Longleftrightarrow\quad
    \overline{A}\to\overline{A}+\frac{1}{1-MPC}\Delta G
    $$

- 균형실질이자율 상승:

    $$\begin{aligned}
    r^{\prime}
    &=\frac{k}{h+\alpha k}\overline{A}-\frac{1}{h+\alpha k}\cdot\frac{M}{\overline{P}}+\frac{k}{h+\alpha k}\cdot\frac{1}{1-MPC}\Delta G\\
    &=r^{*}+\frac{k}{h+\alpha k}\cdot\frac{1}{1-MPC}\Delta G\\
    \therefore\frac{\Delta r}{\Delta G}
    &=\frac{k}{h+\alpha k}\cdot\frac{1}{1-MPC} >0
    \end{aligned}$$

- 균형국민소득 증가:

    $$\begin{aligned}
    Y^{\prime}
    &=\frac{h}{h+\alpha k}\overline{A}+\frac{\alpha}{h+\alpha k}\cdot\frac{M}{\overline{P}}+\frac{h}{h+\alpha k}\cdot\frac{1}{1-MPC}\Delta G\\
    &=Y^{*}+\frac{h}{h+\alpha k}\cdot\frac{1}{1-MPC}\Delta G\\
    \therefore\frac{\Delta Y}{\Delta G}
    &=\underbrace{\frac{h}{h+\alpha k}}_{\substack{\text{이자율 상승에 따른}\\\text{구축효과}}}\cdot\underbrace{\frac{1}{1-MPC}}_{\substack{\text{정부지출의}\\\text{순수 승수효과}}} >0
    \end{aligned}$$

### 조세 감면 정책

- 조세 감면 정책 시행:

    $$
    \overline{T}\to \overline{T}+\Delta T
    \quad\Longleftrightarrow\quad
    \overline{A}\to\overline{A}+\frac{MPC}{1-MPC}\Delta T
    $$

- 균형실질이자율 상승:

    $$\begin{aligned}
    r^{\prime}
    &=\frac{k}{h+\alpha k}\overline{A}-\frac{1}{h+\alpha k}\cdot\frac{M}{\overline{P}}+\frac{k}{h+\alpha k}\cdot\frac{MPC}{1-MPC}\Delta T\\
    &=r^{*}+\frac{k}{h+\alpha k}\cdot\frac{MPC}{1-MPC}\Delta T\\
    \therefore\frac{\Delta r}{\Delta T}
    &=\frac{k}{h+\alpha k}\cdot\frac{MPC}{1-MPC} >0
    \end{aligned}$$

- 균형국민소득 증가:

    $$\begin{aligned}
    Y^{\prime}
    &=\frac{h}{h+\alpha k}\overline{A}+\frac{\alpha}{h+\alpha k}\cdot\frac{M}{\overline{P}}+\frac{h}{h+\alpha k}\cdot\frac{MPC}{1-MPC}\Delta T\\
    &=Y^{*}+\frac{h}{h+\alpha k}\cdot\frac{MPC}{1-MPC}\Delta T\\
    \therefore\frac{\Delta Y}{\Delta T}
    &=\underbrace{\frac{h}{h+\alpha k}}_{\substack{\text{이자율 상승에 따른}\\\text{구축효과}}}\cdot\underbrace{\frac{MPC}{1-MPC}}_{\substack{\text{조세 감면의}\\\text{순수 승수효과}}} >0
    \end{aligned}$$

## 통화 정책의 유효성

![03](/assets/img/posts/7.ECONOMICS/3.macroeconomics/06-03.png){: width="100%"}

### 통화 긴축 정책

- 통화 긴축 정책 시행:

    $$
    M\to M-\Delta M
    $$

- 균형실질이자율 상승:

    $$\begin{aligned}
    r^{\prime}
    &=\frac{h}{h+\alpha k}\overline{A}-\frac{1}{h+\alpha k}\cdot\frac{M}{\overline{P}}+\frac{1}{h+\alpha k}\cdot\frac{1}{\overline{P}}\Delta M\\
    &=r^{*}+\frac{1}{h+\alpha k}\cdot\frac{1}{\overline{P}}\Delta M\\
    \therefore\frac{\Delta r}{\Delta M}
    &=\frac{1}{h+\alpha k}\cdot\frac{1}{\overline{P}}
    \end{aligned}$$

- 균형국민소득 하락:

    $$\begin{aligned}
    Y^{\prime}
    &=\frac{h}{h+\alpha k}\overline{A}+\frac{\alpha}{h+\alpha k}\cdot\frac{M}{\overline{P}}-\frac{\alpha}{h+\alpha k}\cdot\frac{1}{\overline{P}}\Delta M\\
    &=Y^{*}-\frac{\alpha}{h+\alpha k}\cdot\frac{1}{\overline{P}}\Delta M\\
    \therefore\frac{\Delta Y}{\Delta M}
    &=-\frac{\alpha}{h+\alpha k}\cdot\frac{1}{\overline{P}}
    \end{aligned}$$

### 통화 완화 정책

- 통화 완화 정책 시행:

    $$
    M\to M+\Delta M
    $$

- 균형실질이자율 하락:

    $$\begin{aligned}
    r^{\prime}
    &=\frac{h}{h+\alpha k}\overline{A}-\frac{1}{h+\alpha k}\cdot\frac{M}{\overline{P}}-\frac{1}{h+\alpha k}\cdot\frac{1}{\overline{P}}\Delta M\\
    &=r^{*}-\frac{1}{h+\alpha k}\cdot\frac{1}{\overline{P}}\Delta M\\
    \therefore\frac{\Delta r}{\Delta M}
    &=-\frac{1}{h+\alpha k}\cdot\frac{1}{\overline{P}}
    \end{aligned}$$

- 균형국민소득 상승:

    $$\begin{aligned}
    Y^{\prime}
    &=\frac{h}{h+\alpha k}\overline{A}+\frac{\alpha}{h+\alpha k}\cdot\frac{M}{\overline{P}}+\frac{\alpha}{h+\alpha k}\cdot\frac{1}{\overline{P}}\Delta M\\
    &=Y^{*}+\frac{\alpha}{h+\alpha k}\cdot\frac{1}{\overline{P}}\Delta M\\
    \therefore\frac{\Delta Y}{\Delta M}
    &=\frac{\alpha}{h+\alpha k}\cdot\frac{1}{\overline{P}}
    \end{aligned}$$
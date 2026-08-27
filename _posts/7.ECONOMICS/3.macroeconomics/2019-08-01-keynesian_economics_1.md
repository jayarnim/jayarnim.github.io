---
order: 4
title: Keynesian Economics (1) Real Market
date: 2019-08-01
categories: [7.ECONOMICS, 3.macroeconomics]
tags: [economics, macroeconomics, keynesian economics]
math: true
description: >-
    Based on the lecture "Macroeconomics (2017-1)" by Prof. Hyun Hak Kim, Dept. of Economics, College of Economics & Commerce, Kookmin Univ.
image:
    path: /assets/img/posts/7.ECONOMICS/3.macroeconomics/Thumbnail.jpg
---

## 국민소득결정모형

![01](/assets/img/posts/7.ECONOMICS/3.macroeconomics/04-01.png){: width="100%"}

- **국민소득결정모형(Income-Determination Model)**: 투자, 정부지출, 조세가 외생적이라는 가정 하에 총수요(Aggregate Demand; AD)와 총공급(Aggregate Supply; AS)의 관계를 나타내는 모형으로서 **케인스의 십자가(The Keynesian Cross)**라고도 불림

- 소비함수(Consumption Function) 가정:

    $$\begin{aligned}
    C
    &=C_{0}+MPC(D-\overline{T}),\quad 0<MPC<1
    \end{aligned}$$

- 한계소비성향(Marginal Propensity to Consume; MPC)은 $1$ 보다 작으므로 분배 부문($D$)과 지출 부문($E$)이 항상 일치한다고 볼 수 없음:

    $$\begin{aligned}
    E
    &=C_{0}+I_{0}+G_{0}+MPC(D-\overline{T})\\
    &=\left(C_{0}+I_{0}+G_{0}-MPC\cdot\overline{T}\right)+MPC\cdot D
    \end{aligned}$$

## 유효수요의 원리

![02](/assets/img/posts/7.ECONOMICS/3.macroeconomics/04-02.png){: width="100%"}

### 신고전학파

- **세이의 법칙(Say's Law)**: 공급은 스스로 수요를 창출한다는 법칙으로, 생산하기 위해서는 댓가를 지불하여야 하고(분배), 이 댓가는 지출의 재원이 되므로 한 경제에서 공급 과잉이 지속되지 않는다는 법칙

    $$
    D\equiv Y\equiv E
    $$

- (1) 완전고용 수준에서 형성된 총공급이 국민소득을 결정하고, (2) 공급 부문에서 결정된 국민소득과 총수요가 일치하는 수준으로 **물가가 신속하게 조정되어** 총공급이 청산됨:

    $$
    \underbrace{C+S+T}_{=:D}
    \equiv Y
    =\underbrace{C+I+G}_{=:E}
    $$

- (편의상 균형 재정 가정 하에) 실물 시장에서 분배 부문과 지출 부문의 일치를 위하여 대부자금시장을 상정하고 해당 시장에서 실질이자율을 매개로 투자와 저축을 일치시킴:

    $$
    \overline{S}
    =I(r),
    \quad\text{where}\quad r=r^{*}
    $$

- (참고) 신고전학파는 교환 방정식을 근거로 물가($P$)가 변화하는 원인을 국민소득($Y$)과 통화량($M$)에서 찾고 있으며, 총공급이 국민소득($Y$)을 결정하므로 총수요 곡선의 이동은 통화량에 의해서만 발생함:

    $$
    M\overline{V}=PY
    \Longleftrightarrow
    P=\frac{M\overline{V}}{Y}
    $$

### 케인지언

- **유효수요의 원리(Effective Demand)**: 화폐 지불 능력을 갖춘 유효수요가 국민소득을 결정한다는 원리

    $$
    D\equiv Y\overset{?}{\equiv}E
    $$

- 단기적으로는 하방 경직성으로 인하여 **물가가 신속하게 조정되기 어렵기 때문에**, (1) 개별 물가 수준에서의 유효수요가 주어지면 현재 물가 수준에 적합한 국민소득이 결정되고, (2) 수요 부문에서 결정된 국민소득과 일치하는 수준에서만 총공급이 청산 가능함:

    $$\begin{aligned}
    Y
    &=\frac{C_{0}+I_{0}+G_{0}-MPC\cdot\overline{T}}{1-MPC},
    \quad\text{where}\quad S=I
    \end{aligned}$$

- (편의상 균형 재정 가정 하에) 신고전학파는 저축이 실질이자율의 함수라는 전제 하에 대부자금시장을 상정하나, 저축은 가처분소득의 함수이므로 투자와 저축의 균형은 대부자금시장을 매개로 이루어진다고 볼 수 없음:

    $$
    S(Y-T)\overset{?}{=}I(r)
    $$

## 재정 정책의 유효성

- 소비함수(Consumption Function) 가정:

    $$\begin{aligned}
    C
    &=C_{0}+MPC(Y-\overline{T}),\quad 0<MPC<1
    \end{aligned}$$

- 총수요(Aggregate Demand; AD)와 총공급(Aggregate Supply; AS)의 균형점 도출:

    $$\begin{aligned}
    Y^{*}
    &=\frac{C_{0}+I_{0}+G_{0}-MPC\cdot\overline{T}}{1-MPC}
    \end{aligned}$$

- 정부지출의 승수효과(Government Spending Multiplier Effect):

    $$\begin{gathered}
    G_{0}
    \longrightarrow G_{0}+\Delta G\\
    \Downarrow\\
    \begin{aligned}
    Y^{\prime}
    &=\frac{C_{0}+I_{0}+G_{0}+\Delta G-MPC\cdot\overline{T}}{1-MPC}\\
    &=\frac{C_{0}+I_{0}+G_{0}-MPC\cdot\overline{T}}{1-MPC}+\frac{\Delta G}{1-MPC}\\
    &=Y^{*}+\underbrace{\frac{1}{1-MPC}}_{\text{정부지출의 승수 효과}}\cdot\Delta G
    \end{aligned}
    \end{gathered}$$

- 조세의 승수효과(Tax Multiplier Effect):

    $$\begin{gathered}
    \overline{T}
    \longrightarrow \overline{T}-\Delta T\\
    \Downarrow\\
    \begin{aligned}
    Y^{\prime}
    &=\frac{C_{0}+I_{0}+G_{0}-MPC\left(\overline{T}-\Delta T\right)}{1-MPC}\\
    &=\frac{C_{0}+I_{0}+G_{0}-MPC\cdot\overline{T}}{1-MPC}+\frac{MPC\cdot\Delta T}{1-MPC}\\
    &=Y^{*}+\underbrace{\frac{MPC}{1-MPC}}_{\text{조세의 승수 효과}}\cdot\Delta T
    \end{aligned}
    \end{gathered}$$

## 투자-저축 곡선

- **투자-저축 곡선(Invest-Saving Curve; IS Curve)**: **총공급과 총수요가 일치하는 국민소득과 실질이자율 조합을** 나타내는 곡선으로서, 총공급과 총수요의 일치는 투자와 저축의 일치 하에서 성립한다는 점에서 투자-저축 곡선이라고 부름

- 소비함수(Consumption Function) 가정:

    $$\begin{aligned}
    C
    &=C_{0}+MPC(Y-\overline{T}),
    \quad 0<MPC<1
    \end{aligned}$$

- 투자함수(Invest Function) 가정:

    $$\begin{aligned}
    I
    &=I_{0}-br,
    \quad b>0
    \end{aligned}$$

- 총수요(Aggregate Demand; AD)와 총공급(Aggregate Supply; AS)의 균형점 도출:

    $$\begin{aligned}
    Y
    &=\frac{C_{0}+I_{0}+G_{0}-br-MPC\cdot\overline{T}}{1-MPC},
    \quad\text{where}\quad S=I
    \end{aligned}$$

- 실질이자율에 대하여 정리:

    $$\begin{aligned}
    Y
    &=-\frac{b}{1-MPC}r+\frac{C_{0}+I_{0}+G_{0}-MPC\cdot\overline{T}}{1-MPC},
    \quad\text{where}\quad S=I
    \end{aligned}$$
---
order: 5
title: Keynesian Economics (2) Money Market
date: 2019-08-02
categories: [7.ECONOMICS, 3.macroeconomics]
tags: [economics, macroeconomics, keynesian economics]
math: true
description: >-
    Based on the lecture "Macroeconomics (2017-1)" by Prof. Hyun Hak Kim, Dept. of Economics, College of Economics & Commerce, Kookmin Univ.
image:
    path: /assets/img/posts/7.ECONOMICS/3.macroeconomics/Thumbnail.jpg
---

## 유동성 선호 이론

- **유동성 선호 이론(Liquidity Preference Theory)**: 경기가 불확실할수록 사람들이 자산 중 일부를 현금처럼 가장 유동성이 높은 형태로 보유하려는 성향이 있다는 이론
    - **교환의 동기(Transactive Motivation)**: 교환의 매개수단으로서의 보유 동기로서, 계획되었거나(거래적 동기; Transactive Motivation) 계획되지 않은(예비적 동기; Precautionary Movitation) 거래를 이행하기 위하여 보유함
    - **투기적 동기(Speculative Motivation)**: 유동성 높은 수익 자산으로서의 보유 동기로서, 명목이자율이 정상이자율에 비하여 낮을수록 증권보다 화폐를 투기 자산으로서 선호할 유인이 높음

- 케인지언의 화폐수요함수(Keynesian Money Demand Function):

    $$\begin{aligned}
    \frac{M_{D}}{\overline{P}}
    &=L(Y,i)\\
    &=\underbrace{kY}_{\text{교환의 수요}}-\underbrace{hi}_{\text{투기적 수요}},\quad k,b>0 
    \end{aligned}$$

    - $k$: 마샬의 $k$(Marshallian k)로서 화폐의 소득탄력성
    - $h$: 화폐의 명목이자율탄력성

- (참고) 신고전학파의 화폐수요함수(Neoclassical Money Demand Function):

    $$
    M\overline{V}
    =PY
    \Longleftrightarrow
    \frac{M_{D}}{P}
    =\frac{1}{\overline{V}}Y,
    \quad\overline{V}>0
    $$

    - $V$: 화폐 유통 속도(Velocity of Money)로서 관습적으로 고정되어 있으며 마샬의 $k$ 의 역수임

## 유동성 선호-화폐 공급 곡선

![01](/assets/img/posts/7.ECONOMICS/3.macroeconomics/05-01.png){: width="100%"}

- **유동성 선호-화폐 공급 곡선(Liquidity Preference-Money Supply Curve; LM Curve)**: 유동성 선호(Liquidity Preference), 즉 투기적 동기(Speculative Motivation)를 반영한 **실질화폐수요(Real Money Demand)와 통화량(Money Supply)이 일치하는 국민소득과 명목이자율의 조합을** 나타내는 곡선

    $$\begin{aligned}
    Y
    &=\frac{h}{k}i+\frac{1}{k}\cdot\frac{M}{\overline{P}}
    \end{aligned}$$

- (참고) 신고전학파의 화폐수요함수로부터 도출 가능한 LM 곡선:

    $$\begin{aligned}
    Y
    =\frac{MV}{P}
    =\frac{1}{k}\cdot\frac{M}{\overline{P}}
    \end{aligned}$$

- **유동성 함정(Liquidity Trap)**: 화폐의 명목이자율탄력성이 매우 높을 경우($h\to\infty$) LM 곡선이 수평이 되는 현상

    $$
    i
    =\frac{k}{h}Y-\frac{1}{h}\cdot\frac{M}{\overline{P}}
    $$

    - 명목이자율이 지나치게 낮은 상태에서는($i\to 0$) 증권의 상대 가격이 지나치게 높기 때문에, 민간부문에서는 증권의 상대 가격이 장래에 대폭 하락할 것이라는 기대가 형성되어($h\to\infty$) 그 대체재로서 안정성이 높은 화폐를 보유하려 함($M/P\propto -hi$)
    - 이에 따라 LM 곡선은 국민소득($Y$)에 대하여 수평선이 되므로($k/h\to 0$), 해당 구간(유동성 함정 구간)에서는 통화 정책(Monetary Policy)이 정상 작동하지 않음
    - 신고전학파의 관점이 반영된 LM 곡선은 화폐 보유 동기 중 교환의 동기(Transactive Motivation)가 극단적으로 실현된 상태인 반면, 유동성 함정 하의 LM 곡선은 투기적 동기(Speculative Motivation)가 극단적으로 실현된 상태로 볼 수 있음

- (참고) **통화 정책(Monetary Policy)**: 통화 공급량을 증가시키거나 감소시킴으로써 동일 국민소득 수준 하에서의 **명목이자율 수준을 조정하는 정책**으로, 명목이자율을 매개로 실질이자율을 조정하는 것을 최종 목표로 함

    $$
    i=r,\quad\because\pi^{e}=0\quad\text{where}\quad \mathrm{Short-Run}
    $$

    - **통화 긴축 정책(Monetary Tightening)**: 통화량을 줄여서($M\downarrow$) LM 곡선을 좌측으로 이동시킴으로써 동일 국민소득 수준 하에서 명목이자율 수준을 높이는 정책
    - **통화 완화 정책(Monetary Easing)**: 통화량을 늘려서($M\uparrow$) LM 곡선을 우측으로 이동시킴으로써 동일 국민소득 수준 하에서 명목이자율 수준을 낮추는 정책
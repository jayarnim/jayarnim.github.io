---
order: 3
title: Neoclassical Economics (2) Money Market
date: 2019-07-31
categories: [7.ECONOMICS, 3.macroeconomics]
tags: [economics, macroeconomics, classical economics]
math: true
description: >-
    Based on the lecture "Macroeconomics (2017-1)" by Prof. Hyun Hak Kim, Dept. of Economics, College of Economics & Commerce, Kookmin Univ.
image:
    path: /assets/img/posts/Economics/3.Macroeconomics/Thumbnail.jpg
---

## 화폐시장

- **화폐(Money)**: 즉시 결제 가능한 자산의 저량으로서, 필요의 이중일치를 생략하기 위한 목적에서 등장하였으며, 가치의 척도로서, 교환의 매개 수단으로서, 그리고 가치의 저장 수단으로서 기능함

- **화폐시장(Money Market)**: 화폐를 거래하는 시장으로서, 명목이자율(Nominal Interest Rate)을 화폐 단위당 시장 가격으로 하여 중앙은행(Central Bank)이 공급하고 민간부문(Private Sector)이 수요함

## 공급 부문

- **통화량(Money Supply; $M_{S}$)**: 시중에 유통되고 있는 화폐량

    $$
    M_{S}
    =C+D
    $$

    - **민간 부문의 현금보유량(Cash; $C$)**: 민간 부문에서 시중은행에 예치하지 않고 보유 중인 화폐량
    - **민감 부문의 예금(Deposit; $D$)**: 민간 부문에서 시중은행에 예치 중인 화폐량

- **본원 통화(Mondetary Base; $B$)**: 중앙은행이 화폐를 발행할 수 있는 독점적 권한에 기반하여 공급한 화폐량

    $$
    B
    =C+R
    $$

    - **민간 부문의 현금보유량(Cash; $C$)**: 민간 부문에서 은행에 예치하지 않고 보유 중인 화폐량
    - **시중은행의 지급준비금(Payment Reserves; $R$)**: 시중은행에서 민간 부문의 예금 인출을 대비하여 보유 중인 화폐량

- **현금예금율(Cash Ratio Deposit; $cr$)**: 예금 대비 현금보유량의 비율

    $$
    cr
    =\frac{C}{D}
    $$

- **지급준비율(Reserve Requirement Ratio; $rr$)**: 예금 대비 지급준비금의 비율

    $$
    rr
    =\frac{R}{D}
    $$

- **통화 승수(Nomey Multiplier; $m$)**: 본원 통화 단위당 창조하는 통화량

    $$\begin{aligned}
    m
    &=\frac{M_{S}}{B}\\
    &=\frac{C+D}{C+R}\\
    &=\frac{cr+1}{cr+rr}\\
    &=1+\frac{1-rr}{cr+rr}
    \end{aligned}$$

- **통화 창조(Credit Creation)**: 시중은행이 예금과 대출을 반복하는 과정을 통해 본원 통화는 증가하지 않았음에도 시중에 유통되는 통화량이 증가하는 현상

    $$
    M_{S}
    =B\cdot 1+B\cdot\frac{1-rr}{cr+rr}
    $$

## 수요 부문

- **화폐수요(Money Demand, $M_{D}$)**: 교환적 동기에 의하여 민간부문에서 명목소득 중 화폐로 보유하고자 하는 수량

    $$\begin{aligned}
    M_{D}
    &=k\cdot PY,\quad 0<k<1
    \end{aligned}$$

- **화폐 유통 속도(Velocity of Money; $V=1/k$)**: 화폐수요계수의 역수로서 화폐 단위당 평균 사용 횟수를 나타내며, 생산량(Output)을 통화량(Nominal Money Supply)으로 나눈 값

    $$
    V
    =\frac{PY}{M_{D}}
    $$

## 화폐수량설

- **인플레이션(Inflation)**: 화폐의 단위당 교환 가치가 하락하여 동일 생산량에 상응하는 화폐 단위가 증가함에 따라 물가가 상승하는 현상

    $$
    \pi
    =\frac{P_{t+1}-P_{t}}{P_{t}}
    $$

- **어빙 피셔(Irving Fisher)의 교환 방정식(Equation of Exchange)**: 명목총생산(Nominal Gross Domestic Product)은 화폐 시장에 유통된 화폐가 실물 시장에서 교환 목적으로 사용된 총 횟수와 일치한다는 방정식

    $$
    MV
    =PY
    $$ 

- **화폐수량설(Quantity Theory of Money)**: 화폐 유통 속도($V$)는 관습에 의하여 일정하다고 가정하고, 총생산($Y$)은 외생 변수라 가정하였을 때, 통화량($M$)의 증가가 물가($P$)의 상승을 야기한다는 가설

    $$\begin{aligned}
    g(M\overline{V})
    &=g(PY)\\
    \\
    g(M\overline{V})
    &=g(M)+g(\overline{V})\\
    &=m+0\\
    g(PY)
    &=g(P)+g(Y)\\
    &=\pi+g(Y)\\
    \\
    \therefore m
    &=\pi+g(Y)
    \end{aligned}$$

## 피셔 효과

- **이자율(Interest Rate)**: 화폐 단위당 임대 가격 (이하 원금이 $\$1$ 라고 가정)
    - **명목이자율(Nominal Interest Rate; $i$)**: 화폐 단위로 측정된 화폐 단위당 임대 가격
    
        $$
        \frac{1(1+i)}{1}
        =1+i
        $$
    
    - **실질이자율(Real Interest Rate; $r$)**: 실물 단위로 측정된 화폐 단위당 임대 가격

        $$
        \frac{1(1+i)}{P_{t+1}}/\frac{1}{P_{t}}
        =1+r
        $$

- **어빙 피셔(Irving Fisher)의 피셔 방정식(Fisher Equation)**: 명목이자와 실질이자, 그리고 물가상승의 상관관계를 규명하는 방정식

    $$\begin{aligned}
    \underbrace{(1+i)}_{\text{명목 이자}}
    &=\underbrace{(1+r)}_{\text{실질 이자}}\underbrace{(1+\pi^{e})}_{\text{물가 상승}}
    \end{aligned}$$

- **피셔 효과(Fisher effect)**: 중앙은행이 통화량을 늘리면 화폐수량설에 의하여 인플레이션이 발생하고, (실질이자율 $r$ 과 기대물가상승률 $\pi^{e}$ 이 충분히 작다는 가정 하에) 이때 실질이자율 $r$ 은 외생 변수이므로 피셔 방정식에 의하여 명목이자율 $i$ 이 기대물가상승률 $\pi^{e}$ 만큼 증가하게 됨

    $$\begin{aligned}
    i
    &=r+\pi^{e}+r\pi^{e}\\
    &\approx r+\pi^{e},\quad\text{subject to}\quad r,\pi^{e}\to 0
    \end{aligned}$$

    - 실질이자율 $r$ 은 대부자금시장의 공급 부문에 해당하는 저축(Saving; $S$)과 수요 부문인 투자(Invest; I)의 균형을 조정하는 가격으로 화폐 시장의 외생 변수에 해당함
    - 피셔 효과(Fisher effect)는 중앙은행의 통화 정책이 화폐의 단위당 교환 가치에만 영향을 미칠 뿐, 실질 부문(e.g. 생산요소시장, 대부자금시장, 생산물시장)에는 영향을 미치지 못한다는 것을 시사함
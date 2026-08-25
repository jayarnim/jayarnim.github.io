---
order: 1
title: What? Macroeconomics
date: 2019-07-29
categories: [7.ECONOMICS, 3.macroeconomics]
tags: [economics, macroeconomics]
math: true
description: >-
    Based on the lecture "Macroeconomics (2017-1)" by Prof. Hyun Hak Kim, Dept. of Economics, College of Economics & Commerce, Kookmin Univ.
image:
    path: /assets/img/posts/7.ECONOMICS/3.macroeconomics/Thumbnail.jpg
---

## 거시경제학

- **거시경제학(MacroEconomics)**: 각종 거시 경제 변수와 그 결정 요인 및 상호작용을 분석하여 외부 충격(재정 정책, 통화 정책 등)에 따른 시장의 변화와 단기 경기 변동 및 장기 경제 성장을 연구하는 학문

- **국민소득 삼면 등가의 원칙(Three Aspects of National Income Identity)**: 국민소득을 생산, 분배 및 지출의 어느 측면에서 측정하더라도 그 가치가 동일하다는 원칙

    $$
    D=Y=E
    $$

- **생산국민소득(Gross Domestic Product; GDP)**: 국내 경제주체들이 생산한 부가가치의 총합으로서 국내총생산

    $$
    Y
    =f(L,K)
    $$

- **분배국민소득(Gross Domestic Income; GDI)**: 국내 경제주체들이 생산 과정에 참여한 댓가(요소소득)의 총합으로서 국내총소득

    $$
    D
    =w\cdot L+v\cdot K+\pi
    $$

- **지출국민소득(Gross Domestic Expenditure; GDE)**: 국내 경제주체들이 생산된 총부가가치에 지출한 총합으로서 국내총지출

    $$
    E
    =C+I+G
    $$

## 신고전학파

>시장의 가격 변수는 완벽하게 신축적이므로, 경제는 정부 개입 없이도 스스로 청산하여 균형을 달성한다. 화폐는 단지 물가만 결정하는 중립적인 수단일 뿐이다.

- **고전적 이분법(Classical dichotomy)**: 화폐의 중립성(Neutrality of Money)에 의하여 실질 변수(실물 단위; Real Variables)와 명목 변수(화폐 단위; Nominal Variables)는 서로 영향을 주지 않고 독립적으로 결정된다는 법칙

- **왈라스의 법칙(Walras' Law)**: 모든 경제 주체는 예산 제약 하에서 경제적 의사 결정을 수행하기 때문에 모든 시장에서 발생하는 초과수요의 합은 $0$ 이 된다는 법칙

    $$
    \sum_{i=1}^{n}{p_{i}z_{i}}
    =0
    $$

- **세이의 법칙(Say's Law)**: 왈라스의 법칙(Walras' Law) 근거하여 공급은 스스로 수요를 창출한다는 법칙으로, 생산하기 위해서는 댓가를 지불하여야 하고(분배), 이 댓가는 지출의 재원이 되므로 한 경제에서 공급 과잉이 지속되지 않는다는 법칙
    - 실물 시장과 화폐 시장을 구분하여 왈라스의 법칙(Walras' Law)을 기술하면 다음과 같음:

        $$
        \underbrace{\sum_{i=1}^{n-1}{P_{i}(D_{i}-S_{i})}}_{\text{실물 시장}}+\underbrace{(D_{M}-S_{M})}_{\text{화폐 시장}}
        =0
        $$

    - 신고전학파에서는 화폐수요가 거래적 동기에 의해서만 발생한다고 가정하므로 화폐시장의 초과수요는 항상 $0$ 에 수렴함:

        $$
        D_{M}-S_{M}
        =0
        $$

    - 따라서 한 경제에서 실물 시장의 총수요(Aggregate Demand; AD)와 총공급(Aggregate Supply; AS)은 항상 균형을 이루게 됨:

        $$\begin{gathered}
        \sum_{i=1}^{n-1}{P_{i}(D_{i}-S_{i})}
        =0\\
        \Updownarrow\\
        \sum_{i=1}^{n-1}{P_{i}D_{i}}
        =\sum_{i=1}^{n-1}{P_{i}S_{i}}
        \end{gathered}$$

### (참고) 신고전학파 시장 구분

- **생산요소시장(Factor Market)**: 노동(Labor)과 자본(Capital)의 균형 가격 하에서 투입량이 결정되고, 이에 따라 최종적으로 **생산량(Gross Domestic Product)**이 결정되는 시장

    $$\begin{gathered}
    w=MP_{L},\quad v=MP_{K}\\
    \Downarrow\\
    Y=f(K,L)
    \end{gathered}$$

- **대부자금시장(Loanable Funds Market)**: 저축(Saving)과 투자(Invest)의 균형점에서 **실질이자율(Real Interest Rate)**이 결정되는 시장

    $$\begin{gathered}
    S=I(r)
    \end{gathered}$$

- **생산물시장(Goods Market)**: 공급 부문에서 결정된 생산량이 **시장 청산(Market Clearing)**되는 시장

    $$\begin{gathered}
    Y
    =C+I+G
    \end{gathered}$$

- **화폐시장(Money Market)**: 중앙은행의 통화량(Money Supply)과 민간 부문의 거래적 동기(Transaction Motive)에 의하여 **물가(Price)**가 결정되는 시장

    $$
    M_{S}
    =\frac{1}{V}\cdot PY
    $$

## 케인지언

>미래가 불확실할수록 유동성 선호로 인하여 화폐수요가 증가함에 따라 화폐시장의 명목이자율이 상승한다. 하지만 시장의 가격 변수는 단기적으로는 경직되어 있으므로(물가가 조정되지 않으므로) 시장이 스스로 청산하여 균형을 회복하기 어렵다. 따라서 유효수요를 관리하기 위하여 정부의 적극적 개입이 필요하다.<br>
- $i\to(i+\alpha)\Longrightarrow r\to(r+\alpha)\quad(\because i=r+\pi,\Delta\pi=0)$
- $I\mid (r+\alpha) < I \mid r\quad(\because\partial I/\partial r < 0)$
- $Y>C+I^{\prime}+G\quad(\because Y=C+I^{*}+G)$

- **유효수요의 원리(Principle of Effective Demand)**: 생산물시장은 생산요소시장에서 결정된 총생산이 자동으로 청산(Market Clearing)되는 시장이 아니라, 현재 물가 수준(Price)에서 형성된 총수요(Aggregate Demand; AD)에 적절한 총공급(Aggregate Supply; AS) 수준이 결정되는 시장임

    $$
    \underbrace{Y}_{AS}=\underbrace{C+I+G}_{AD}
    $$

- **유동성 선호 이론(Liquidity Preference Theory)**: 단기적으로는 물가(Price)가 경직되어 있으며, 화폐시장(Money Market)에서 결정되는 것은 물가(Price)가 아니라 명목이자율(Nominal Interest Rate)임

    $$
    \frac{M_{S}}{P}
    =L(Y,i)
    $$

### (참고) 케인지언 시장 구분

- **생산물시장(Goods Market)**: 유효수요(Effective Demand)가 **총공급(Aggregate Supply; AS)의 적정 수준을 결정하는 시장**으로서, 가격의 하방 경직성으로 인하여 유효수요(Effective Demand)는 화폐시장에서 결정된 명목이자율(Nominal Interest Rate)의 영향을 받음

    $$
    AS
    =AD
    $$

- **화폐시장(Money Market)**: 중앙은행의 통화량(Money Supply)과 민간 부문의 유동성 선호(Liquidity Preference)에 의하여 **명목이자율(Nominal Interest Rate)이 결정되는 시장**

    $$
    \frac{M_{S}}{P}
    =L(Y,i)
    $$
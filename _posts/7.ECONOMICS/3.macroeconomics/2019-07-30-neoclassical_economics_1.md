---
order: 2
title: Neoclassical Economics (1) Real Market
date: 2019-07-30
categories: [7.ECONOMICS, 3.macroeconomics]
tags: [economics, macroeconomics, neoclassical economics]
math: true
description: >-
    Based on the lecture "Macroeconomics (2017-1)" by Prof. Hyun Hak Kim, Dept. of Economics, College of Economics & Commerce, Kookmin Univ.
image:
    path: /assets/img/posts/7.ECONOMICS/3.macroeconomics/Thumbnail.jpg
---

## 가정

- **오일러의 정리(Euler's theorem)**: 생산함수가 규모수익불변(Constant Returns to Scale; CRS)이면, 즉 규모에 따라 증가하거나 감소하는 비율이 달라지지 않고 일정하다면(1차 동차함수), 그 생산함수는 각 생산요소의 한계효과와 그 생산요소 투입량의 합계로써 표현될 수 있음

    $$\begin{aligned}
    Y
    &=f(L,K)\\
    &=\frac{\partial f}{\partial L}L+\frac{\partial f}{\partial K}K\\
    &=MP_{L}L+MP_{K}K
    \end{aligned}$$

- **완전경쟁(Perfectly Competitive Market; PCM)** 하에서 재화나 용역의 교환 가치는 그 한계효과(Marginal Effect) 수준에서 결정됨:

    $$\begin{aligned}
    MP_{L}
    &=w\\
    MP_{K}
    &=v
    \end{aligned}$$

- **완전경쟁(Perfectly Competitive Market; PCM)** 하에서 생산함수가 **규모수익불변(Constant Returns to Scale; CRS)**이라면 국민소득 삼면 등가의 법칙(Three Aspects of National Income Identity)에 의하여 국내총생산(Gross Domestic Product)과 국내총소득(Gross Domestic Income)이 일치하므로 **이윤은 $0$ 이 됨**:

    $$\begin{aligned}
    Y
    &=w\cdot L + v\cdot K\\
    D
    &=w\cdot L+v\cdot K+\pi\\
    \therefore \pi
    &=0\quad(\because Y=D)
    \end{aligned}$$

## 실물 시장 균형

- **생산요소시장(Factor Market)**: 노동(Labor)과 자본(Capital)의 균형 가격 하에서 투입량이 결정되고, 이에 따라 최종적으로 **생산량(Gross Domestic Product)이 결정되는 시장**

    $$
    Y
    =D
    $$

- **대부자금시장(Loanable Funds Market)**: 저축(Saving)과 투자(Invest)의 균형점에서 **실질이자율(Real Interest Rate)이 결정되는 시장**

    $$
    \overline{S}
    =I(r)
    $$

    - **저축(Saving; $S$)**: 대부자금시장의 공급 부문으로서, 소득($Y$), 소비지출($C_{0}$), 정부지출($G_{0}$) 및 조세($T_{0}$)가 외생적으로 주어졌을 때, 민간부문의 가처분소득에서 소비지출을 제외한 소득과 정부부문의 조세수입에서 정부지출을 제외한 수입의 합계임

        $$\begin{aligned}
        \overline{S}
        &=Y-(C+G_{0})
        \end{aligned}$$

    - **투자(Invest; $I$)**: 대부자금시장의 수요 부문으로서, 실질이자율(Real Interest Rate)에 대하여 음의 상관관계를 가지는 함수로써 표현됨

        $$\begin{aligned}
        \frac{\partial I}{\partial r}
        <0
        \end{aligned}$$

- **생산물시장(Goods Market)**: 공급 부문에서 결정된 생산량이 **시장 청산(Market Clearing)되는 시장**으로서, 총수요(Aggregate Demand; AD)는 총공급(Aggregate Supply; AS)에 의하여 결정됨

    $$
    \underbrace{D=f(L,K)}_{\text{요소시장에서 공급량 결정}}=Y=\underbrace{C+I+G=E}_{\text{생산물시장에서 공급량 청산}}
    $$

## 정부지출 확대 정책의 구축효과

- **구축효과(Crowding-Out Effect)**: 정부지출을 늘려서 총수요(Aggregate Demand; AD)를 조정하려는 **재정 정책(Fiscal Policy)은 대부자금시장을 위축시킬 뿐** 가치 규모를 확대할 수 없음

- 정부지출을 늘렸다고 하자:

    $$
    G^{\prime}
    =G_{0}+\Delta G
    $$

- 대부자금시장 공급 부문이 조정되면서 실질이자율(Real Interest Rate)이 상승함에 따라 수요 부문이 위축됨:

    $$\begin{aligned}
    S^{\prime}
    &=Y-(C+G^{\prime})\\
    &=\underbrace{Y-(C+G_{0})}_{=\overline{S}}-\Delta G\\
    &=I(r)-\Delta G
    \end{aligned}$$

- 정부지출의 증가분은 투자지출의 감소분과 상쇄되므로 지출 규모는 이전과 동일함:

    $$\begin{aligned}
    C+(I(r)-\Delta G)+(G_{0}+\Delta G)
    &=C+I(r)+G_{0}
    \end{aligned}$$

## 조세 감면 정책의 유효성

- **리카도 대등정리(Ricardian equivalence)**: 정부지출 수준이 일정하다면 그 재원 조달 방법의 변화로는 민간부문의 지출 규모에 영향을 미칠 수 없다는 정리

- 소비지출의 $2$-기간 예산제약식:

    $$\begin{aligned}
    \underbrace{C_{1}}_{\text{1기간 소비지출}}+\underbrace{\frac{C_{2}}{1+r}}_{\text{2기간 소비지출}}
    &=\underbrace{(Y_{1}-T_{1})}_{\text{1기간 가처분소득}}+\underbrace{\frac{Y_{2}-T_{2}}{1+r}}_{\text{2기간 가처분소득}}
    \end{aligned}$$

- 정부지출의 $2$-기간 예산제약식:

    $$\begin{aligned}
    G_{1}+\frac{G_{2}}{1+r}
    &=T_{1}+\frac{T_{2}}{1+r}
    \end{aligned}$$

- 정부가 $1$ 기간에 조세를 감면한다고 하자. 정부는 지출 계획에 따라 예산을 확보하여야 하므로 국채를 발행하여 부족한 예산을 충당하고 그 비용을 $2$ 기간으로 전가하게 됨:

    $$\begin{aligned}
    T_{1}^{\prime}
    &=T_{1}-\Delta T\\
    T_{2}^{\prime}
    &=T_{2}+\Delta T
    \end{aligned}$$

- 최종적으로 민간부문의 평생 가처분소득식은 조세 감면 이전과 동일함:

    $$\begin{aligned}
    W^{\prime}
    &=Y-(T_{1}-\Delta T)+\frac{Y_{2}-(T_{2}+(1+r)\Delta T)}{1+r}\\
    &=\underbrace{(Y_{1}-T_{1})}_{\text{1기간 가처분소득}}+\underbrace{\frac{Y_{2}-T_{2}}{1+r}}_{\text{2기간 가처분소득}}+\underbrace{\Delta T-\Delta T}_{\text{조세 감면 효과}}
    \end{aligned}$$
---
order: 8
title: Solow-Swan Model
date: 2019-08-05
categories: [7.ECONOMICS, 3.macroeconomics]
tags: [economics, macroeconomics, economic growth theory, solow-swan model]
math: true
description: >-
    Based on the lecture "Macroeconomic Change and Growth (2018-2)" by Prof. Jai Hyun Nahm, Dept. of Economics, College of Economics & Commerce, Kookmin Univ.
image:
    path: /assets/img/posts/7.ECONOMICS/3.macroeconomics/Thumbnail.jpg
---

## 솔로우-스완 모형

- **경제성장론(Economic Growth Theory)**: 한 나라 구성원들의 생활수준을 장기적으로 향상시키는 요인에 관하여 연구하는 학문 (e.g. 물적 자본의 증가, 인적 자본의 향상, 과학 기술의 진보, 인구 증가 등)
    - **경제성장(Economic Growth)**: 한 나라 구성원들의 생활수준이 향상되는 현상으로서 **1인당 국내총생산(GDP)의 증가로** 정의함

- **솔로우-스완 모형(Solow-Swan Model)**: 인구 증가 및 기술 진보가 **자본의 축적에 따른 1인당 생활 수준 변화에** 미치는 영향을 동태적으로 분석하는 모형
    - **균형 성장(Balanced Growth Path)**: 경제는 1인당 국내총생산, 투자 및 소비가 균형적으로 성장하며, 그 동력은 저축률의 증가, 물적 자본의 증가, 인적 자본의 향상 혹은 인구 증가보다는 과학 기술의 진보에 있음을 함의함
    - **외생적 성장(Exogenous Growth)**: 단, 해당 모형은 기술진보율(Rate of Labor-Augmenting Technological Progress)을 외생적(Exogenous)으로 주어진 것으로 가정하므로 과학 기술의 진보 원리를 설명하지는 못한다는 한계가 있음

## 가정

- **총생산함수(Aggregate Production Function)**: 생산기술 수준이 외생적으로 주어졌을 때 국내총생산과 국내 동원 가능한 총생산요소 간 상관관계를 규명한 관계식으로서, **한계 생산 체감의 법칙(Diminishing Marginal Product)과 규모에 대한 수익 불변(Constant Returns to Scale; CRS)을 가정함**

    $$
    Y
    =F(K,L)
    $$

- **1인당 총생산함수(Production Function per Capita)**: 편의상 인구 수 $N$ 의 대리변수로서 노동자 수 $L$ 를 사용하며, 총생산함수의 규모 수익 불변 가정 하에 다음과 같이 도출 가능함

    $$
    \frac{Y}{L}
    =F\left(\frac{K}{L},\frac{L}{L}\right)
    \quad\Longleftrightarrow\quad
    y
    =f(k)
    $$

- **1인당 투자함수(Investment Function per Capita)**: 단기 경기 변동(Short-Run Business Cycles)에서는 저축(Saving)과 투자(Investment)가 균형을 이루지 않을 수 있으나, 장기 경기 성장(Long-Run Economic Growth) 과정에서는 저축(Saving)과 투자(Investment)가 균형을 이룬다고 가정함

    $$
    \frac{I}{L}
    =s\cdot F\left(\frac{K}{L},\frac{L}{L}\right)
    \quad\Longleftrightarrow\quad
    i
    =s\cdot f(k)
    $$

    - $s$: 저축률(Savings Rate)로서 외생적으로 주어짐

## 정상 상태

![01](/assets/img/posts/7.ECONOMICS/3.macroeconomics/08-01.png){: width="100%"}

- **자본의 운동 방정식(Equation of Motion for Capital)**: 시간의 흐름에 따른 자본 축적량을 나타내는 동태적 방정식

    $$\begin{aligned}
    \Delta k
    &=\frac{\mathrm{d}k}{\mathrm{d}t}\\
    &=i-d\cdot k\\
    &=s\cdot f(k)-d\cdot k
    \end{aligned}$$

    - $d$: 자본의 감가상각률(Depreciation Rate)

- **정상 상태(Steady States; s.s.)**: 1인당 자본의 순증가분이 $0$ 에 수렴하여 외부 교란 요인이 없는 한 유지되는 장기 균형(균제) 상태

    $$\begin{aligned}
    \Delta k
    =0
    \quad\Longleftrightarrow\quad
    s\cdot f(k)
    =d\cdot k
    \end{aligned}$$

- **수준 효과(Level Effect)**: 변수 $x$ 의 변화에 따른 (정상 상태에서의) 1인당 생활 수준 $y^{*}$ 의 변화 효과

    $$
    \frac{y_{1}^{*}-y_{0}^{*}}{x_{1}-x_{0}}
    $$

- **성장 효과(Growth Effect)**: 변수 $x$ 의 변화에 따른 (정상 상태에서의) 1인당 생활 수준의 성장률 $g(y^{*})$ 의 변화 효과

    $$
    \frac{\mathrm{d}g(y^{*})}{\mathrm{d}x},
    \quad\mathrm{for}\quad
    g(y)
    =\frac{\mathrm{d}y}{\mathrm{d}t}\cdot\frac{1}{y}
    $$

## 저축률의 변화

![01](/assets/img/posts/7.ECONOMICS/3.macroeconomics/08-02.png){: width="100%"}

- **황금률(Golden Rule; g.r.)**: 1인당 소비(Consumption per Capita)를 극대화하는 정상 상태(Steady States) 혹은 그러한 정상 상태를 형성하는 저축률(Savings Rate)로서, 한계 생산 체감의 법칙 가정 하에서는 자본의 한계 생산과 한계 비용(감가상각률)이 일치하는 수준에서 황금률이 결정됨

    $$\begin{aligned}
    s_{\text{g.r.}}
    &=\mathrm{arg} \max_{s}{(1-s)f(k^{*})}\\
    &=\mathrm{arg} \max_{s}{\left[f(k^{*})-d\cdot k^{*}\right]},
    \quad\because s\cdot f(k^{*})=d\cdot k\\
    &=\left\{s\mid\frac{\Delta f(k^{*}\mid s)}{\Delta k}=d\right\}
    \end{aligned}$$

- 위 그림에서 저축률을 $s_{0}\to s_{1}$ 로 증가시키면 정상 상태에서의 1인당 국내총생산 $y_{0}^{*}<y_{1}^{*}$, 1인당 투자 $i_{0}^{*}<i_{1}^{*}$ 는 모두 증가함. 따라서 저축률의 변화에 따른 1인당 국내총생산 및 1인당 투자의 수준 효과는 양적으로 발휘됨:

    $$
    \frac{y_{1}^{*}-y_{0}^{*}}{s_{1}-s_{0}}>0,
    \quad
    \frac{i_{1}^{*}-i_{0}^{*}}{s_{1}-s_{0}}>0
    $$

- 위 그림에서 저축률 $s_{0}$ 은 황금률에 해당함. 저축률을 $s_{0}\to s_{1}$ 로 증가시키면 정상 상태에서의 1인당 소비 $c_{0}^{*}>c_{1}^{*}$ 는 감소함. 따라서 저축률의 변화에 따른 1인당 소비의 수준 효과는 음적으로 발휘됨:

    $$
    \frac{c_{1}^{*}-c_{0}^{*}}{s_{1}-s_{0}}<0
    $$

- 정상 상태에서 1인당 국내총생산 $y^{*}=f(k^{*})$ 은 상수로 고정되므로 그 증가율은 $0$ 이 됨. 따라서 저축률의 변화에 따른 1인당 국내총생산, 1인당 투자 및 1인당 소비의 성장 효과는 존재한다고 볼 수 없음:

    $$
    \frac{\mathrm{d}y^{*}}{\mathrm{d}t}=0,
    \quad
    \frac{\mathrm{d}i^{*}}{\mathrm{d}t}=0,
    \quad
    \frac{\mathrm{d}c^{*}}{\mathrm{d}t}=0
    $$

## 인구 증가

![01](/assets/img/posts/7.ECONOMICS/3.macroeconomics/08-03.png){: width="100%"}

- 자본의 운동 방정식(Equation of Motion for Capital):

    $$\begin{aligned}
    \Delta k
    &=\frac{\mathrm{d}k}{\mathrm{d}t}\\
    &=\frac{\mathrm{d}(K/L)}{\mathrm{d}t}\\
    &=\frac{1}{L}\cdot\frac{\mathrm{d}K}{\mathrm{d}t}-\frac{K}{L}\cdot\frac{1}{L}\cdot\frac{\mathrm{d}L}{\mathrm{d}t}\\
    &=\frac{1}{L}\left(I-d\cdot K\right)-\left(\frac{1}{L}\cdot\frac{\mathrm{d}L}{\mathrm{d}t}\right)\frac{K}{L}\\
    &=i-d\cdot k-n\cdot k\\
    &=s\cdot f(k)-(d+n)\cdot k
    \end{aligned}$$

- 위 그림에서 인구가 $n$ 의 증가율로 $L_{0}\to L_{1}$ 로 증가하면 정상 상태에서의 1인당 국내총생산 $y_{0}^{*}>y_{1}^{*}$, 1인당 투자 $i_{0}^{*}>i_{1}^{*}$ 는 모두 감소함. 따라서 인구 증가에 따른 1인당 국내총생산 및 1인당 투자의 수준 효과는 음적으로 발휘됨:

    $$
    \frac{y_{1}^{*}-y_{0}^{*}}{L_{1}-L_{0}}<0,
    \quad
    \frac{i_{1}^{*}-i_{0}^{*}}{L_{1}-L_{0}}<0
    $$

- 인구가 $n$ 의 증가율로 $L_{0}\to L_{1}$ 로 증가하더라도 정상 상태에서 1인당 국내총생산 $y^{*}=f(k^{*})$ 은 상수로 고정되므로 그 증가율은 $0$ 이 됨. 따라서 인구 증가에 따른 1인당 국내총생산 및 1인당 투자의 성장 효과는 존재한다고 볼 수 없음:

    $$
    \frac{\mathrm{d}y^{*}}{\mathrm{d}t}=0,
    \quad
    \frac{\mathrm{d}i^{*}}{\mathrm{d}t}=0,
    \quad
    \frac{\mathrm{d}c^{*}}{\mathrm{d}t}=0
    $$

## 과학 기술의 진보

- **노동 증대형 기술 진보(labor-augmenting technological progress)**: 노동자의 효율성이나 생산성을 높여, 마치 노동자의 수가 증가한 것과 동일한 경제적 효과를 내는 기술 발전 형태

    $$\begin{aligned}
    Y
    =F(K,LE)
    \quad\mathrm{for}\quad
    g(E)\equiv z
    \end{aligned}$$

- **유효 노동(Effective Labor; $LE$) 단위당** 국내총생산, 투자 및 자본 정의:

    $$\begin{aligned}
    \upsilon\equiv\frac{Y}{LE}=E\cdot f(k),
    \quad
    \iota\equiv\frac{I}{LE}=E\cdot s\cdot f(k),
    \quad
    \kappa\equiv\frac{K}{LE}=E\cdot k
    \end{aligned}$$

- 자본의 운동 방정식(Equation of Motion for Capital):

    $$\begin{aligned}
    \Delta\kappa
    &=\frac{\mathrm{d}\kappa}{\mathrm{d}t}\\
    &=\frac{\mathrm{d}(K/LE)}{\mathrm{d}t}\\
    &=\frac{1}{LE}\cdot\frac{\mathrm{d}K}{\mathrm{d}t}-\frac{K}{LE}\cdot\frac{1}{LE}\cdot\frac{\mathrm{d}LE}{\mathrm{d}t}\\
    &=\frac{1}{LE}\left(I-d\cdot K\right)-\left(\frac{1}{LE}\cdot\frac{\mathrm{d}LE}{\mathrm{d}t}\right)\frac{K}{LE}\\
    &=\iota-d\cdot\kappa-z\cdot\kappa\\
    &=s\cdot f(\kappa)-(d+z)\cdot\kappa
    \end{aligned}$$

- 노동의 효율성(Efficiency of Labor)이 $E_{0}\to E_{1}$ 로 증가하면 정상 상태에서 **유효 노동 단위당($LE$) 국내총생산 및 투자는 감소하지만, 노동자 1인당($L$) 국내총생산 및 투자는 증가함**. 따라서 노동의 효율성 변화에 따른 국내총생산 및 투자의  수준 효과는 양적으로 발휘됨:

    $$
    \frac{y_{1}^{*}-y_{0}^{*}}{E_{1}-E_{0}}>0,
    \quad
    \frac{i_{1}^{*}-i_{0}^{*}}{E_{1}-E_{0}}>0
    $$

- **균형 성장(Balanced Growth Path; BGP)**: 정상 상태에서 유효 노동 단위당($LE$) 국내총생산은 상수로 고정되지만, 노동자 1인당($L$) 국내총생산($y=f(k)$), 투자($i=sf(k)$) 및 소비($c=(1-s)f(k)$)은 모두 동일한 속도로 성장함

    $$\begin{aligned}
    g(y)
    &=g\left(\frac{Y}{LE}\cdot E\right)\\
    &=\underbrace{g(\upsilon)}_{=0}+\underbrace{g(E)}_{=z}\\
    &=z
    \end{aligned}$$
---
order: 7
title: Keynesian Economics (4) AD-AS Model
date: 2019-08-04
categories: [7.ECONOMICS, 3.macroeconomics]
tags: [economics, macroeconomics, keynesian economics]
math: true
description: >-
    Based on the lecture "Macroeconomics (2017-1)" by Prof. Hyun Hak Kim, Dept. of Economics, College of Economics & Commerce, Kookmin Univ.
image:
    path: /assets/img/posts/7.ECONOMICS/3.macroeconomics/Thumbnail.jpg
---

## 총수요-총공급 모형

- **총수요-총공급 모형(`A`ggregate `D`emand-`A`ggregate `S`upply Model)**: 물가 수준과 국내총지출 및 국내총생산의 균형점과 그 변화 양상을 규명하는 모형

- **총수요 곡선(Aggregate Demand; AD)**: 각 물가 수준에서 소비자가 수요하는 재화와 용역의 수량(유효수요)을 나타내는 곡선으로서, IS-LM 모형에서 도출된 국민소득(국내총지출)의 균형점

    $$
    AD(P)
    =\frac{h}{h+\alpha k}\overline{A}+\frac{\alpha}{h+\alpha k}\cdot\frac{M}{P}
    $$

- **총공급 곡선(Aggregate Supply; AS)**: 각 물가 수준에서 생산자가 공급하고자 하는 재화와 용역의 수량(국내총생산)을 나타내는 곡선

    $$
    AS(P)
    =\begin{cases}\begin{aligned}
    AD(P),\quad&\mathrm{Short-Run}\\
    Y^{*}+\frac{1}{\lambda}(P-P^{e}),\quad&\mathrm{Long-Run}
    \end{aligned}\end{cases}
    $$

## (참고) 총공급 곡선 도출

![01](/assets/img/posts/7.ECONOMICS/3.macroeconomics/07-01.png){: width="100%"}

- **필립스 곡선(Phillips Curve)**: 단기적으로 **물가상승률(Inflation Rate)과 실업률(Unemployment Rate) 간 상충 관계가 있음을** 규명한 관계식으로서, 경기가 회복되어 일자리가 창출되면 총수요가 증가하여 물가가 상승하는 반면, 경기가 침체되어 실업자가 증가하면 총수요가 감소하여 물가가 하락하는 원리를 시사함

    $$
    \pi_{t}-\pi_{t}^{e}
    =-\beta(u_{t}-u_{n}),\quad\beta>0
    $$

    - $u_{n}$: 자연실업률(Natural Rate of Unemployment)

- **오쿤의 법칙(Okun's Law)**: 경제성장률(GDP Growth Rate)과 실업률(Unemployment Rate) 간 상충 관계가 있음을 규명한 관계식으로서, 경기가 회복되어 경제가 성장하면 일자리가 창출되어 실업률이 감소하고, 경기가 침체되어 경제 성장이 둔화되면 일자리가 감소하여 실업률이 증가하는 원리를 시사함

    $$
    u_{t}-u_{n}
    \approx-\gamma(Y_{t}-Y^{*}),\quad\gamma>0
    $$

    - $Y^{*}$: 완전고용산출량(Full-Employment Output)

- 필립스 곡선(Phillips Curve)에 오쿤의 법칙(Okun's Law)을 적용하여 물가상승률(Inflation Rate)과 경제성장률(GDP Growth Rate)의 관계식 도출:

    $$\begin{aligned}
    \pi_{t}
    &=\pi_{t}^{e}+\beta\gamma(Y_{t}-Y^{*})
    \end{aligned}$$

- 물가상승률(Inflation Rate)의 정의에 근거하여 물가(Price)와 국내총생산(GDP)의 관계식 도출:

    $$\begin{aligned}
    P_{t}
    &=P_{t}^{e}+\beta\gamma P_{t-1}(Y_{t}-Y^{*})
    \end{aligned}$$

- 국내총생산(GDP)에 대하여 정리:

    $$\begin{aligned}
    Y_{t}
    &=Y^{*}+\frac{1}{\lambda}(P_{t}-P_{t}^{e}),
    \quad\lambda>0
    \end{aligned}$$

## 기대 가설

- **정태적 기대(Static Expectation)**: 미래는 현재와 동일할 것이라는 가설로서, 해당 가설 하에서는 예상 물가 수준이 반복 누적되어 항상 동일한 방향으로 오류가 발생함 (체계적 오류)

    $$
    P_{t}^{e}
    =P_{t-1}
    $$

- `Neoclassic` **완전 예견(Perfect Foresight)**: 경제 주체들이 미래를 정확하게 맞춘다고 가정하는 가설

    $$
    P_{t}^{e}
    =P_{t}
    $$

- `Keynesian` **적응적 기대(Adaptive Expectation)**: 경제 주체들은 과거의 예측 오류를 바탕으로 미래의 기대를 수정한다는 이론 (과거 중심적 예측)

    $$\begin{aligned}
    P_{t}^{e}
    &=P_{t-1}^{e}+\alpha\underbrace{(P_{t-1}-P_{t-1}^{e})}_{\text{예측 오차}},\quad 0<\alpha<1\\
    &=\alpha\underbrace{P_{t-1}}_{\text{현재 물가}}+(1-\alpha)\underbrace{P_{t-1}^{e}}_{\substack{\text{과거 물가의}\\\text{가중 평균}}}\\
    &=\alpha P_{t-1}+(1-\alpha)\underbrace{(\alpha P_{t-2}+(1-\alpha)P_{t-2}^{e})}_{=:P_{t-1}^{e}}\\
    &=\alpha P_{t-1}+\alpha(1-\alpha)P_{t-2}+(1-\alpha)^{2}P_{t-2}^{e}\\
    &=\alpha P_{t-1}+\alpha(1-\alpha)P_{t-2}+(1-\alpha)^{2}\underbrace{(\alpha P_{t-3}+(1-\alpha)P_{t-3}^{e})}_{=:P_{t-2}^{e}}\\
    &=\alpha P_{t-1}+\alpha(1-\alpha)P_{t-2}+\alpha(1-\alpha)^{2}P_{t-3}+(1-\alpha)^{3}P_{t-3}^{e}\\
    &=\cdots
    \end{aligned}$$

- `New-classic` **합리적 기대(Rational Expectation)**: 경제 주체들은 현재 이용 가능한 모든 정보를 활용하여 합리적으로 예측한다는 이론 (미래 지향적 예측)

    $$
    P_{t}^{e}
    =\mathbb{E}\left[P_{t}\mid\Omega_{t-1}\right]
    $$
---
order: 9
title: Welfare Economics (2) Social Choice
date: 2019-07-23
categories: [Economics, Microeconomics]
tags: [Economics, Microeconomics, Welfare Economics, Pareto Efficiency, Pareto, Efficiency, Social Welfare, Welfare, Equity, Social Choice]
math: true
description: >-
    Based on the lecture "Applied Microeconomics (2018-2)" by Prof. Jin Woo Park, Dept. of Economics, College of Economics & Commerce, Kookmin Univ.
image:
    path: /_post_refer_img/Microeconomics/Thumbnail.jpg
---

## Pareto Efficiency
-----

- **자원 배분 상태에 대한 평가 기준**
    - **자원 배분의 효율성(Efficiency)** : 파레토 효율성(Pareto Efficiency)
    - **자원 배분의 형평성(Equity)** : 사회후생함수(Social Welfare Function)

### What? Pareto Efficiency

- **파레토 효율성(Pareto Efficiency)** : 임의의 경제주체의 효용수준을 이전보다 불리하게 만들지 않고서는 어떤 경제주체의 효용수준도 개선할 수 없을 정도로 자원이 배분되었음

- **예시**

    | 자원 배분 방법 | 부존자원량 | 총배분자원량 | $A$ | $B$ | 잉여자원량 |
    |---|---|---|---|---|---|
    | 배분1 | 100 | 100 | 30 | 70 | 0 |
    | 배분2 | 100 | 100 | 70 | 30 | 0 |
    | 배분3 | 100 | 100 | 50 | 50 | 0 |
    | 배분4 | 100 | 80 | 20 | 60 | 20 |
    | 배분5 | 100 | 80 | 60 | 20 | 20 |
    | 배분6 | 100 | 80 | 40 | 40 | 20 |

    - $\text{배분1},\text{배분2},\text{배분3}$ : 임의의 경제주체가 취득한 자원을 회수하지 않고서는 다른 경제주체의 자원 보유량을 개선할 수 없는 상태로서 **파레토 최적인 상태임(Pareto Optimal)**
    - $\text{배분4},\text{배분5},\text{배분6}$ : 임의의 경제주체가 취득한 자원을 회수하지 않고서도 잉여자원 $20$ 으로써 다른 경제주체의 자원 보유량을 개선할 수 있는 상태로서 **파레토 개선 가능한 상태임(Pareto Improvement)**
    - 따라서 $\text{배분1},\text{배분2},\text{배분3}$ 은 $\text{배분4},\text{배분5},\text{배분6}$ 보다 **파레토 우월함(Pareto Superiority)**

### Condition

- **생산의 효율성(Productive Efficiency)** : 사용 가능한 생산요소 제약 하 경제 전반의 재화 생산량을 극대화하여, 임의의 재화의 생산량을 몇 단위 포기하지 않고서는 다른 재화의 생산량을 개선하지 못하는 상태를 이룸

    $$
    MRTS^{(X)}_{L,K}=\frac{w}{v}=MRTS^{(Y)}_{L,K}
    $$

    <div style="text-align: center;">
        <img src="/_post_refer_img/Microeconomics/09-01.png" alt="01" width="100%">
        <p><em>생산요소 $L,K$ 제약 하 재화 $X,Y$ 에 대한 생산의 계약곡선</em></p>
    </div>

    <div style="text-align: center;">
        <img src="/_post_refer_img/Microeconomics/09-02.png" alt="02" width="100%">
        <p><em>상품 공간 상에 표현된 재화 $X,Y$ 에 대한 생산의 계약곡선으로서<br>생산가능경계(Production Possibility Frontier; PPF)</em></p>
    </div>

- **교환의 효율성(Allocative Efficiency)** : 배분 가능한 부존자원 제약 하 경제 전반의 효용을 극대화하여, 임의의 경제주체의 효용수준을 이전보다 불리하게 만들지 않고서는 다른 경제주체의 효용수준을 개선하지 못하는 상태를 이룸

    $$
    MRS^{(A)}_{X,Y}=\frac{P_X}{P_Y}=MRS^{(B)}_{X,Y}
    $$

    <div style="text-align: center;">
        <img src="/_post_refer_img/Microeconomics/09-03.png" alt="03" width="100%">
        <p><em>부존자원 $X,Y$ 제약 하 경제주체 $A,B$ 에 대한 교환의 계약곡선</em></p>
    </div>

- **총체적 효율성(Overall Efficiency)** : 사용 가능한 생산요소 제약 하 극대화된 재화 생산량을 경제주체들에게 모두 배분하여 경제 전반의 효용수준을 극대화한 상태를 이룸

    $$
    MRPT_{X,Y}=MRS_{X,Y}
    $$

    <div style="text-align: center;">
        <img src="/_post_refer_img/Microeconomics/09-05.png" alt="05" width="100%">
        <p><em>총체적 효율성 하에서는 재화별 한계기술대체율, 재화 간 한계생산변환율, 그리고 경제주체별 한계대체율이 일치함</em></p>
    </div>

    <div style="text-align: center;">
        <img src="/_post_refer_img/Microeconomics/09-04.png" alt="04" width="100%">
        <p><em>주어진 자원들과 기술 수준에서 달성 가능한 최대 효용 조합으로서<br>효용가능경계(Utility Possibility Frontier; UPF)</em></p>
    </div>

## Social Welfare Function
-----

- **사회후생함수(Social Welfare Function)** : 사회 구성원들의 효용수준($X$)과 사회후생수준($Y$) 간 상관관계를 나타내는 함수

    $$
    SW=F\left(U_{A},U_{B}\right)
    $$

    > 효율성의 정의가 파레토 효율성으로써 합의된 데 반해, 형평성은 윤리적 관점에 따라 그 해석이 다양함. 이에 따라 파레토 최적 상태 하 형평성 달성도를 나타내는 사회후생함수 역시 어느 하나로 합의되지 않고 다양한 형태를 띰.

- **(초기) 공리주의 사회후생함수(Utilitarian Social Welfare Function)** : 최대 다수의 최대 행복

    $$
    SW=U_{A}+U_{B}
    $$

    ![06](/_post_refer_img/Microeconomics/09-06.png){: width="100%"}

- **롤스 사회후생함수(Rawlsian Social Welfare Function)** : 최소 수혜자의 최대 이익

    $$
    SW=\min{\left[U_{A},U_{B}\right]}
    $$

    ![07](/_post_refer_img/Microeconomics/09-07.png){: width="100%"}

- **(실질적) 평등주의 사회후생함수(Egalitarian Social Welfare Function)** : 한계효용의 평등

    $$
    SW=\left(U_A\right)^{\alpha} \cdot \left(U_B\right)^{1-\alpha}
    $$

    ![08](/_post_refer_img/Microeconomics/09-08.png){: width="100%"}
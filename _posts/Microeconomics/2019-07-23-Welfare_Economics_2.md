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

- **자원 배분에 관한 사회적 의사결정 기준**

    > 주어진 자원들과 기술 수준에서 달성 가능한 최대 효용 조합 하에서 형평성 있는 지점을 선택함

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
        <p><em>총체적 효율성 하에서는 재화 간 한계생산변환율과 경제주체별 재화 간 한계대체율이 일치함</em></p>
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

    > 비록 효용이 주관적 개념이긴 하나, 개인 간에 질적으로는 차이가 없고, 오로지 양적으로만 차이가 있음. 따라서 사회 전체의 효용수준은 그저 그 사회 구성원들이 누리는 효용의 총합에 불과함.

    $$
    SW=U_{A}+U_{B}
    $$

    ![06](/_post_refer_img/Microeconomics/09-06.png){: width="100%"}

- **롤스 사회후생함수(Rawlsian Social Welfare Function)** : 최소 수혜자의 최대 이익

    > 사회 구성원들에게 무지의 베일을 씌운 원초적 상황 하에서 민주적으로 자원 배분 정책을 수립한다고 하자. 타인의 이익에 무관심하고 오로지 자신의 이익에만 관심이 있음에도 불구하고, 사회 구성원들은 자신이 최악의 상황에 처할 가능성을 고려하여 최소극대화 원칙에 근거한 배분 정책을 수립할 것임.

    $$
    SW=\min{\left[U_{A},U_{B}\right]}
    $$

    ![07](/_post_refer_img/Microeconomics/09-07.png){: width="100%"}

- **(실질적) 평등주의 사회후생함수(Egalitarian Social Welfare Function)** : 한계효용의 평등

    > 빈자에게 있어서 1원과 부자의 그것이 가지는 실질적 가치가 같다고 볼 수 없음. 따라서 사회 전체의 효용수준을 논함에 있어서 개인의 사정을 고려해야 함.

    $$
    SW=\left(U_A\right)^{\alpha} \cdot \left(U_B\right)^{1-\alpha}
    $$

    ![08](/_post_refer_img/Microeconomics/09-08.png){: width="100%"}

### Impossibility Theorem

> 합리성의 공리와 민주성의 공리는 상호위배된다. 따라서 사회후생수준을 평가할 수 있는, 합리적인 동시에 민주적인 사회선호체계란 존재할 수 없다. (케네스 애로우)

- **합리적 사회선호체계의 공리**
    1. **완비성(Completeness)**; 사회선호체계가 모든 사회적 상태를 비교하고 평가할 수 있어야 한다.

        $$
        X \neq Y \implies X \succeq Y \;\text{or}\; Y \succeq X \quad\text{for}\quad X, Y \in \mathcal{S}
        $$

    2. **이행성(Transitivity)**; 사회적 상태 $X, Y, Z$ 에 대하여 사회선호체계가 $X$ 를 $Y$ 보다 선호하고 $Y$ 를 $Z$ 보다 선호하면 $X$ 를 $Z$ 보다 선호해야 한다.

        $$
        X \succeq Y \;\text{and}\; Y \succeq Z \implies X \succeq Z \quad\text{for}\quad X, Y, Z \in \mathcal{S}
        $$

    3. **파레토 원칙(Pareto Principle)**; 임의의 사회적 상태에 대하여 모든 사회 구성원들이 해당 사회적 상태를 다른 사회적 상태보다 선호한다면, 사회선호체계 역시 해당 사회적 상태를 다른 사회적 상태보다 선호해야 한다.

        $$\begin{aligned}
        X \succ_i Y \implies X \succ Y \quad\text{for}\quad X, Y &\in \mathcal{S},\\ i^{\forall} &\in N
        \end{aligned}$$

    4. **독립성(Independence)**; 사회선호체계가 두 가지 사회적 상태의 선호관계를 평가함에 있어서 이들과 무관한 것으로부터 영향을 받지 말아야 한다.

        $$\begin{aligned}
        X \succ Y \implies X \succ^{\prime} Y \quad\text{for}\quad X, Y &\in \mathcal{S},\\ Z &\in \mathcal{S} \setminus \{X, Y\}
        \end{aligned}$$

- **민주적 사회선호체계의 공리**
    5. **비독재성(Non-dictatorship)**; 사회선호체계가 사회 구성원 소수의 선호체계에 좌우되지 말아야 한다.

        $$
        \nexists i \in N \; \text{such that} \; X \succ_i Y \implies X \succ Y \quad\text{for}\quad X, Y \in \mathcal{S}
        $$

- **이행성과 민주성의 동시 성립 불가능성**
    - 사회 구성원 $A,B,C$ 가 사회적 상태 $X,Y,Z$ 에 대하여 각각 다음과 같이 평가한다고 하자

        $$\begin{aligned}
        A:\quad &X \succ_A Y \; \text{and} \; Y \succ_A Z\\
        B:\quad &Y \succ_B Z \; \text{and} \; Z \succ_B X\\
        C:\quad &Z \succ_C X \; \text{and} \; X \succ_C Y
        \end{aligned}$$

    - 사회선호체계는 파레토 원칙 및 비독재성에 의해 사회적 상태를 다음과 같이 평가함

        $$\begin{aligned}
        \mathcal{S}: X \succ Y \; \text{and} \; Y \succ Z \; \text{and} \; Z \succ X
        \end{aligned}$$

    - 따라서 민주성의 공리에 기초하여 도출한 사회선호체계는 이행성을 보장하지 못함
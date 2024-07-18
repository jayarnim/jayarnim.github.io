### Filter Approach

- **승산(Odds)** : 변수 $Y$ 가 반응할 가능성이 반응하지 않을 가능성보다 몇 배 높은가

    $$\begin{aligned}
    \text{odds}(Y)
    &= \frac{P(Y=1)}{1-P(Y=1)}
    \end{aligned}$$

- **승산비(Odds Ratio; OR)** : 변수 $X$ 가 참일 때 $Y$ 가 반응할 가능성이, $X$ 가 거짓일 때 $Y$ 가 반응할 가능성보다 몇 배 높은가

    $$\begin{aligned}
    \text{OR}(Y|X)
    &= \frac{\text{odds}(X=1)}{\text{odds}(X=0)}\\
    &= \frac{\frac{P(Y=1 \vert X=1)}{1-P(Y=1 \vert X=1)}}{\frac{P(Y=1 \vert X=0)}{1-P(Y=1 \vert X=0)}}
    \end{aligned}$$

    - $$ \text{OR}(Y \vert X) = 1 $$ : $X$ 의 변동이 $Y$ 의 변동에 영향을 미치지 않음
    - $$ \text{OR}(Y\vert X) < 1 $$ : $X$ 는 $Y$ 와 음의 상관관계에 있음
    - $$ \text{OR}(Y \vert X) > 1 $$ : $X$ 는 $Y$ 와 양의 상관관게에 있음

- **로지스틱 회귀식 가중치와 승산비의 상관관계 이해**

    - 단순 회귀 분석 하 로지스틱 회귀식은 다음과 같음

        $$
        \ln{\frac{P(Y=1)}{1-P(Y=1)}}
        =\beta_0 + \beta_1 X
        $$

    - $X=1$ 일 때의 로지스틱 회귀식

        $$\begin{aligned}
        \ln{\displaystyle\frac{P(Y=1 \vert X=1)}{1-P(Y=1 \vert X=1)}}
        &= \beta_0 + \beta_1 \times 1 \\
        &= \beta_0 + \beta_1
        \end{aligned}$$

    - $X=0$ 일 때의 로지스틱 회귀식

        $$\begin{aligned}
        \ln{\displaystyle\frac{P(Y=1 \vert X=0)}{1-P(Y=1 \vert X=0)}}
        &= \beta_0 + \beta_1 \times 0 \\
        &= \beta_0
        \end{aligned}$$

    - 두 회귀식을 빼면 다음과 같음

        $$\begin{aligned}
        &\ln{\displaystyle\frac{P(Y=1 \vert X=1)}{1-P(Y=1 \vert X=1)}} - \ln{\displaystyle\frac{P(Y=1 \vert X=0)}{1-P(Y=1 \vert X=0)}}\\
        &= \ln{\frac{\frac{P(Y=1 \vert X=1)}{1-P(Y=1 \vert X=1)}}{\frac{P(Y=1 \vert X=0)}{1-P(Y=1 \vert X=0)}}}\\
        &= (\beta_0 + \beta_1) - \beta_0\\
        &= \beta_1
        \end{aligned}$$

    - 따라서 설명변수 $X$ 의 가중치 $\beta_1$ 과 승산비 $\text{OR}(Y\|X)$ 간에는 다음과 같은 관계가 성립함

        $$\begin{aligned}
        \therefore \text{OR}(Y|X)
        &= \frac{\frac{P(Y=1 \vert X=1)}{1-P(Y=1 \vert X=1)}}{\frac{P(Y=1 \vert X=0)}{1-P(Y=1 \vert X=0)}} \\
        &= \exp[\beta_1]
        \end{aligned}$$
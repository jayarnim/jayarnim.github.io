# Index

1. 모델 복잡도와 과적합의 상관관계
2. 분산, 편향과 과적합의 상관관계
3. 정형화와 규제
4. `sklearn.linear_model.Lasso & Ridge`

<hr></br>


## 오차와 편향, 분산 간 상관관계 이해

- **잡음의 이해**

    $$\begin{aligned}
    y = f(x) + \varepsilon
    \end{aligned}$$

    - $y$ : 관측치의 실제값으로서 모수

    - $f(x)$ : 구현하고자 하는 관측치 생성 함수로서 모수의 추정량

    - $\varepsilon$ : 모수를 정확하게 추정하지 못하는 원인으로서 잡음(Noise)
        - $\varepsilon \sim N(0,\sigma^2)$ 가정

- 오차의 구성

    $$\begin{aligned}
    Err
    &= E[\varepsilon^2]
    &= E
    \end{aligned}$$


$$\begin{aligned}

Err
&= E[(y-\hat{y})^2]\\
&= E[(f(x)+\varepsilon-\hat{y})^2]\\
&= E[(f(x)-\hat{y})^2+\varepsilon^2+2\varepsilon(f(x)-\hat{y})]\\
&= E[(f(x)-\hat{y})^2]+E[\varepsilon^2]+2 \cdot E[\varepsilon] \cdot E[f(x)-\hat{y}]\\
&= E[(f(x)-\hat{y})^2] + \sigma^2 \quad (\because \varepsilon \sim N(0,\sigma^2))\\
\\
E[(f(x)-\hat{y})^2]
&= E[(f(x)-\overline{y}+\overline{y}-\hat{y})^2]\\
&= E[(f(x)-\overline{y})^2+(\overline{y}-\hat{y})^2+2 \cdot (f(x)-\overline{y}) \cdot (\overline{y}-\hat{y})]\\
&= E[(f(x)-\overline{y})^2]+E[(\overline{y}-\hat{y})^2]+2 \cdot E[f(x)-\overline{y}] \cdot E[\overline{y}-\hat{y}]\\
&= E[(f(x)-\overline{y})^2]+E[(\overline{y}-\hat{y})^2] \quad (\because E[f(x)-\overline{y}] = 0)\\
\\
Bias[\hat{y}]
&= E[\hat{y}-f(x)]\\
Var[\hat{y}]
&= E[(\hat{y}-E[\hat{y}])^2]\\
&= E[(\overline{y}-\hat{y})^2]\\
\\
\therefore Err
&= Bias[\hat{y}]^2 + Var[\hat{y}] + \sigma^2
\end{aligned}$$



## 모델 복잡도와 과적합의 상관관계

<p align="center"><a href="#"><img alt="과적합" src="https://github.com/jayarnim/jayarnim/assets/116495744/8acf85ff-c937-41e5-9633-1613c3b4c0f7" width=80%></a></p>

- 모델을 단순하게 설계할수록 모델이 관측치의 전반적인 특징을 제대로 포착하지 못해 **과소적합(UnderFitting)** 됨
- 모델을 복잡하게 설계할수록 모델이 표본에만 국한되어 나타나는 상세한 특징까지 포착하게 되어 표본에 **과대적합(OverFitting)** 됨

</br>

## 분산, 편향과 모델 복잡도의 상관관계

- **손실함수의 분해**
    - 선형회귀의 목적함수인 잔차 자승의 기대값을 $MSE$ 로 정의함

        $$\begin{aligned}
        \min_{\beta_0, \beta_j^{\forall}} {MSE}
        \end{aligned}$$

    - $MSE$ 를 추정량 $\hat{Y}$ 의 분산 $Var(\hat{Y})$ 와 편향 $Bias(\hat{Y})$ 으로 양분할 수 있음

        $$\begin{aligned}
        MSE
        &= E[(Y-\hat{Y})^2] \\
        &= Var(\hat{Y}) + (Bias(\hat{Y}))^2 \\
        &= Var(\hat{Y}) + \{(E(\hat{Y})-Y)^2\}
        \end{aligned}$$

- **분산과 편향의 이해**

    - $Var(\hat{Y})$ : 추정량의 기대값 $E(\hat{Y})$ 과 추정치 $\hat{y_i^{\forall}}$ 의 차이
    - $Bias(\hat{Y})$ : 모수 $Y$ 와 그 추정량의 기대값 $E(\hat{Y})$ 의 차이

    <p align="center"><a href="#"><img alt="분산과편향의이해" src="https://github.com/jayarnim/jayarnim/assets/116495744/cb542dc8-172e-4b66-9c09-93abdcbfec1a" width=80%></a></p>

- **분산, 편향과 모델 복잡도의 관계**

    <p align="center"><a href="#"><img alt="복잡도" src="https://github.com/jayarnim/jayarnim/assets/116495744/05e615db-1162-44ea-854b-11bebfc1c7a9" width=80%></a></p>

    - 모델을 복잡하게 설계할수록 예측값과 실제값의 차이는 감소하는 반면, 예측값과 그 평균의 차이는 증가함
    - 모델을 단순하게 설계할수록 예측값과 실제값의 차이는 증가하는 반면, 예측값과 그 평균의 차이는 감소함
    - 즉, 모델 복잡도는 편향과 음의 상관관계, 분산과 양의 상관관계에 있음

</br>

## 정형화와 규제

<p align="center"><a href="#"><img alt="정형화" src="https://github.com/jayarnim/jayarnim/assets/116495744/84cf465f-57ee-4b7e-8b04-04c1d80eff81" width=80%></a></p>

- **정형화(Regularization)** : 모델이 표본에 과적합되지 아니하고 일반화될 수 있도록 규제하는 작업

    $$\begin{aligned}
    \min_{\beta_0, \beta_j^{\forall}}(MSE + Penalty)
    &= \min_{\beta_0, \beta_j^{\forall}}(E[(Y-\hat{Y})^2] + Penalty) \\
    &= \min_{\beta_0, \beta_j^{\forall}}(Var(\hat{Y}) + (Bias(\hat{Y}))^2 + Penalty)
    \end{aligned}$$

    - 위 논의를 종합하면 편향이 클수록 모델이 단순하게 설계되어 과소적합될 가능성이 높음
    - 반대로 분산이 클수록 모델이 복잡하게 설계되어 표본에 과대적합될 가능성이 높음
    - 모델을 일반화하기 위해 편향과 분산을 포괄하는 $MSE$ 에 가중치에 관한 규제 $Penalty$ 를 더하여 예측 자유도를 제한함

- **규제(Penalty)의 종류**

    <p align="center"><a href="#"><img alt="규제비교" src="https://github.com/jayarnim/jayarnim/assets/116495744/5766884b-64dc-4099-a69f-6b295482458a" width=80%></a></p>

    - **L-1(Least Absolute Shrinkage and Selection Operator; LASSO)**

        $$\begin{aligned}
        Penalty
        &= \alpha ||\overrightarrow{w}||_{L1} \\
        &= \alpha \times (|\beta_1| + |\beta_2| + \cdots + |\beta_n|) \\
        &= \alpha \displaystyle\sum_{i=1}^{n}{|\beta_i|}
        \end{aligned}$$

    - **L-2(Ridge)**

        $$\begin{aligned}
        Penalty
        &= \alpha ||\overrightarrow{w}||_{L2} \\
        &= \alpha \times \{(\beta_1)^2 + (\beta_2)^2 + \cdots + (\beta_n)^2\} \\
        &= \alpha \displaystyle\sum_{i=1}^{n}{(\beta_i)^2}
        \end{aligned}$$











## Index

1. Ensemble
2. Voting
3. `sklearn.ensemble.VotingClassifier`

<hr></br>

## Ensemble

- **Ensemble** : 단일 모델들을 결합하는 기법

- **구분**
    - **Voting** : 단일 모델들을 수동으로 결합하는 방식

        <p align="center"><a href="#"><img alt="보팅" src="https://github.com/jayarnim/jayarnim/assets/116495744/505a65f5-cebd-4a62-a02d-3a6a7d19b066" width=80%></a></p>

    - **Bagging(Bootstrap Aggregating)** : 단일 모델들을 병렬로 작업하도록 설계하는 방식

        <p align="center"><a href="#"><img alt="bagging" src="https://github.com/jayarnim/jayarnim/assets/116495744/901c311e-f4bf-4df5-901a-88873b1a3e66" width=80%></a></p>

    - **Boosting** : 단일 모델들을 직렬로 심화 작업하도록 설계하는 방식

        <p align="center"><a href="#"><img alt="boosting" src="https://github.com/jayarnim/jayarnim/assets/116495744/020824f7-a8e4-4c67-825d-5c0cd3142f30" width=80%></a></p>

</br>

## Voting

- **Hard Voting** : 최빈값으로 관측치의 범주를 선정하는 방식

    <p align="center"><img alt="하드보팅" src="https://github.com/jayarnim/jayarnim/assets/116495744/115cdb86-1d0d-4cd9-adc7-136798eed8d1" width=80%></p>

- **Soft Voting** : 각 범주에 속할 확률에 대한 평균이 가장 큰 범주로 관측치의 범주를 선정하는 방식

    <p align="center"><img alt="소프트보팅" src="https://github.com/jayarnim/jayarnim/assets/116495744/fd6eaad0-54fa-403e-9957-345999429e6e" width=80%></p>

</br>

## [`sklearn.ensemble.VotingClassifier`](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.VotingClassifier.html#sklearn-ensemble-votingclassifier)

```python
from sklearn.svm import SVC
from sklearn.neighbors import KNeighborsClassifier
from sklearn.linear_model import LogisticRegression
from sklearn.ensemble import VotingClassifier

estimator_list = [
    ("Support Vector Machine", SVC()),
    ("k-NN", KNeighborsClassifier()),
    ("Logistic Regression", LogisticRegression())
    ]

voting_clf = VotingClassifier(
    n_jobs = -1,
    estimators = estimator_list,
    voting = 'soft'
    )
```
### 💡 General HyperParameter

- `n_jobs(default : None)` : 병렬로 작업할 코어 갯수

### 💡 Model HyperParameter

- `estimators` : 동원할 알고리즘 목록

- `weights(default : None)` : 각 알고리즘별 가중치

- `voting(default : 'hard')` : 결합 방식

    - `'hard'` : Hard Voting
    - `'soft'` : Soft Voting

</br><hr>

#### 이미지 출처
- https://velog.io/@jochedda
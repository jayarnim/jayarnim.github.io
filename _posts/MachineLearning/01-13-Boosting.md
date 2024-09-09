## Index

1. GBM
2. `sklearn.ensemble.GradientBoostingClassifier`

<hr></br>

## GBM

- [**Ensemble**](https://velog.io/@jayarnim/Ensemble-and-Voting)

- **Boosting** : 단일 모델들을 직렬로 심화 작업하도록 설계하는 방식

    <p align="center"><a href="#"><img alt="boosting" src="https://github.com/jayarnim/jayarnim/assets/116495744/020824f7-a8e4-4c67-825d-5c0cd3142f30" width=80%></a></p>

    - 이전 모델에 대하여 그 손실이 큰 관측치들을 **학습률(Learning Rate)**만큼 가중하여 심화학습함

        - [**경사하강법과 학습률의 이해**](https://velog.io/@jayarnim/%EA%B2%BD%EC%82%AC%ED%95%98%EA%B0%95%EB%B2%95%EA%B3%BC-SGDRegression)

- **Gradient Boosting Machine(GBM)** : **Decision Tree** 에 기반한 **Boosting Ensemble Algorithm**

    <p align="center"><a href="#"><img alt="그라디언트부스팅머신" src="https://github.com/jayarnim/jayarnim/assets/116495744/353d194d-74db-4a05-b0e9-88248d3925e9" width=80%></a></p>

    - [**Decision Tree**](https://velog.io/@jayarnim/%EA%B7%A0%EC%9D%BC%EB%8F%84%EC%99%80-Decision-Tree)

</br>

## [`sklearn.ensemble.GradientBoostingClassifier`](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingClassifier.html#sklearn-ensemble-gradientboostingclassifier)

```python
from sklearn.ensemble import GradientBoostingClassifier
```

### 💡 General HyperParameter

- `random_state(default : None)`
- `warm_start(default : False)` : 동작 메시지 출력 여부 설정

### 💡 Model HyperParameter

- **`criterion(default : 'friedman_mse')` : 오차($\approx$ 불순도) 측정 방법**
    - `'friedman_mse'`
    - `'squared_error'`

- `max_features(default : None)` : 규칙 설계 시 고려할 설명변수 갯수

    - `'sqrt'` : $\sqrt{n}$
    - `'log2'` : $\log_2{n}$
    - `None` : $n$

- **`n_estimators(default : 100)` : 동원할 Decision Tree 의 개수**

### 💡 Gradient Descent HyperParameter

- `learning_rate(default : 0.1)` : 학습률

- `loss(default : 'log_loss')` : 손실 함수
    - `'log_loss'`
    - `'deviance'`
    - `'exponential'`

- `tol(default : 0.0001)` : 허용 손실

- `n_iter_no_change(default : None)` : 손실이 몇 회 이상 유효하게 감소하지 않을 경우 학습을 중단할 것인가

### 💡 Pruning

- **Pre-Pruning**
    - `max_depth(default : 3)` : 트리 최대 깊이
    - `max_leaf_nodes(default : None)` : 리프 노드의 최대 갯수
    - `min_samples_split(default : 2)` : 하위 노드로 가지를 뻗기 위해 필요한 최소한의 샘플 개수
    - `min_impurity_decrease(default : 0)` : 하위 노드로 가지를 뻗기 위해 필요한 최소한의 불순도 개선 정도
    - `min_samples_leaf(default : 1)` : 리프 노드가 되기 위해 필요한 최소한의 샘플 개수

- **Cost-Complexity Pruning**

    - `ccp_alpha(default : 0)`









## Index

1. XGBoost
2. `xgboost.XGBClassifier`

<hr></br>

## XGBoost

- [**Ensemble**](https://velog.io/@jayarnim/Ensemble-and-Voting)

- **Boosting** : 단일 모델들을 직렬로 심화 작업하도록 설계하는 방식

    <p align="center"><a href="#"><img alt="boosting" src="https://github.com/jayarnim/jayarnim/assets/116495744/020824f7-a8e4-4c67-825d-5c0cd3142f30" width=80%></a></p>

    - 이전 모델에 대하여 그 손실이 큰 관측치들을 **학습률(Learning Rate)**만큼 가중하여 심화학습함

        - [**경사하강법과 학습률의 이해**](https://velog.io/@jayarnim/%EA%B2%BD%EC%82%AC%ED%95%98%EA%B0%95%EB%B2%95%EA%B3%BC-SGDRegression)

- **eXtreme Gradient Boosting(XGBoost)** : GBM을 균형 트리 분할 방식을 보존하면서 보완한 알고리즘

    - [**Decision Tree**](https://velog.io/@jayarnim/%EA%B7%A0%EC%9D%BC%EB%8F%84%EC%99%80-Decision-Tree)

    - [**Gradient Boosting Machine**](https://velog.io/@jayarnim/GBM)

    - **균형 트리 분할 방식(Level-Wise Tree Growth)** : 모든 리프 노드에서 균등하게 가지치기하는 방식

        <p align="center"><a href="#"><img alt="level" src="https://github.com/jayarnim/jayarnim/assets/116495744/f99789f7-ee66-4750-8bac-6c5caa9eb8a7" width=80%></a></p>

        - **장점** : 트리 형태가 비대칭적으로 형성되거나 깊이가 심화되지 않아 과대적합을 방지할 수 있음
        - **단점** : 손실을 최소화하지 못할 가능성이 높음

</br>

## `xgboost.XGBClassifier`

```python
from xgboost import XGBClassifier
```

### 💡 General HyperParameter

- `random_state(default : None)`
- `silent(default : 1)` : 동작 메시지 출력 여부 설정
- `n_jobs(default : None)` : 병렬로 작업할 코어 갯수

### 💡 Model HyperParameter

- `objective(default : 'binary:logistic')` : 목적 함수로서 GBM의 `criterion` 과 유사함
    - `'binary:logistic'` : 이항 분류 시 시그모이드 함수를 사용하여 관측치가 각 범주에 속할 확률을 반환함
    - `'multi:softprob'` : 다항 분류 시 소프트맥스 함수를 사용하여 관측치가 각 범주에 속할 확률을 반환함
    - `'multi:softmax'` : 다항 분류 시 소프트맥스 함수를 사용하여 관측치가 속할 확률이 가장 높은 범주를 반환함

- `n_estimators(default : 100)` : 동원할 Decision Tree 의 개수

### 💡 Gradient Descent HyperParameter

- `learning_rate(default : None)` : 학습률로서 통상 $0.1 \sim 0.2$ 의 값을 설정함

- `early_stopping_rounds(default : None)` : 손실이 몇 회 이상 유효하게 감소하지 않을 경우 학습을 중단할 것인가

### 💡 Pruning

- **Pre-Pruning**

    - `max_depth(default : None)` : 트리 최대 깊이로서 통상 $3 \sim 10$ 의 값을 설정함
    - `min_child_weight(default : None)` : 어떤 노드에 위치한 모든 관측치의 가중치 합에 대하여, 해당 노드가 하위 노드로 가지치기하기 위해 필요한 최소합
    - `max_leaves(default : None)` : 리프 노드의 최대 갯수
    - `gamma(default : None)` : 하위 노드로 가지치기 하기 위한 최소 손실 감소 값

### 💡 Validation Hyperperameter

```python
XGBClassifier.fit()
```

- `eval_set` : 교차검증 시 사용할 검증용 데이터 세트

- `eval_metric` : 교차검증 시 사용할 평가 지표
    - `error` : Binary classification error rate(임계값 0.5)
    - `logloss` : Negative log-likelihood
    - `merror` : multiclass classification error rate
    - `mlogloss` : multiclass logloss
    - `auc` : area under curve








## Index

1. LightGBM
2. `lightgbm.LGBMClassifier`

<hr></br>

## LightGBM

- [**Ensemble**](https://velog.io/@jayarnim/Ensemble-and-Voting)

- **Boosting** : 단일 모델들을 직렬로 심화 작업하도록 설계하는 방식

    <p align="center"><a href="#"><img alt="boosting" src="https://github.com/jayarnim/jayarnim/assets/116495744/020824f7-a8e4-4c67-825d-5c0cd3142f30" width=80%></a></p>

    - 이전 모델에 대하여 그 손실이 큰 관측치들을 **학습률(Learning Rate)**만큼 가중하여 심화학습함

        - [**경사하강법과 학습률의 이해**](https://velog.io/@jayarnim/%EA%B2%BD%EC%82%AC%ED%95%98%EA%B0%95%EB%B2%95%EA%B3%BC-SGDRegression)

- **Light Gradient Boosting Machine(LightGBM)** : GBM을 리프 중심 트리 분할 방식으로 보완한 알고리즘

    - [**Decision Tree**](https://velog.io/@jayarnim/%EA%B7%A0%EC%9D%BC%EB%8F%84%EC%99%80-Decision-Tree)

    - [**Gradient Boosting Machine**](https://velog.io/@jayarnim/GBM)

    - **리프 중심 트리 분할 방식(Leaf-Wise Tree Growth)** : 리프 노드 중 손실이 가장 큰 노드만 취사선택하여 분할하는 방식

        <p align="center"><a href="#"><img alt="leaf" src="https://github.com/jayarnim/jayarnim/assets/116495744/f2e375a3-baa6-43e7-ba0f-4a8940581a7f" width=80%></a></p>

        - **장점** : 리프 노드 중 손실이 큰 노드를 심화 작업하므로 손실 최소화에 뛰어남
        - **단점** : 트리 형태가 비대칭적으로 형성되거나 깊이가 심화되어 과대적합될 가능성이 높음

</br>

## `lightgbm.LGBMClassifier`

```python
from lightgbm import LGBMClassifier
```

### 💡 General HyperParameter

- `random_state(default : None)`
- `silent(default : 1)` : 동작 메시지 출력 여부 설정
- `n_jobs(default : -1)` : 병렬로 작업할 코어 갯수

### 💡 Model HyperParameter

- `objective(default : None)` : 목적 함수로서 GBM의 `criterion` 과 유사함
    - `binary` : 이항 분류 분석
    - `multiclass` : 다항 분류 분석

- `n_estimators(default : 100)` : 동원할 Decision Tree 의 개수

### 💡 Gradient Descent HyperParameter

- `learning_rate(default : 0.1)` : 학습률로서 통상 $0.1 \sim 0.2$ 의 값을 설정함

- `early_stopping_rounds(default : None)` : 손실이 몇 회 이상 유효하게 감소하지 않을 경우 학습을 중단할 것인가

### 💡 Pruning

- **Pre-Pruning**

    - `max_depth(default : -1)` : 트리 최대 깊이
    - `num_leaves(default : 31)` : 리프 노드의 최대 갯수
    - `min_child_samples(default : 20)` : 리프 노드 관측치의 최소 갯수
    - `min_child_weight(default : 0.001)` : 어떤 노드에 위치한 모든 관측치의 가중치 합에 대하여, 해당 노드가 하위 노드로 가지치기하기 위해 필요한 최소합
    - `min_split_gain(default : 0.0)` : 하위 노드로 가지치기 하기 위한 최소 손실 감소 값

### 💡 To Prevent Underfitting

- **About Imbalance in the number of observations between categories**

    - `class_weight(default : None)` : 가중할 범주와 그 값

        - `'balanced'`
        - `dictionary type`

### 💡 Validation Hyperperameter

```python
LGBMClassifier.fit()
```

- `eval_set` : 교차검증 시 사용할 검증용 데이터 세트

- `eval_metric` : 교차검증 시 사용할 평가 지표
    - `error` : Binary classification error rate(임계값 0.5)
    - `logloss` : Negative log-likelihood
    - `merror` : multiclass classification error rate
    - `mlogloss` : multiclass logloss
    - `auc` : area under curve
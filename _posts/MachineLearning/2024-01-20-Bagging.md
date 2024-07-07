## Index

1. Random Forest
2. `sklearn.ensemble.RandomForestClassifier`

<hr></br>

## Random Forest

- [**Ensemble**](https://velog.io/@jayarnim/Ensemble-and-Voting)

- **Bagging(Bootstrap Aggregating)** : 단일 모델들을 병렬로 작업하도록 설계하는 방식

    <p align="center"><a href="#"><img alt="bagging" src="https://github.com/jayarnim/jayarnim/assets/116495744/901c311e-f4bf-4df5-901a-88873b1a3e66" width=80%></a></p>

- **Random Forest** : **Decision Tree** 에 기반한 **Bagging Ensemble Algorithm**

    <p align="center"><a href="#"><img alt="랜덤포레스트" src="https://github.com/jayarnim/jayarnim/assets/116495744/675e25fe-d139-4d0f-8299-f2220661d28a" width=80%></a></p>

    - [**Decision Tree**](https://velog.io/@jayarnim/%EA%B7%A0%EC%9D%BC%EB%8F%84%EC%99%80-Decision-Tree)

</br>

## [`sklearn.ensemble.RandomForestClassifier`](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html#sklearn-ensemble-randomforestclassifier)

```python
from sklearn.ensemble import RandomForestClassifier
```

### 💡 General HyperParameter

- `random_state(default : None)`
- `warm_start(default : False)` : 동작 메시지 출력 여부 설정
- `n_jobs(default : None)` : 병렬로 작업할 코어 갯수

### 💡 Model HyperParameter

- `criterion(default : 'gini')` : 균일도 측정 방법
    - `'gini'` : 지니지수
    - `'entropy'` : 엔트로피지수

- `max_features(default : 'sqrt')` : 규칙 설계 시 고려할 설명변수 갯수

    - `'sqrt'` : $\sqrt{n}$
    - `'log2'` : $\log_2{n}$
    - `None` : $n$

- **`n_estimators(default : 100)` : 동원할 Decision Tree 의 개수**

### 💡 Pruning

- **Pre-Pruning**
    - `max_depth(default : None)` : 트리 최대 깊이
    - `max_leaf_nodes(default : None)` : 리프 노드의 최대 갯수
    - `min_samples_split(default : 2)` : 하위 노드로 가지를 뻗기 위해 필요한 최소한의 샘플 개수
    - `min_impurity_decrease(default : 0)` : 하위 노드로 가지를 뻗기 위해 필요한 최소한의 불순도 개선 정도
    - `min_samples_leaf(default : 1)` : 리프 노드가 되기 위해 필요한 최소한의 샘플 개수

- **Cost-Complexity Pruning**

    - `ccp_alpha(default : 0)`

### 💡 To Prevent Underfitting

- **About Imbalance in the number of observations between categories**

    - `class_weight(default : None)` : 가중할 범주와 그 값

        - `'balanced'`
        - `dictionary type`
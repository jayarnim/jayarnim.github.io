---
order: 2
title: Data Preprocessing
date: 2024-01-02
categories: [Artificial Intelligence, Machine Learning]
tags: [writing]
math: true
image:
  path: /img/MachineLearning/Thumbnail.jpg
---

# 💡 Data Preprocessing
-----

![01](/img/MachineLearning/02-01.jpg){: width="100%"}

- **정의** : 데이터를 분석에 사용할 수 있는 형식의 데이터로 만드는 일련의 과정

- **필요성** : 분석에 완벽하게 적합한 데이터를 얻는 것은 불가능함
    - **호환성 문제**
        - 데이터 불일치
        - 데이터 중복

    - **데이터 수집 문제**
        - 센서와 데이터베이스 간 통신 문제
        - 센서 자체 문제
        - 샘플링 기반 데이터 수집 정책

- **데이터 품질에 영향을 끼치는 인자**
    - **Nosie** : 데이터 측정 시 무작위로 발생하여 오류를 발생시키는 문제
    - **Outlier** : 대부분의 데이터와 다른 특성을 보이거나 특정 속성의 값이 유별난 데이터
    - **Artifact** : 어떤 요인으로 인해 반복적으로 발생하는 왜곡이나 오류
    - **Precision** : 동일한 결과물을 반복적으로 측정하였을 때 각 측정값 사이의 일관성 문제
    - **Bias** : 측정 장비에 포함된 시스템 상 문제
    - **Accuacy** : 측정 장비의 한계로 정확하지 않은 수를 측정함에 따라 발생하는 문제
    - **Inconsistent Value** : 데이터 불일치 문제
    - **Duplicate** : 데이터 중복 문제

- **절차**
    - **Data Integration** : 동일한 단위, 양식으로 데이터를 결합하는 절차

    - **Data Cleansing** : 낮은 품질의 데이터를 활용할 수 있도록 하는 절차
        - 중복값 제거
        - 결측치 처리
        - 이상치 처리

    - **Data Transformation** : 데이터 형식 및 구조를 학습에 적합하도록 변환하는 절차
        - 표준화(Standardization)
        - 정규화(Normalization)

    - **Data Reduction** : 고차원 데이터를 저차원 데이터로 변환하는 절차

# 💡 Data Cleansing
-----

### 결측치 처리

- **결측치 종류**
    - **완전 무작위 결측(Missing Completely At Random; MCAR)** : 데이터가 어떤 패턴이나 규칙 없이 누락되는 경우
    - **무작위 결측(Missing At Random; MAR)** : 데이터의 누락이 다른 변수에 종속된 경우
    - **비무작위 결측(Missing Not At Random; MNAR)** : 결측치가 어떤 규칙 또는 패턴을 따라 발생하는 경우

- **결측치 처리 권장 사항**
    - **10% 미만** : 제거 또는 대체
    - **10~20%** : 최빈값, 평균, 중앙값 등으로 대체
    - **20% 이상** : model-based method

### 이상치 처리

- **이상치의 정의** : 관측된 데이터의 범위에서 지나치게 벗어나 값이 매우 크거나 작은 값

- **이상치의 탐지** : Turkey Fence 기법

    ![02](/img/MachineLearning/02-02.png){: width="100%"}

    $$\begin{aligned}
    Outliers
    &=\{X|X < X_{lower} \; or \; X > X_{upper}\}
    \end{aligned}$$

    - **하한값($X_{lower}$)** : $Q_1-IQR \times 1.5$
    - **상한값($X_{upper}$)** : $Q_3+IQR \times 1.5$
    - **사분위 범위(InterQuartile Range; IQR)** : $Q_3 - Q_1$

# 💡 Data Transformation
-----

![03](/img/MachineLearning/02-03.png){: width="100%"}

### z-Score 정규화

```python
from sklearn.preprocessing import StandardScaler
```

- **정의** : 값의 분포를 평균이 0, 분산이 1인 형태로 변환함

    $$
    X_{scaled}=\frac{X_{origin}-E(X)}{\sigma}
    $$

- **기능** : 정규 분포화

### (이상치) 강건 정규화

```python
from sklearn.preprocessing import RobustScaler
```

- **정의** : 평균과 분산 대신 중앙값과 사분위 범위를 활용함

    $$
    X_{scaled}=\frac{X_{origin}-median}{IQR}
    $$

- **기능** : 이상치 영향력 최소화

### 최대-최소 정규화

```python
from sklearn.preprocessing import MinMaxScaler
```

- **정의** : 값의 분포를 특정 범위로 확대 혹은 축소함

    $$
    X_{scaled}=\frac{X_{origin}-X_{min}}{X_{max}-X_{min}}
    $$

- **기능** : 척도 통일
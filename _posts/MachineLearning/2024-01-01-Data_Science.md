---
order: 1
title: What? Data Science
date: 2024-01-01
categories: [Artificial Intelligence, Machine Learning]
tags: [writing]
math: true
image:
  path: /img/MachineLearning/Thumbnail.jpg
---

# 💡 Data-Driven Decision Making

-----

### 데이터 기반 의사결정

- **Descriptive** : Explains What Happend
    - Comprehensive, Accurate, Live Data
    - Effective Visualisation

- **Diagnostic** : Explains Why It Happend
    - Ability to Drill Down to the Root-cause
    - Ability to Isolate All Confounding Information

- **Predictive** : Forcasts What Might Happned
    - Business Have Remained Fairly Consistent Over Time
    - Historical Patterns Being Used to Predict Specific Outcomes Using Algorithms
    - Decisions are Automated Using Algorithms and Tech.

- **Prescriptive** : What Do I Need to Do?
    - Recommends Action Based On The Forecast
    - Applying Advanced Analytical Techs to Make Specific Recommendatons

### 데이터 기반 문제 해결 과정

- **문제 정의**

    > 어떤 문제를 해결할 것인가?
    > 이를 위해 필요한 데이터는 무엇인가?

- **데이터 획득**

    > 어떻게 데이터를 수집할 것인가?

- **데이터 탐색**

    > 데이터 전처리
    > 탐색적 자료 분석

- **모델링**

    > 문제에 맞는 기계학습 알고리즘 선택
    > 모델 구축

- **배포**

    > 제품 배포 및 시스템 유지 보수

# 💡 Data Science

-----

### 데이터 과학의 이해

- **정의**

    > 정형, 비정형의 다양한 데이터로부터 지식 및 시사점을 도출하는 데 과학적 방법론을 동원하는 융합 분야(출처 : 위키백과)

- **주요 개념**

    - **빅데이터(Bigdata)**

        > 통상적으로 사용되는 데이터 수집, 관리, 처리 소프트웨어의 수용 한계를 넘어서는 크기의 데이터(출처 : 위키백과)

        - Volume(Data Quantity)
        - Variety(Data Types)
        - Velocity(Data Speed)
        - Value(Data Impact)

    - **데이터 마이닝(Data Mining)**

        > 대규모로 저장된 데이터 안에서 체계적이고 자동적으로 통계적 규칙이나 짜임을 분석하여 가치 있는 정보를 빼내는 과정(출처 : 위키백과)

    - **기계학습(Machine Learning)**

        > 기계가 일일이 코드로 명시하지 않은 동작을 데이터로부터 학습하여 실행할 수 있도록 하는 알고리즘을 개발하는 연구 분야(출처 : 위키백과)

    - **인공지능(Artificial Intelligence; AI)**

        > 인간의 학습, 추론, 지각 능력을 인공적으로 구현하려는 컴퓨터 과학의 세부 분야(출처 : 위키백과)

### 기계학습의 분류

- **지도학습(Supervised Learning)**
    - **정의** : 정답 세트가 존재하는 데이터를 활용하는 학습 방법

    - **분류**
        - **판별 분석(Classificaiton)** : 범주형 값을 가지는 종속변수를 예측하는 방법론
        - **회귀 분석(Regression)** : 수치형 값을 가지는 종속변수를 예측하는 방법론

- **비지도학습(Unsupervised Learning)**
    - **정의** : 정답 세트가 존재하지 않는 데이터를 활용하는 학습 방법

    - **분류**
        - **군집화(Clustering)** : 유사한 개체들의 집단을 만든 후 새 개체가 어떤 집단과 유사한지 예측하는 방법론
        - **차원축소(Dimension Reduction)** : 고차원 데이터를 저차원 데이터로 변환하는 방법론

# 💡 [Scikit-Learn Library](https://scikit-learn.org/stable/#)

-----

- **API 사용 방법**

    1. 적절한 알고리즘 클래스 불러오기
    2. 인터페이스의 하이퍼 파라미터를 적절한 값으로 설정하여 인스턴스 생성
    3. 데이터 세트를 문제지(Feature)와 정답지(Traget)로 배치
    4. `fit()` 을 통해 인스턴스를 학습용 데이터 세트로 훈련
    5. `predict()` 을 통해 훈련된 인스턴스에 평가용 데이터 세트를 적용하여 성능 평가

### 모듈

- **알고리즘**    
    
    | 모듈 | 설명 | 예시 |
    |------|------|------|
    | sklearn.tree | 결정 트리 알고리즘 제공 | Decision Tree 등 |
    | sklearn.neighbors | 최근접 이웃 알고리즘 제공 | K-NN 등 |
    | sklearn.svm | 서포트 벡터 머신 알고리즘 제공 |
    | sklearn.naive_bayes | 나이브 베이즈 알고리즘 제공 | 가우시안 NB, 다항 분포 NB 등 |
    | sklearn.cluster | 클러스터링 알고리즘 제공 | K-Means, 계층형 클러스터링, DBSCAN 등 |
    | sklearn.linear_model | 회귀분석 알고리즘 제공 | 선형 회귀, 확률적 경사하강 회귀(SGD), 릿지(Ridge), 라쏘(Lasso), 로지스틱 회귀 등 |
    | sklearn.decomposition | 차원 축소 알고리즘 제공 | PCA, NMF, Truncated SVD 등 |
    | sklearn.ensemble | 앙상블 알고리즘 제공 | Random Forest, AdaBoost, GradientBoost 등 |

- **전처리**
    
    | 모듈 | 설명 | 예시 |
    |------|------|------|
    | sklearn.preprocessing | 데이터 전처리 기능 제공 | 인코더, 스케일러 등 |
    | sklearn.feature_selection | 특성(feature)을 선택할 수 있는 기능 제공 | 
    | sklearn.feature_extraction | 특성(feature)을 추출할 수 있는 기능 제공 |
    | sklearn.pipeline | 특성 처리, 학습, 예측을 묶어서 실행할 수 있는 기능 제공 |

- **검증 및 성능 평가 지표**

    | 모듈 | 설명 | 예시 |
    |------|------|------|
    | sklearn.model_selection | 교차 검증, 최적 하이퍼파라미터 추출 API 제공 | GridSearch 등 |
    | sklearn.metrics | 성능 평가 지표 제공 | Accuracy, Precision, Recall, ROC-AUC, RMSE 등 |

### 내장 데이터 세트

```py
sklearn.datasets
```

- **내장 데이터 형식**

    | 이름 | 설명 |
    |------|------|
    | DESCR | 자료에 대한 설명 |
    | data | 설명 변수 |
    | target | 반응 변수 |
    | feature_names | 설명 변수 이름 리스트 |
    | target_names | 반응 변수 이름 리스트 |    
    
- **내장 데이터 세트 목록**

    | 데이터 로드 함수 | 데이터 | 참고 |
    |------|------|------|
    | load_boston | 보스턴 집값 | 내장 데이터  |
    | load_diabetes | 당뇨병 |  |
    | load_linnerud | linnerud |  |
    | load_iris | 붓꽃 |  |
    | load_digits | 필기 숫자(digit) 이미지 |  |
    | load_wine | 포도주(wine) 등급 |  |
    | load_breast_cancer | 유방암 진단 |  |
    | fetch_california_housing | 캘리포니아 집값 | 인터넷 다운로드 |
    | fetch_covtype | 토지조사 |  |
    | fetch_20newsgroups | 뉴스 그룹 텍스트 |  |
    | fetch_olivetti_faces | 얼굴 이미지 |  |
    | fetch_lfw_people | 유명인 얼굴 |  |
    | fetch_lfw_pairs | 유명인 얼굴 |  |
    | fetch_rcv1 | 로이터 뉴스 말뭉치 |  |
    | fetch_kddcup99 | Kddcup 99 Tcp dump |  |
    | make_regression | 회귀분석용 | 가상 데이터 |
    | make_classification | 분류용 |  |
    | make_blobs | 클러스터링용 |  |
---
order: 1
title: What? RecSys
date: 2024-01-18
categories: [Research Interest, Recommender System]
tags: [Data Mining, Recommender System, Metric]
math: true
description: >-
    Based on the following lectures <br>
    (1) “Recommendation System Design (2024-1)” by Prof. Ha Myung Park, Dept. of Artificial Intelligence. College of SW, Kookmin Univ. <br>
    (2) "Recommender System (2024-1)" by Prof. Hyun Sil Moon, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
    path: /_post_refer_img/RecommenderSystem/Thumbnail.jpg
---

## What? RecSys
-----

- **추천시스템(Recommender System)** : 정보과부하 문제(Information Overload Problem)를 해결하기 위한 **개인화 정보 필터링 서비스(Personalized Information Filtering Service)** 로서, 사용자에게 적합한 아이템을 제안함으로써 개인화된 경험을 제공하는 기술

    - **정보과부하 문제(Information Overload Problem)** : 인간이 처리할 수 있는 정보량 이상의 정보가 제공되어 오히려 개인의 정보 학습 및 의사결정이 방해 받는 현상

- **검색 엔진과 비교**

    | | Search Engine | Recommender System |
    |---|---|---|
    | 사용자의 자세 | 능동성 | 수동성 |
    | 사용자 선호 파악 | 검색어 | 알고리즘 |
    | 사용자 선호 정보 | 검색 키워드 | 사용자 프로파일 <br> 아이템 프로파일 <br> **사용자 과거 행동** |

- **사용자-아이템 상호작용 데이터(User-Item Interaction Data)** : 사용자의 아이템에 대한 선호 여부 및 정도를 포함하는 데이터
    - **명시적 선호 데이터(Explicit Rating Data)** : 제시된 평가 시스템에 따라 직접 표출된 선호도
    - **암시적 선호 데이터(Implicit Rating Data)** : 행동을 통해 우회로 표출된 선호도
        - 암시적 선호를 순서적으로 나타내는 경우, 이를 선호보다는 확신으로 해석함
    - **순서적 선호 데이터(Ordinal Rating Data)** : 정해진 숫자 또는 연속적인 범위로 표시된 선호도
    - **단항 선호 데이터(Unary Rating Data)** : 상호작용이 있었다는 사실을 기록한 데이터

## Filtering Methods
-----

- **Most Popular(Best Seller)**

- **내용 기반 필터링 기법(`C`ontent-`b`ased Filtering Method; CB)** : 타깃 사용자가 상호작용한 아이템의 콘텐츠를 분석하여 이와 유사한 콘텐츠를 보유하고 있는 아이템을 추천하는 방법

    > Show me more of the same what I've liked!

    ![01](/_post_refer_img/RecommenderSystem/01-01.png){: width="100%"}

- **협업 필터링 기법(`C`ollaborative `F`iltering Method; CF)** : 타깃 사용자의 구매 기록을 바탕으로 유사한 사용자 혹은 아이템을 탐색하여 추천하는 방법

    > Tell me what's popular among my peers!

    ![02](/_post_refer_img/RecommenderSystem/01-02.png){: width="100%"}

- **하이브리드 기법(Hybrid Method)** : 협업 필터링 기법과 내용 기반 필터링 기법을 결합하는 방법

    | | Content-based Filtering | Collaborative Filtering |
    |---|---|---|
    | 빅데이터 | X | Rating Sparsity Problem |
    | 사용자 의존성 | X | Cold Start Problem |
    | 아이템 커스터마이징 | X | Grey Sheep Problem |
    | 도메인 지식 필요성 | Feature Engineering Problem | X |
    | 도메인 종속성 | X | CORS Problem <br> (`C`ross-`O`rigin `R`esource `S`haring) |
    | 추천 결과의 참신성 | X | Popularity Bias Problem |
    | 추천 결과의 의외성 | Trival Recommendation Problem | X |

## Goal
-----

- **추천시스템의 목적** : 고객 가치 창출을 통한 기업 이윤 도모
    - **가치 명제(Value Proposition)** : 고객이 필요로 하는 가치를 창출하기 위한 상품 및 서비스 조합
    - **구매 가치(Purchase Value)** : 상품 및 서비스를 구매함으로써 고객이 직접적으로 얻게 되는 실용 가치
    - **브랜드 가치(Brand Value)** : 브랜드에 대한 고객의 주관적/무형적 평가에 기초한, 고객이 특정 브랜드를 소유 및 경험함으로써 누리는 심리적 가치
    - **관계 가치(Relationship Value)** : 특정 기업에 대한 구매 가치나 브랜드 가치를 넘어서 기업이 고객과 형성하게 되는 관계의 양적, 질적 정도

- **좋은 추천시스템의 요건**
    - **효과적(Effective)** : 사용자에게 얼마나 잘 맞는 아이템을 제안할 수 있는가
    - **효율적(Efficient)** : 제안 생성 및 제공 과정에서 컴퓨팅 자원을 얼마나 잘 활용할 수 있는가
    - **설명력(Explainable)** : 사용자에게 아이템을 제안한 근거나 로직을 설명할 수 있는가
    - **설득력(Persuasive)** : 사용자가 제안된 아이템을 실제로 구매하거나 사용하도록 유도할 수 있는가

- **효과적인 추천의 목표**
    - **적합성(Relevance)** : 사용자가 관심 있을 것으로 짐작되는 아이템을 제안함
    - **참신성(Novelty)** : 사용자가 이전에 관측하지 못했을 것으로 짐작되는 아이템을 제안함
    - **의외성(Serendipity)** : 사용자가 예상하지 못했을 것으로 짐작되는 아이템을 제안함
    - **다양성(Diversity)** : 제안된 정보 묶음이 확일적이지 않고 다양한 특성을 가진 정보들로 구성되어 있음

## Metrics
-----

### Focusing on Relevance

- **Ordinal Rating Prediction**
    - RMSE(`R`oot `M`ean `S`quared `E`rror)
    - MAE(`M`ean `A`bsolute `E`rror)

- **Unary Rating Prediction**
    - Recall
    - Precision
    - F1-Score

- **Top-K Rank Prediction**
    - NDCG(`N`ormalized `D`iscounted `C`umulative `G`ain) : under the Explicit Ratings
    - MAP(`M`ean `A`verage `P`recision) : under the Implicit Ratings
    - MRR(`M`ean `R`eciprocal `R`ank)

### Focusing on Diversity

- **Variance-based Diversity**
    - Shanon Entropy
    - Simpson Concentration
    - Renyi Entropy

- **Equity-based Diversity**
    - The Gini Coefficient derived from a Lorenz curve

-----

### 이미지 출처

- https://towardsdatascience.com/essentials-of-recommendation-engines-content-based-and-collaborative-filtering-31521c964922
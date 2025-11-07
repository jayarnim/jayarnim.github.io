---
order: 2
title: Text Data Preprocessing
date: 2024-08-13
categories: [DATA MINING TECHS, 2.text analytics]
tags: [AI Application, NLP]
math: true
description: >-
    Based on the lecture “Text Analytics (2024-1)” by Prof. Je Hyuk Lee, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
    path: /_post_refer_img/DataMiningTechs/2.TextAnalytics/Thumbnail.png
---

## Text Analytics
-----

- **텍스트 애널리틱스(Text Analytics)** : 텍스트로부터 정보를 추출하는 과정

    > Text mining, text data mining(TDM) or text analytics is the process of deriving high-quality information from text. It involves "the discovery by computer of new, previously unknown information, by automatically extracting inofrmation from different written resources. (Wikipedia)

- **사례**

    | | 규칙 기반 방법론 | 통계적 방법론 | 신경망 기반 방법론 | RNN | Attention |
    |---|---|---|---|---|---|
    | 단어 표현 | One-Hot Encoding | - | Word2Vec | ELMo | - |
    | 문서 표현 | DTM | - | Doc2Vec | - | - |
    | 언어 모형 | - | SLM | NNLM | RNNLM | BERT |
    | 토픽 모형 | - | LSA, LDA | - | - | BERTopic |
    | 기계 번역 | RBMT | SMT | - | SEQ2SEQ | Transformer |
    | 생성 모형 | - | - | - | - | GPT |

## Process
-----

- **문제 정의(Problem Definition)**

    > 어떤 문제를 해결할 것인가? 이를 위해 필요한 데이터는 무엇인가?

- **텍스트 데이터 획득(Text Data Collection)**
    - 크롤링(Crawling)
    - 스크래이핑(Scraping) 등

- **텍스트 데이터 전처리(Text Data Preprocessing)** : 자연어를 특정 단위로 분할하고, 유용하지 않은 데이터를 제거하고, 동일한 의미를 가진 데이터를 획일화하는 작업
    - 토큰화(Tokenization)
    - 정제(Cleansing)
    - 정규화(Normalization) 등

- **벡터 표현(Vector Representation)** : 자연어를 컴퓨터가 이해할 수 있는 형식으로 표현하는 작업
    - 원-핫 인코딩(One-Hot Encoding)
    - 워드 투 벡터(Word2Vec) 등

- **모델링(Modeling)**
    - Summarization
    - Visualization
    - **Topic Model**
    - Docs Classification
    - Docs Clustering
    - **NLU(`N`atural `L`anguage `U`nderstanding)**
    - **NLG(`N`atural `L`anguage `G`eneration)**

## Text Data Preprocessing
-----

- **순서**
    1. 토큰화(Tokenization)
    2. 정제(Cleansing)
    3. 정규화(Normalization)

### Tokenization

- **자연어(Natural Language)** : 사람들이 일상적으로 쓰는 언어를 인공적인 언어인 인공어와 구분하여 부르는 개념(Wikipedia)
    - 형태상으로는 문자(Character)로, 의미상으로는 단어(Word)로 구성된 시계열 데이터(Sequence Data)
    - 자연어를 컴퓨터가 이해할 수 있는 형식으로 변환함에 있어, 그 의미가 반영될 수 있어야 함

- **토큰화(Tokenization)** : 주어진 말뭉치를 토큰 단위로 나누는 작업
    - **말뭉치(Corpus)** : 자연어 처리 목적으로 수집된 텍스트 데이터
    - **토큰(Token)** : 문장이나 단어 등 의미의 최소 단위

- **POS(`P`art `o`f `S`peech) Tagging** : (특히 동음이의어를 구분하기 위하여) 토큰에 그 앞, 뒤 문맥상 적합한 품사를 태깅하는 작업

### Cleansing

- **정제(Cleansing)** : 말뭉치에서 노이즈를 제거하는 작업
    - 등장 빈도가 적은 토큰 제거
    - (특히 영어에서) 길이가 짧은 토큰 제거
    - 불용어(Stopwords) 제거
    - 오탈자, 띄어쓰기 교정 등

### Normalization

- **정규화(Normalization)** : 다른 형태를 취하나 의미가 같은 단어들을 하나로 통합하여 동일한 표현으로 만드는 작업

- **표제어 추출(Lemmatization)** : 대상 토큰의 품사에 알맞은 표제어를 추출하는 행위
    - **표제어(Lemma)** : 기본 사전형 단어

- **어간 추출(Stemming)** : 단어의 변형된 형태를 제거하거나 치환하여 어간을 추출하는 행위로서, 형태학적 파싱보다는 정해진 규칙에 따라 접사를 잘라내는 작업에 가까움
    - **형태학(Morphology)** : 형태소로부터 단어가 형성되는 과정을 분석하는 학문
    - **형태소(Morpheme)** : 의미가 있는, 가장 작은 말의 단위
        - **어간(Stem)** : 단어의 의미를 담고 있는 부분
        - **접사(Affix)** : 단어에 추가적인 의미를 부여하는 부분

### Agglutinative Language

- **교착어(Agglutinative Language)** : 한국어 등 어간에 문법적으로 기능하는 형태소가 결합하여 문법적 기능이 부여되는 언어

- **자립형태소** : 자립하여 사용할 수 있는 형태소
    - 체언(명사, 대명사, 수사)
    - 수식언(관형사, 부사)
    - 감탄사 등

- **의존형태소** : 다른 형태소와 결합하여 사용되는 형태소
    - **어미** : 동사, 형용사의 어간에 결합하여 문법적 기능을 부여하는 형태소
    - **조사** : 체언에 결합하여 문법적 기능을 부여하는 형태소
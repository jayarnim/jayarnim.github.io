---
order: 4
title: Word Embedding Methods
date: 2024-08-01
categories: [AI & Data Mining, Text Analytics]
tags: [Data Mining, Text Mining]
math: true
description: >-
    Based on the lecture “Text Analytics (2024-1)” by Prof. Je Hyuk Lee, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
    path: /_post_refer_img/TextAnalytics/Thumbnail.png
---

## Word Embedding
-----

- **희소 표현(Sparse Representation)** : 하나의 단어를 하나의 차원으로 하는 $n$ 차원 공간에 단어를 표현하는 방법

    $$\begin{aligned}
    \text{Dog}&=\begin{pmatrix} 1 & 0 & 0 & 0 & 0 & \cdots \end{pmatrix}\\
    \text{Puppy}&=\begin{pmatrix} 0 & 0 & 1 & 0 & 0 & \cdots \end{pmatrix}
    \end{aligned}$$

    - Dimensionality Curse Problem in Sparse Vector
    - Semantic/Structural Disjointness Problem

- **단어 임베딩(Word Embedding)** : 희소 표현의 한계점을 보완한 바 분포 가설에 근거하여 단어를 밀집된 형태로 표현하는 방법

    > ***Embedding*** <br> An embedding is a mapping of a discrete - categorical - variable to a vector of continuous numbers. <br> In the context of machine learning, an embedding is a low-dimensional, learned continuous vector representation of discrete variables into which you can translate high-dimensional vectors.

    - **밀집 표현(Dense Representation)** : 연구자가 설정한 $k \le n$ 차원 공간에 단어를 표현하는 방법

        $$\begin{aligned}
        \text{Dog}&=\begin{pmatrix} 0.1 & 0.3 & -0.2 \end{pmatrix}\\
        \text{Puppy}&=\begin{pmatrix} 0.1 & 0.3 & -0.3 \end{pmatrix}
        \end{aligned}$$

    - **분산 표현(Distributed Representation)** : 분포 가설에 근거하여 ***단어의 의미*** 를 다차원 공간에 표현하는 방법

        - **분포 가설(Distributional Hypothesis)** : 비슷한 문맥에서 등장하는, 다시 말해 비슷하게 분포되어 있는 단어들은 비슷한 의미를 가짐

            $$\begin{aligned}
            &\text{My dog is cute. Sometimes my dog braks at me.}\\
            &\text{My puppy is cute. Sometimes my puppy braks at me.}
            \end{aligned}$$

## Word2Vec
-----

- **Word2Vec(Word to Vector)** : 단어 임베딩 학습 방법
    - **CBOW(`C`ontinuous `B`ag `o`f `W`ords)** : 주변 단어들로부터 중심 단어를 예측하는 과정에서 단어의 벡터 표현을 학습하는 방법
    - **Skip-Gram** : 중심 단어로부터 주변 단어들을 예측하는 과정에서 단어의 벡터 표현을 학습하는 방법
    - **SGNS(`S`kip-`G`ram with `N`egative `S`ampling)**

## Fast-Text
-----

## Glove
-----
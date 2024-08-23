---
order: 4
title: Word Representation
date: 2024-08-01
categories: [AI & Data Mining, Text Analytics]
tags: [Data Mining, Text Mining]
math: true
description: >-
    Based on the lecture “Text Analytics (2024-1)” by Prof. Je Hyuk Lee, Dept. of Data Science, The Grad. School, Kookmin Univ.
image:
    path: /_post_refer_img/TextAnalytics/Thumbnail.png
---

## Word Representation
-----

- **희소 표현(Sparse Representation)** : 하나의 단어를 하나의 차원으로 하는 $n$ 차원 공간에 단어를 표현하는 방법

    $$\begin{aligned}
    \text{Dog}&=\begin{pmatrix} 1 & 0 & 0 & 0 & 0 & \cdots \end{pmatrix}\\
    \text{Puppy}&=\begin{pmatrix} 0 & 0 & 1 & 0 & 0 & \cdots \end{pmatrix}
    \end{aligned}$$

    - Dimensionality Curse Problem in Sparse Vector
    - Semantic/Structural Disjointness Problem

- **밀집 표현(Dense Representation)** : 연구자가 설정한 $k \le n$ 차원 공간에 단어를 표현하는 방법

- **분산 표현(Distributed Representation)** : 분포 가설에 근거하여 ***단어의 의미*** 를 다차원 공간에 표현하는 방법

    - **분포 가설(Distributional Hypothesis)** : 비슷한 문맥에서 등장하는, 다시 말해 비슷하게 분포되어 있는 단어들은 비슷한 의미를 가짐

        $$\begin{aligned}
        &\text{My dog is cute. Sometimes my dog braks at me.}\\
        &\text{My puppy is cute. Sometimes my puppy braks at me.}
        \end{aligned}$$

## Word2Vec
-----

## Fast-Text
-----

## Glove
-----
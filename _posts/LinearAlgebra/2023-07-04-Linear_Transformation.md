---
order: 4
title: Linear Transformation
date: 2023-07-04
categories: [Mathematical Techs, Linear Algebra]
tags: [Mathematics]
math: true
description: >-
  Based on the lecture “Mathematics for Artificial Intelligence (2022-1)” by Prof. Yeo Jin Chung, Dept. of AI, Big Data & Management, College of Business Administration, Kookmin Univ.
image:
  path: /_post_refer_img/LinearAlgebra/Thumbnail.png
---

## Linear Transformation
-----

### 선형변환

- **정의** : 하나의 벡터를 입력하여 다른 벡터를 출력하는 함수

    ![01](/_post_refer_img/LinearAlgebra/04-01.jpg){: width="100%"}

- **기하학적 의미** : 평면을 휘어트리지 않는 선에서 벡터 공간을 늘리고 뒤틀어서 입력 벡터가 나타내는 직선을 출력 벡터가 나타내는 직선으로 변화하는 과정

    ![02](/_post_refer_img/LinearAlgebra/04-02.jpg){: width="100%"}

- **성질**
    - $L(\overrightarrow{v} + \overrightarrow{w}) = L(\overrightarrow{v}) + L(\overrightarrow{w})$
    - $L(\alpha \times \overrightarrow{v}) = \alpha L(\overrightarrow{v})$

- **선형변환을 통한 행렬과 벡터 곱의 이해**

    > 행렬 $$A = \begin{pmatrix} 1&3\\-2&0 \end{pmatrix}$$ 과 벡터 $$\overrightarrow{v} = \begin{pmatrix} 1\\-2 \end{pmatrix}$$ 의 곱은 $$\overrightarrow{v}$$ 에 대하여 단위벡터를 기저로 사용하는 직교좌표계에서 $$A$$ 의 열벡터 $$\overrightarrow{a_1}=\begin{pmatrix} 1\\-2 \end{pmatrix}, \overrightarrow{a_2}=\begin{pmatrix} 3\\0 \end{pmatrix}$$ 를 기저로 사용하는 좌표계로의 선형변환으로 이해할 수 있음

    $$\begin{aligned}
    L(\overrightarrow{v})
    &= L(\begin{pmatrix} 1\\-2 \end{pmatrix}) \\
    &= L(-1 \overrightarrow{i} + 2 \overrightarrow{j}) \\
    &= -1L(\overrightarrow{i}) + 2L(\overrightarrow{j}) \\
    &= -1 \begin{pmatrix} 1\\-2 \end{pmatrix} + 2\begin{pmatrix} 3\\0 \end{pmatrix} \\
    &= \begin{pmatrix} 1&3\\-2&0 \end{pmatrix} \begin{pmatrix} -1\\2 \end{pmatrix} \\
    &= \begin{pmatrix} 1&3\\-2&0 \end{pmatrix} \overrightarrow{v}
    \end{aligned}$$

### 기저의 변환과 좌표

- 벡터 $$\overrightarrow{v}=\begin{pmatrix}-1\\2\end{pmatrix}$$ 는 단위벡터 $$\overrightarrow{i}=\begin{pmatrix}1\\0\end{pmatrix}, \overrightarrow{j}=\begin{pmatrix}0\\1\end{pmatrix}$$ 를 기저로 사용하는 직교좌표계의 좌표 $$(x, y) = (-1, 2)$$ 을 의미함

    $$\begin{aligned}
    \begin{pmatrix}
    -1\\
    2
    \end{pmatrix}
    &= -1 
    \begin{pmatrix}
    1\\
    0
    \end{pmatrix}
    + 2
    \begin{pmatrix}
    0\\
    1
    \end{pmatrix}
    \end{aligned}$$

- 선형변환 $$L(\overrightarrow{v})$$ 를 통해 입력벡터 $$\overrightarrow{v}$$ 는 출력벡터 $$\begin{pmatrix}5\\2\end{pmatrix}$$ 로 변환되었음

    $$\begin{aligned}
    L(\overrightarrow{v})
    &= \begin{pmatrix}5\\2\end{pmatrix}
    \end{aligned}$$

- 출력벡터 $$\begin{pmatrix}5\\2\end{pmatrix}$$ 는 벡터 $$L(\overrightarrow{i})=\begin{pmatrix}1\\-2\end{pmatrix}, L(\overrightarrow{j})=\begin{pmatrix}3\\0\end{pmatrix}$$ 를 기저로 사용하는 변환된 좌표계의 좌표 $$(x, y) = (-1, 2)$$ 을 의미함

    $$\begin{aligned}
    \begin{pmatrix}5\\2\end{pmatrix}
    &= -1 \begin{pmatrix}1\\-2\end{pmatrix} + 2 \begin{pmatrix}3\\0\end{pmatrix}
    \end{aligned}$$

## 특별한 선형변환
-----

- **Rotation Matrix** : 반시계 방향으로 $\theta^{\circ}$ 회전하는 선형변환

    ![03](/_post_refer_img/LinearAlgebra/04-03.jpg){: width="100%"}

    $$
    \begin{pmatrix}
    \cos \theta & -\sin \theta \\
    \sin \theta & \cos \theta
    \end{pmatrix}
    $$

- **Scaling Matrix** : $X$ 축을 $\alpha$ 배, $Y$ 축을 $\beta$ 배 늘리는 선형변환

    ![04](/_post_refer_img/LinearAlgebra/04-04.png){: width="100%"}

    $$
    \begin{pmatrix}
    \alpha & 0 \\
    0 & \beta
    \end{pmatrix}
    $$

- **Shearing Matrix** : 각 축의 기저벡터를 변형시키는 선형변환

    ![05](/_post_refer_img/LinearAlgebra/04-05.jpg){: width="100%"}

    - **Horizontal Shearing Matrix(Shear in $$X$$)** : $$X$$ 축의 기저벡터는 그대로, $$Y$$ 축의 단위벡터는 $$\begin{pmatrix} s\\1 \end{pmatrix}$$ 으로 변형시키는 선형변환

        $$
        \begin{pmatrix} 1&s\\0&1 \end{pmatrix}
        $$

    - **Vertical Shearing Matrix(Shear in $$Y$$)** : $$Y$$ 축의 기저벡터는 그대로, $$X$$ 축의 단위벡터는 $$\begin{pmatrix} 1\\s \end{pmatrix}$$ 으로 변형시키는 선형변환

        $$
        \begin{pmatrix} 1&0\\s&1 \end{pmatrix}
        $$

    - **Arbitrary Shearing Matrix** : $$X$$ 축의 기저벡터는 $$\begin{pmatrix} 1\\ t \end{pmatrix}$$ 으로, $$Y$$ 축의 단위벡터는 $$\begin{pmatrix} s\\ 1 \end{pmatrix}$$ 으로 변형시키는 선형변환

        $$
        \begin{pmatrix} 1&s\\ t&1 \end{pmatrix}
        $$

## Determinant
-----

- **행렬식(Determinant; $det$)** : 행렬로 표현되는 선형변환의 어떤 특성을 표현하는 값

    $$
    \vert A \vert
    = \displaystyle\sum_{\sigma \in S_n} (sgn(\sigma) \prod_{i=1}^{n}a_{i,\sigma_{i}})
    $$

    - $S_n$ : $\{1,2,\cdots,n\}$ 의 모든 순열
    - $\sigma_i$ : $S_n$ 의 원소 중 하나인 $\sigma$ 의 $i$ 번째 원소
    - $sgn(\sigma)$ : 주어진 순열을 연속적으로 짝수만큼 움직였을 때 재정렬되면 $1$, 아니면 $-1$의 값을 가지는 규칙

- **행렬식의 기하학적 의미** : 행렬 $A$ 에 의한 선형변환이 변화시키는 면적의 비율 $c$

    ![06](/_post_refer_img/LinearAlgebra/04-06.jpg){: width="100%"}

- **$det(A)=0$ 인 경우의 기하학적 의미**

    $$\begin{aligned}
    A
    &= \begin{pmatrix} 4&2 \\ 2&1 \end{pmatrix} \\
    &= \begin{bmatrix} \overrightarrow{a_1} & \overrightarrow{a_2} \end{bmatrix}
    \end{aligned}$$

    - $det(A)=0$ 이면 행렬 $A$ 의 열벡터는 선형 종속임

        $$\begin{aligned}
        \overrightarrow{a_1}
        &= 2 \times \overrightarrow{a_2}
        \end{aligned}$$

    - $A$ 에 의한 선형변환은 모든 점을 $1$ 차원 직선에 $mapping$ 하여 그 면적을 $0$ 으로 만듦

        $$\begin{aligned}
        \begin{pmatrix} 4&2 \\ 2&1 \end{pmatrix} \begin{pmatrix} 3 \\ 1 \end{pmatrix}
        = \begin{pmatrix} 10 \\ 5 \end{pmatrix}
        \end{aligned}$$

- **해석**
    - $n \times n$ 정방행렬에 대하여 그 행렬식이 $0$ 이 아닌 경우 그 역행렬이 존재함
    - $n \times n$ 정방행렬에 대하여 그 행렬식이 $0$ 이 아닌 경우 그 계수는 $n$ 임
    - $n \times n$ 정방행렬에 대하여 그 행렬식이 $0$ 이 아닌 경우 이를 구성하는 구성하는 모든 벡터는 선형 독립임
    - $n \times n$ 정방행렬에 대하여 그 행렬식이 $0$ 이 아닌 경우 이를 구성하는 구성하는 모든 벡터를 $span$ 하여 $n$ 차원 공간을 구성할 수 있음

- **성질**
    - $det(\alpha)=\alpha$
    - $det(I)=1$
    - $det(A)=det(A^T)$
    - $det(A^{-1})=det(A)^{-1}$
    - $det(AB)=det(A) \times det(B)$
    - $det(\alpha \times A_n)=\alpha^n \times det(A_n)$
    - $\begin{vmatrix} \cdots & \overrightarrow{a_i} \cdots \overrightarrow{a_j} \end{vmatrix}=-\begin{vmatrix} \cdots & \overrightarrow{a_j} \cdots \overrightarrow{a_i} \end{vmatrix}$
    - $\begin{vmatrix}\alpha \times a & \alpha \times b \\ c & d\end{vmatrix} = \alpha \times \begin{vmatrix}a&b\\ c&d\end{vmatrix}$

- **계산 방법**
    - $det(A_2)=a_{11}a_{22}-a_{12}a_{21}$
    - 삼각행렬에 대하여 그 행렬식은 대각항 원소들의 곱으로 구할 수 있음
    - $3\times 3$ 이상의 정방행렬에 대하여 그 행렬식은 **가우스-조르단 소거법(Gaussian Elimination)**으로 구함
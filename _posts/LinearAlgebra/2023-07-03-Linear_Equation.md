## Index

1. 선형방정식
2. 선형방정식의 갯수와 미지수의 갯수가 같은 경우
3. 선형방정식의 갯수보다 미지수의 갯수가 더 많은 경우
4. 미지수의 갯수보다 선형방정식의 갯수가 더 많은 경우

<hr></br>

## 선형방정식

- **선형방정식(Linear Equation)** : 최고차 항의 차수가 $1$ 을 넘지 않는 다항방정식으로서 $1$ 차 방정식

    $$\begin{aligned}
    & a_1x_1 + a_2x_2 + \cdots + a_nx_n
    = b
    \end{aligned}$$
    
    - **선형방정식의 벡터화**

        $$\begin{aligned}
        \begin{pmatrix}
        a_1&a_2&\cdots&a_n
        \end{pmatrix}

        \begin{pmatrix}
        x_1\\
        x_2\\
        \vdots\\
        x_n
        \end{pmatrix}
        = b
        \end{aligned}$$

    - **이때 벡터 $\overrightarrow{a}$ 는 방정식의 계수들을 나열하고 있음**

        $$\begin{aligned}
        \overrightarrow{a}^T \overrightarrow{x}
        = b
        \end{aligned}$$

- **선형연립방정식(Linear System)** : 둘 이상의 선형방정식의 집합

    $$\begin{aligned}
    \begin{matrix}
    a_{11}x_1 & + & a_{12}x_2 & + & \cdots & + & a_{1n}x_n & = & b_1 \\
    a_{21}x_1 & + & a_{22}x_2 & + & \cdots & + & a_{2n}x_n & = & b_2 \\
    \vdots & + & \vdots & + & \ddots & + & \vdots & = & \vdots \\
    a_{m1}x_1 & + & a_{m2}x_2 & + & \cdots & + & a_{mn}x_n & = & b_m
    \end{matrix}
    \end{aligned}$$

    - **선형연립방정식의 행렬화**

        $$\begin{aligned}
        \begin{pmatrix}
        a_{11}&a_{12}&\cdots&a_{1n}\\
        a_{21}&a_{22}&\cdots&a_{2n}\\
        \vdots&\vdots&\ddots&\vdots\\
        a_{m1}&a_{m2}&\cdots&a_{mn}
        \end{pmatrix}

        \begin{pmatrix}
        x_1\\
        x_2\\
        \vdots\\
        x_n
        \end{pmatrix}
        
        &=
        \begin{pmatrix}
        b_1\\
        b_2\\
        \vdots\\
        b_m
        \end{pmatrix}
        \end{aligned}$$

    - **첨가 행렬(Augmented Matrix)** : 선형연립방정식 계수들의 집합으로서 벡터 $\overrightarrow{x}$ 를 선형변환하는 행렬

        $$\begin{aligned}
        A \overrightarrow{x}
        &= \overrightarrow{b}
        \end{aligned}$$

        - 첨가 행렬 $A$ 의 열벡터 $\overrightarrow{a_1}, \overrightarrow{a_2}, \cdots, \overrightarrow{a_n}$ 을 구분하여 표현할 수 있음

            $$\begin{aligned}
            \overrightarrow{a_1} x_1 + \overrightarrow{a_2} x_2 + \cdots + \overrightarrow{a_n} x_n
            &= \overrightarrow{b}
            \end{aligned}$$

</br>

## 선형방정식의 갯수와 미지수의 갯수가 같은 경우

- **첨가 행렬의 역행렬과 방정식의 해**

    $$\begin{aligned}
    \begin{pmatrix}
    a_{11}&a_{12}\\
    a_{21}&a_{22}
    \end{pmatrix}
    \begin{pmatrix}
    x_1\\
    x_2
    \end{pmatrix}
    =
    \begin{pmatrix}
    b_1\\
    b_2
    \end{pmatrix}
    \Leftrightarrow A \overrightarrow{x} = \overrightarrow{b}
    \end{aligned}$$

    - **크기가 $n \times n$ 인 첨가 행렬 $A$ 에 대하여 그 역행렬 $A^{-1}$ 이 존재할 조건**

        - $Rank(A_n)=n$
        - $det(A) \ne 0$
        - $A$ 의 열벡터 $\overrightarrow{a_1}, \overrightarrow{a_2}, \cdots, \overrightarrow{a_n}$ 를 $span$ 하여 $n$ 차원 공간을 구성할 수 없음
        - $A$ 의 열벡터 $\overrightarrow{a_1}, \overrightarrow{a_2}, \cdots, \overrightarrow{a_n}$ 는 모두 선형 독립임

    - **첨가 행렬 $A$ 에 대하여 그 역행렬이 존재하면 단 하나의 해가 존재함**

        <p align="center"><img alt="해가존재하는경우(1)" src="https://github.com/jayarnim/jayarnim/assets/116495744/621fd8a4-db8e-4868-b199-eba7410a8513" width=80%></p>

    - **첨가 행렬 $A$ 에 대하여 그 역행렬이 존재하지 않으면 불능이거나 부정임**
        - **불능(Underdetermined)** : 해를 구할 수 없음

            <p align="center"><img alt="해가존재하지않는경우(1)" src="https://github.com/jayarnim/jayarnim/assets/116495744/26977e0b-42ba-411d-8661-8f1b94853d7f" width=80%></p>

        - **부정(Inconsistent, Impossible)** : 해가 무수히 많아 하나로 정할 수 없음

            <p align="center"><img alt="해가무수히많이존재하는경우(1)" src="https://github.com/jayarnim/jayarnim/assets/116495744/f68bbb6f-4a77-4b1f-853f-9171f58e7d4f" width=80%></p>

- **해가 하나 존재하는 경우의 기하학적 이해**

    <p align="center"><img alt="해가존재하는경우(2)" src="https://github.com/jayarnim/jayarnim/assets/116495744/70a61509-be66-4e5f-b25f-97bc51c39924" width=80%></p>

    $$
    \begin{pmatrix}
    7&2\\
    -7&5
    \end{pmatrix}
    \begin{pmatrix}
    x_1\\
    x_2
    \end{pmatrix}
    =
    \begin{pmatrix}
    -5\\
    12
    \end{pmatrix}
    \Leftrightarrow
    \overrightarrow{a_1}x_1
    + \overrightarrow{a_2}x_2
    = \overrightarrow{b}
    $$
    
    $$
    \overrightarrow{a_1}
    = \begin{pmatrix}
    7\\
    -7
    \end{pmatrix},
    \overrightarrow{a_2}
    = \begin{pmatrix}
    2\\
    5
    \end{pmatrix},
    \overrightarrow{b}
    = \begin{pmatrix}
    -5\\
    12
    \end{pmatrix}
    $$

    - **$\overrightarrow{a_1}, \overrightarrow{a_2}$ 를 $span$ 하여 $2$ 차원 평면을 구성할 수 있음**
        - $\overrightarrow{a_1}$ 와 $\overrightarrow{a_2}$ 는 선형 독립임

    - **$\overrightarrow{a_1}, \overrightarrow{a_2}$ 가 $span$ 하여 구성할 수 있는 $2$ 차원 평면에 $\overrightarrow{b}$ 가 포함됨**

    - **$\overrightarrow{a_1}, \overrightarrow{a_2}$ 를 선형결합하여 $\overrightarrow{b}$ 를 만들 수 있음**
        - $\overrightarrow{b}$ 는 $\overrightarrow{a_1}, \overrightarrow{a_2}$ 에 대하여 선형 종속임

- **해를 구할 수 없는 경우의 이해**

    <p align="center"><img alt="해가존재하지않는경우(2)" src="https://github.com/jayarnim/jayarnim/assets/116495744/c466e0d2-abfe-433c-9c08-95af0b05946c" width=80%></p>

    $$
    \begin{pmatrix}
    5&5\\
    5&5
    \end{pmatrix}
    \begin{pmatrix}
    x_1\\
    x_2
    \end{pmatrix}
    =
    \begin{pmatrix}
    10\\
    20
    \end{pmatrix}
    \Leftrightarrow
    \overrightarrow{a_1}x_1
    + \overrightarrow{a_2}x_2
    = \overrightarrow{b}
    $$
    
    $$
    \overrightarrow{a_1}
    = \begin{pmatrix}
    5\\
    5
    \end{pmatrix},
    \overrightarrow{a_2}
    = \begin{pmatrix}
    5\\
    5
    \end{pmatrix},
    \overrightarrow{b}
    = \begin{pmatrix}
    10\\
    20
    \end{pmatrix}
    $$

    - **$\overrightarrow{a_1}, \overrightarrow{a_2}$ 를 $span$ 하여 $2$ 차원 평면을 구성할 수 없음**
        - $\overrightarrow{a_1}$ 와 $\overrightarrow{a_2}$ 는 선형 종속임

    - **$\overrightarrow{a_1}, \overrightarrow{a_2}$ 가 $span$ 하여 구성할 수 있는 $1$ 차원 직선에 $\overrightarrow{b}$ 가 포함되지 않음**

    - **$\overrightarrow{a_1}, \overrightarrow{a_2}$ 를 선형결합하여 $\overrightarrow{b}$ 를 만들 수 없음**
        - $\overrightarrow{b}$ 는 $\overrightarrow{a_1}, \overrightarrow{a_2}$ 에 대하여 선형 독립임

- **해가 무수히 많은 경우의 이해**

    <p align="center"><img alt="해가무수히많이존재하는경우(2)" src="https://github.com/jayarnim/jayarnim/assets/116495744/df6f2207-d411-4772-99be-6ed543673e98" width=80%></p>

    $$
    \begin{pmatrix}
    1&1\\
    2&2
    \end{pmatrix}
    \begin{pmatrix}
    x_1\\
    x_2
    \end{pmatrix}
    =
    \begin{pmatrix}
    10\\
    20
    \end{pmatrix}
    \Leftrightarrow
    \overrightarrow{a_1}x_1
    + \overrightarrow{a_2}x_2
    = \overrightarrow{b}
    $$
    
    $$
    \overrightarrow{a_1}
    = \begin{pmatrix}
    1\\
    2
    \end{pmatrix},
    \overrightarrow{a_2}
    = \begin{pmatrix}
    1\\
    2
    \end{pmatrix},
    \overrightarrow{b}
    = \begin{pmatrix}
    10\\
    20
    \end{pmatrix}
    $$

    - **$\overrightarrow{a_1}, \overrightarrow{a_2}$ 를 $span$ 하여 $2$ 차원 평면을 구성할 수 없음**
        - $\overrightarrow{a_1}$ 와 $\overrightarrow{a_2}$ 는 선형 종속임

    - **$\overrightarrow{a_1}, \overrightarrow{a_2}$ 가 $span$ 하여 구성할 수 있는 $1$ 차원 직선에 $\overrightarrow{b}$ 가 포함됨**

    - **$\overrightarrow{a_1}, \overrightarrow{a_2}$ 를 선형결합하여 $\overrightarrow{b}$ 를 만들 수 있음**
        - $\overrightarrow{b}$ 는 $\overrightarrow{a_1}, \overrightarrow{a_2}$ 에 대하여 선형 종속임

</br>

## 선형방정식의 갯수보다 미지수의 갯수가 더 많은 경우

<p align="center"><img alt="선형방정식의갯수보다미지수갯수가더많은경우" src="https://github.com/jayarnim/jayarnim/assets/116495744/c899d00d-e42e-433b-8305-e72df82bfc2c" width=80%></p>

$$
\begin{pmatrix}
1&2&3\\
1&5&1
\end{pmatrix}
\begin{pmatrix}
x_1\\
x_2\\
x_3
\end{pmatrix}
=
\begin{pmatrix}
2\\
1
\end{pmatrix}
\Leftrightarrow
A\overrightarrow{x}
= \overrightarrow{b}
$$

- 하나의 방정식을 만족하는 벡터 $\overrightarrow{x}$ 는 $3$ 차원 공간의 $2$ 차원 평면을 구성함
- 두 방정식을 동시에 만족하는 벡터 $\overrightarrow{x}$ 는 두 평면이 교차하는 $1$ 차원 직선의 모든 점임

</br>

## 미지수의 갯수보다 선형방정식의 갯수가 더 많은 경우

<p align="center"><img alt="미지수갯수보다선형방정식의갯수가더많은경우" src="https://github.com/jayarnim/jayarnim/assets/116495744/81f7746a-eb06-4261-afe6-062bd778215b" width=80%></p>

$$
\begin{pmatrix}
0&1\\
-2&1\\
2&1\\
\end{pmatrix}
\begin{pmatrix}
x_1\\
x_2
\end{pmatrix}
=
\begin{pmatrix}
-1\\
-4\\
8
\end{pmatrix}
\Leftrightarrow
A\overrightarrow{x}
= \overrightarrow{b}
$$

- 하나의 방정식을 만족하는 벡터 $\overrightarrow{x}$ 는 $2$ 차원 평면의 $1$ 차원 직선을 구성함
- 세 방정식을 동시에 만족하는 벡터 $\overrightarrow{x}$ 는 존재하지 않음
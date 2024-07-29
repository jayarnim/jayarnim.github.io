---
order: 4
title: Partial Derivative
date: 2022-07-14
categories: [Mathematical Techs, Calculus]
tags: [Mathematics]
math: true
description: >-
  Based on the lecture “Mathematics for Artificial Intelligence (2022-1)” by Prof. Yeo Jin Chung, Dept. of AI, Big Data & Management, College of Business Administration, Kookmin Univ.
image:
  path: /_post_refer_img/Calculus/Thumbnail.jpg
---

## 편미분(Partial Derivative)
-----

- **정의** : 다변수함수 $y=f(x,\cdots)$ 에 대하여, 변수 $x$ 를 제외한 모든 변수를 일정한 상수로 고정하였을 때 $x$ 축에 평행한 방향에 대한 $y$ 의 순간변화율

    - $z$ 에 대한 $x,y$ 의 2변수함수 $f$ 를 상정하자

        $$
        z=f(x,y)
        $$

    - $y=b$ 로서 고정되어 있을 경우, $z$ 는 $x$ 만의 함수라고 볼 수 있음

        $$
        z=f(x,y=b)
        $$

    - $z$ 에 대한 $x$ 만의 함수 $f(x,y=b)$ 가 $x=a$ 에서 미분 가능하다고 하자

        $$\begin{aligned}
        \frac{\partial}{\partial x}f(a,b)
        &= \lim_{h\rightarrow 0}\frac{f(a+h,b)-f(a,b)}{h}
        \end{aligned}$$

    - $(a,b)$ 에서 $x$ 에 관한 **편미분계수(Partial Derivatial)** 를 다음과 같이 표현함

        $$\begin{aligned}
        D_{x}f(x=a,y=b)
        &=f_{x}(x=a,y=b)\\
        &=\frac{\partial}{\partial x} f(x=a,y=b)\\
        &=\frac{\partial z}{\partial x}
        \end{aligned}$$

- **예시**
    - $\text{temperature} = T(x, time)$

        ![01](/_post_refer_img/Calculus/04-01.png){: width="100%"}

    - $\text{temperature} = T(x,time=3)$

        ![02](/_post_refer_img/Calculus/04-02.png){: width="100%"}

    - $\text{temperature} = T(x) \\ (\text{s.t.} \, time=3)$

        ![03](/_post_refer_img/Calculus/04-03.png){: width="100%"}

    - $\displaystyle\frac{d}{dx}T(x,time=3)$

        ![04](/_post_refer_img/Calculus/04-04.png){: width="100%"}

- **고계편도함수** : 다변수함수에 대하여 그 편도함수의 편도함수
    - $z$ 에 대한 $x,y$ 의 2변수함수 $f$ 를 상정하자

        $$
        z=f(x,y)
        $$

    - $f$ 의 $x,y$ 에 대한 1계편도함수는 다음과 같음

        $$
        f_{x}(x,y) = \frac{\partial}{\partial x}f(x,y)\\
        f_{y}(x,y) = \frac{\partial}{\partial y}f(x,y)
        $$

    - 1계편도함수의 $x,y$ 에 대한 편도함수는 다음과 같음

        $$\begin{aligned}
        f_{xx}(x,y)
        &= (f_{x})_{x}\\
        &= \frac{\partial^2}{\partial x^2}f(x,y)\\\\
        f_{xy}(x,y)
        &= (f_{x})_{y}\\
        &= \frac{\partial^2}{\partial y \partial x}f(x,y)\\\\
        f_{yx}(x,y)
        &= (f_{y})_{x}\\
        &= \frac{\partial^2}{\partial x \partial y}f(x,y)\\\\
        f_{yy}(x,y)
        &= (f_{y})_{y}\\
        &= \frac{\partial^2}{\partial y^2}f(x,y)
        \end{aligned}$$

## 2변수함수의 극값
-----

- **2변수함수의 그래프**

    ![05](/_post_refer_img/Calculus/04-05.png){: width="100%"}

    - 2변수함수 $z=f(x,y)$ 의 그래프 $\{(x,y,f(x,y)) \vert (x,y)\in D(f)\}$ 는 $xyz$-공간에서의 곡면임

- **2변수함수의 임계점**
    - **임계점(Critical Point)** : 함수의 1계편도함수 값이 $0$ 이거나 존재하지 않는 지점

        $$
        f_x = f_y = 0
        $$

    - **극점(Local Extremum Point)** : 임계점 중에서 극값을 갖는 지점

        ![06](/_post_refer_img/Calculus/04-06.png){: width="100%"}

        - $f$ 의 임계점 $(a,b)$ 의 모든 열린 근방 $(x,y)$ 에 대하여 다음 중 **하나만을** 만족하는 경우
            - **극대점** : $f(a,b) \leq f(x,y)$
            - **극소점** : $f(a,b) \ge f(x,y)$

        - 이는 $x,y$ 에 대한 이계편도함수가 다음을 만족함을 의미함

            $$
            f_{xx} \cdot f_{yy} - f^{2}_{xy} > 0
            $$

    - **안장점(Saddle Point)** : 임계점 중에서 극값을 갖지 않는 점으로서, 어떤 측면에서는 극소값이 되고, 동시에 다른 측면에서는 극대값이 되는 지점

        ![07](/_post_refer_img/Calculus/04-07.png){: width="100%"}

        - $f$ 의 임계점 $(a,b)$ 의 모든 열린 근방 $(x,y)$ 에 대하여 다음을 **동시에** 만족하는 경우
            - $f(a,b) \leq f(x,y)$
            - $f(a,b) \ge f(x,y)$

        - 이는 $x,y$ 에 대한 이계편도함수가 다음을 만족함을 의미함

            $$
            f_{xx} \cdot f_{yy} - f^{2}_{xy} < 0
            $$

- **헤시안 행렬의 행렬식을 활용한 2변수함수의 극값 판별**
    - **헤시안 행렬(Hessian Matrix)** : 어떤 이변수함수의 이계편도함수를 표현한 행렬

        $$
        \begin{pmatrix}
        f_{xx}&f_{xy}\\
        f_{xy}&f_{yy}\\ 
        \end{pmatrix}
        $$

    - **헤시안 행렬의 행렬식($D$)**

        $$\begin{aligned}
        D
        &=f_{xx} \cdot f_{yy} - f^{2}_{xy}\\
        &=\begin{vmatrix}
        f_{xx}&f_{xy}\\
        f_{xy}&f_{yy}\\ 
        \end{vmatrix}
        \end{aligned}$$

    - **헤시안 행렬의 행렬식을 활용한 2변수함수의 극값 판별**
        - $f_x=f_y=0$ 인 점 $(a,b)$ 의 근방에서 함수 $f$ 와 그 일계편도함수가 모두 연속이라고 하자
            - $D=0$ : 극값의 존재 여부를 결정할 수 없음
            - $D<0$ : $f$ 는 $(a,b)$ 에서 안장점을 가짐
            - $D>0$ : $f$ 는 $(a,b)$ 에서 극값을 가짐
                - $f_{xx} < 0$ : 극대값
                - $f_{xx} > 0$ : 극소값

## 그라디언트(Gradient)
-----

- **정의** : $n$ 변수함수 $y=f(x_{1},x_{2},\cdots,x_{n})$ 에 대하여 각 변수에 대한 일계편도함수로 구성된 벡터

    $$
    \nabla f
    =(\frac{\partial f}{\partial x_{1}}, \frac{\partial f}{\partial x_{2}}, \cdots, \frac{\partial f}{\partial x_{n}})^{T}
    $$

- **해석** : $$\nabla f \vert _{(x_{1},x_{2},\cdots,x_{n})}$$ 는 점 $$(x_{1},x_{2},\cdots,x_{n})$$ 에서 $$f$$ 의 값이 가장 가파르게 증가하는 방향임

    ![08](/_post_refer_img/Calculus/04-08.png){: width="100%"}
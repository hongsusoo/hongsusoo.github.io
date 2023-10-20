---
defaults:
  - scope:
      path: ""
      type: posts
    values:
      layout: single
      author_profile: true
      comments: true
      share: true
      related: true

title: "[선형대수] 고윳값 분해 "
excerpt: "about : 선형대수"
toc: true
toc_sticky: true
toc_label: "Label"
categories: 
  - Linear Algebra
tags:
  - [선형대수]
date: 2021-12-05
last_modified_at: 2021-12-05
---

<br>

# 고유값 분해

- 행렬의 내부 구조를 파악하기 위한 방법

## 고유값과 고유벡터

- 정방 행렬 $A$에 대해 $Av = \lambda v$를 만족하는 영벡터가 아닌 벡터 $v$, 실수 $\lambda$가 존재한다 가정하면
- 실수 $\lambda$를 **고윳값(eigenvalue)**, 벡터 $v$를 **고유벡터(eigenvector)** 라고 함
- 이런 고윳값과 고유벡터를 찾는 작업을 **고유분해(eigen-decomposition)** 또는 **고윳값 분해(eigenvalue decomposition)** 라고 함

## 의미

- 행렬 A의 고유벡터는 행렬 A를 곱해서 변환해도 방향이 바뀌지 않음
- 고유값은 변환된 고유벡터와 원래 고유벡터의 크기 비율
- 추가 설명 : 행렬 A는 어떤 선형변환을 할 수 있는 행렬이다. 하지만, 고유벡터가 곱해질 경우 방향을 바꾸지 못하는 성질이 있다. 따라서 어떤 임의의 벡터에 배수를 곱한 값과 A로 선형변환한 값이 동일해지는 영벡터가 아닌 $v$가 존재할때, $v$를 행렬 $A$의 공유벡터라 정의한다.

![image](https://user-images.githubusercontent.com/77658029/144732173-97f1cea4-f93a-465d-9953-57737daccc8d.png)

## 특성방정식(Characteristic Equation)

- 행렬만 주어졌을때 고윳값과 고유벡터를 구하기 위한 방정식
- 
- 식 : $det(A-\lambda I) = 0$ (역행렬이 존재하지 않는 조건)
- 위 식이 영이 아니라면 역행렬이 존재하기 때문에 고유벡터 $v$는 항상 영벡터가 되기 때문에 행렬식이 0이 되도록 사용($(A - \lambda I)^{-1}(A - \lambda I)v = 0 \rightarrow v=0$)

### 특성방정식 예제

- 방정식의 해를 찾으면 되는데, 항상 실수값을 갖지는 않음
- 중복고윳값(repeated eigenvalue)나 복소수 고윳값이 나오게 될 수 있음

![image](https://user-images.githubusercontent.com/77658029/144732749-26cee4fb-92dc-4235-bf30-45e582ce4e45.png)


## 고윳값의 개수

- 정리 : 중복된 고윳값을 각각 별개로 생각하고 복소수인 고윳값도 고려한다면 N차원 정방행렬의 고윳값은 항상 N개다.


## Numpy를 활용한 고유 분해

### 고윳값이 실수일 경우

**📰code**
```python
import numpy as np

A = np.array([[2,3],[2,1]])
w,V = np.linalg.eig(A)

print("고윳값 :",w)
print("고유벡터 :",V)

print("Av=λv :")
print("Av =",A@V) #행렬곱
print("λv =",w*V) #스칼라곱
```
**🔍result**
```python
고윳값 : [ 4. -1.]
고유벡터 : [[ 0.83205029 -0.70710678]
            [ 0.5547002   0.70710678]]
Av=λv :
Av = [[ 3.32820118  0.70710678]
      [ 2.21880078 -0.70710678]]
λv = [[ 3.32820118  0.70710678]
      [ 2.21880078 -0.70710678]]
```

### 고윳값이 허수일 경우

**📰code**
```python
import numpy as np

A = np.array([[0,-1],[1,0]])
w,V = np.linalg.eig(A)

print("고윳값 :",w)
print("고유벡터 :",V)

print("Av=λv :")
print("Av =",A@V) #행렬곱
print("λv =",w*V) #스칼라곱
```
**🔍result**
```python
고윳값 : [0.+1.j 0.-1.j]
고유벡터 : [[0.70710678+0.j 0.70710678-0.j]
             [0.-0.70710678j 0.+0.70710678j]]
Av=λv :
Av = [[0.+0.70710678j 0.-0.70710678j]
      [0.70710678+0.j 0.70710678+0.j]]
λv =  [[0.+0.70710678j 0.-0.70710678j]
      [0.70710678+0.j 0.70710678+0.j]]
```

## 대각화(Diagonalization)

- N차원의 정방행렬 A가 N개의 복소수 고윳값과 이에 대응하는 고유벡터를 가지게 되는데, 이때 대응하는 고윳값과 고유벡터를 정의하고, 

$\lambda_1, \lambda_2, \cdots, \lambda_N \;\;\; v_1, v_2, \cdots, v_N$

- 고유벡터행렬 $V = \left[ v_1 \cdots v_N \right]$
- 고윳값행렬 $\Lambda =
            \begin{bmatrix}
            \lambda_{1} & 0 & \cdots & 0 \\
            0 & \lambda_{2} & \cdots & 0 \\
            \vdots & \vdots & \ddots & \vdots \\
            0 & 0 & \cdots & \lambda_{N} \\
            \end{bmatrix}$
- 행렬$A$와 고유벡터행렬 $V$의 곱은 고유벡터행렬 $V$과 고윳값행렬 $\Lambda$의 곱과 같음

![image](https://user-images.githubusercontent.com/77658029/144733574-954dd71e-e234-453b-a6bc-0485e8b30762.png)

> **만약 고유벡터 행렬$V$의 역행렬이 존재한다면,** 행렬을 다음과 같이 고유벡터행렬과 고윳값행렬의곱으로 표현할 수 있음, 이런 작업을 **대각화(Diagonalization)** 라고 함($A = V \Lambda V^{-1}$)

### 대각화가능 여부

> 고유벡터가 선형독립이면 대각화 가능함

- $A = V \Lambda V^{-1}$ 식에서 $V^{-1}$가 존재하기 위해서는 고유벡터행렬이 역행렬을 가져야하고, 역행렬을 갖기 위해서는 정방행렬의 모든 열벡터가 선형독립이어야 함

### 고윳값과 역행렬

> 대각화 가능한 행렬에 0인 고윳값이 없으면 항상 역행렬이 존재함

- $A^{-1} = (V\Lambda V^{-1})^{-1} = V \Lambda^{-1} V^{-1}$

## 대칭행렬의 고유분해

> 행렬 $A$가 실수인 대칭행렬이면, 고윳값이 실수이고, 고유벡터는 서로 직교함

- 만약 고유벡터들이 크기가 1이 되도록 정규화된 상태면, 고유벡터행렬 $V$는 정규직교 행렬이므로 전치행렬의 역행렬임

$^T V = V V^T = I$

$V^{-1} = V^T$

> 실수인 대칭행렬은 항상 대각화 가능함

### 대칭행렬 고유분해 증명

>"실수 대칭핼렬의 고윳값과 고유벡터는 모두 실수값이고, 
또한 서로 다른 고윳값에 해당하는 고유벡터는 서로 직각이다."

만약 $A = A^T \in R^{n\times n}$ 인 경우

$Av = \lambda v \tag{1}$

위 식의 켤레복소수를 확인하면

$\bar{A}\bar{v} = \bar{\lambda} \bar{v} \tag{2}$

여기서 $A$는 실수 이기 때문에 $A = \bar{A}$이므로

$A\bar{v} = \bar{\lambda} \bar{v} \tag{3}$ 

(※ A가 실수 행렬이면, 고윳값과 고유벡터의 켤레값도 고윳값, 고유벡터가 됨을 확인할 수 있음)

$A = A^T$이기 떄문에 양변에 전치(Transpose)하면

$\bar{v}^T A = \bar{\lambda} \bar{v}^T \tag{4}$

식 (1)의 양변에 $\bar{v}^T$를 곱하면,

$\bar{v}^TAv = \lambda \bar{v}^Tv \tag{5}$

식 (4)의 양변에 $v$를 곱하면,

$\bar{v}^T Av = \bar{\lambda} \bar{v}^Tv \tag{6}$

식(5),(6)의 좌변이 같기 때문에 우변도 같다. 

$\bar{v}^TAv = \lambda \bar{v}^Tv = \bar{\lambda} \bar{v}^Tv \tag{7}$

$(\lambda-\bar{\lambda}) \bar{v}^Tv = 0 \tag{8}$

따라서,

 $\lambda = \bar{\lambda} \tag{9}$
 
이므로 고윳값은 실수인 것을 확인할 수 있음


한편, 고유값과 고유벡터의 정의에서 

$(A- \lambda I) \mathbf{v} = 0 \tag{10}$

에서 $A-\lambda I$가 실수 행렬이므로, $\lambda$에 해당하는 고유벡터 v도 실수벡터가 되어야 한다. 

고윳값 $\lambda$에 해당하는 고유벡터를 $v$, 고유값 $\mu$에 해당하는 고유벡터를 $w$라고 정의하면

$\begin{align} A v &= \lambda v \\ A w &= \mu w \end{align} \tag{11}$

위 식의 양변에 각각 $w^T$와 $v^T$를 곱하면 다음과 같다

$\begin{align} w^T A v &= \lambda w^T v \\ v^T A w &= \mu v^T w \end{align} \tag{12}$

위 두 식은 모두 **스칼라**이고, $A = A^T$ 이므로 두 개의 식은 같다.

$\begin{align} v^T A w &= (v^T A w)^T \\ &= w^T A^T v \\ &= w^T A v \end{align} \tag{13}$

(12)식에 대입하면,

$(\lambda - \mu ) w^T v= 0 \tag{14}$

만약, $\lambda$, $\mu$가 서로 다른 값을 갖는다면(서로 다른 고윳값을 가진다면), 

$w^T v= 0 \tag{15}$

이기 때문에, 고유벡터는 서로 직각이다.


### 대칭행렬을 Rank-1 행렬의 합으로 분해

- N차원 대칭행렬 A는 다음처럼 N개의 Rank-1 행렬 $A_i = v_i v^{T}_{t}$의 합으로 표시 가능함

![image](https://user-images.githubusercontent.com/77658029/144735869-6e0b138c-38f8-4ad7-a50a-36b0cedf19bf.png)
![image](https://user-images.githubusercontent.com/77658029/144735880-f4ec1811-dcae-4b47-9689-be7548e62e8c.png)


**📰code**
```python
import numpy as np

A = np.array([[60., 30., 20.],
              [30., 20., 15.],
              [20., 15., 12.]])

w, V = np.linalg.eig(A)
w1, w2, w3 = w
v1 = V[:, 0:1]
v2 = V[:, 1:2]
v3 = V[:, 2:3]
A1 = w1 * v1 @ v1.T
A2 = w2 * v2 @ v2.T
A3 = w3 * v3 @ v3.T

print("A = λ1v1v1^T + λ2v2v2^T + λ3v3v3^T =")
print(A1+A2+A3)
```
**🔍result**
```python
A = λ1v1v1^T + λ2v2v2^T + λ3v3v3^T =
[[60. 30. 20.]
 [30. 20. 15.]
 [20. 15. 12.]]
```

### 대칭행렬의 고윳값 부호

- 대칭행렬이 위와 같이 Rank-1 행렬의 합으로 표시되고, 고유벡터가 서로 직교한다는 성질을 이용하면

> 대칭행렬이 양의 정부호(positive definite)(0 미포함)이면 고윳값은 모두 양수이다. 역도 성립한다. 

> 대칭행렬이 양의 준정부호(positive semideifinite)(0을 포함)이면 고윳값은 모두 0이거나 양수다. 역도 성립한다.


## 분산행렬(Scatter Matrix)

> 분산행렬은 양의 준정부호이고 고윳값은 0보다 같거나 크다.

> 행렬 $X ∈ R^{N×M}(N≥M)$가 풀랭크이면 이 행렬의 분산행렬 $X^TX$의 역행렬이 존재한다.

행렬 $X$가 풀랭크이면 $X$의 열벡터가 기저벡터를 이루기 때문에 영벡터가 아닌 모든 벡터 $v$에 대해 $Xv = u$는 영벡터가 될 수 없다. 


**📌reference**
- [Datascienceschool](https://datascienceschool.net/02%20mathematics/03.03%20%EA%B3%A0%EC%9C%B3%EA%B0%92%20%EB%B6%84%ED%95%B4.html)
- [대칭행렬 고유분해 증명](https://pasus.tistory.com/9)
<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

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

title: "[선형대수] 행렬(matrix) 기초"
excerpt: "about : 선형대수"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  Linear Algebra
tags:
  - 
date: 2021-08-02
last_modified_at: 2021-08-02
---
<br>

# 행렬

- 벡터를 원소로 가지는 2차원 배열

![image](https://user-images.githubusercontent.com/77658029/127812785-c6baec0f-8c23-46a3-ab69-c7e9ddbad21b.png)

## 행렬에 대한 이해1

- 벡터는 한 점을 나타내는데, 그 데이터의 모임이 행렬


## 구성

- 행렬(n x m 행렬)
- n개의 행벡터
- 각 벡터는 m개의 원소를 가짐

![image](https://user-images.githubusercontent.com/77658029/127812825-8fd0eb7d-83aa-48c3-a6d0-78bd8c6746ea.png)

## 전치행렬(transpose matrix)

- $x_{ij} ↔ x_{ji}$로 행과 열을 바꿔주는 연산
- $n x m$ 행렬을 전치하면 $m x n$ 행렬이됨

## 스칼라곱

- 벡터의 스칼라곱과 동일하게 행렬의 모든 벡터의 길이를 조정함
- 계산은 상수값이 모든 원소들에 곱해짐

## 덧셈, 뺄셈

- 벡터의 덧셈과 동일한 모양을 가지면 두 행렬를 더 하거나 뺄 수 있음
- 동일 위치의 성분끼리 연산이됨

## 성분곱

- 벡터의 성분곱과 동일하게 동일한 위치의 성분들끼리 곱해짐
- ⨀ 기호로 표현함

## 곱셈

- 앞에있는 행렬의 행벡터와 뒤에 있는 행렬의 열벡터의 내적으로 구할 수 있음
- @ 연산을 사용함
- 행렬의 곱셈은 교환법칙이 성립하지 않음


![image](https://user-images.githubusercontent.com/77658029/127814292-d75b9a40-7c84-4464-b096-524633edb7bd.png)


## 내적

- numpy에서의 np.inner는 행렬의 내적을 계산해줌
- 앞에있는 행렬의 행벡터와 뒤에 있는 행렬의 행벡터의 내적으로 계산됨
- 뒤에 행렬을 전치하여 계산하면 행렬의 곱과 동일해짐

**📰code**
```python
import numpy as np

x=np.array(np.arange(9).reshape(3,3))
y=np.array(np.arange(9).reshape(3,3), dtype=int)

x@(y.T),np.inner(x,y)
```
**🔍result**
```
(array([[  5,  14,  23],
        [ 14,  50,  86],
        [ 23,  86, 149]]),
 array([[  5,  14,  23],
        [ 14,  50,  86],
        [ 23,  86, 149]]))
```

## 행렬에 대한 이해 2

- 행렬은 벡터공간에서 사용되는 연산자(operator) 역할을 함
- 다른 차원으로 매칭 시켜줄 수 있음
- 행렬곱을 통해 패턴을 추출하고, 데이터 압축이 가능함

## 항등행렬

- 임의의 행렬이 항등행렬을 곱했을때, 행렬이 그대로 나오게 하는 행렬
- I로 통용됨

![image](https://user-images.githubusercontent.com/77658029/127817286-c5ee4394-2430-4643-ac96-bf5553f1a9d0.png)

## 역행렬(inverse matrix)

- 어떤 행렬 A의 연산을 거꾸로 되돌리는 행렬
- 한 행렬과 그 행렬의 역행렬을 곱하면 항등행렬이 나옴
- 행과 열의 차원이 같고 행렬식(determinant)이 0이 아닌경우에만 계산 가능함
- `np.linalg.inv(x)` 함수를 사용하여 구할 수 있음
- $A$의 역행렬은 $A^{-1}$로 표기함

![image](https://user-images.githubusercontent.com/77658029/127816923-2d3c74c3-078a-4882-a59b-c4fbaf808b4f.png)

## 유사역행렬(pseudo-inverse)

- 무어펜로즈(Moore-penrose) 역행렬이라고도 불림
- $A$의 무어펜로즈 역행렬은 $A^{+}$로 표기함
- n, m의 차원 크기에 따라서 구하는 식이 달라짐

💡 $A^TA$ 혹은 $AA^T$의 차원은 nxn or mxm 이 되는데 이 값이 작아는 방향으로 선택한다고 생각하면 쉬움

💡 $(A^TA)^{-1}$을 풀어쓰면 $A^{-1}(A^T)^{-1}$이 되기 때문에 $(A^T)^{-1}$랑 붙는 쪽에 $A^T$가 오면 $A^{-1}$만 남게된다고 생각하면 쉬움

![image](https://user-images.githubusercontent.com/77658029/127817388-2c3dbc56-e7e5-47ab-964f-a47b17f28dcd.png)

**📰code**
```python
import numpy as np

x=np.array(np.arange(8).reshape(4,2)) # n>m
y=np.array(np.arange(8).reshape(2,4)) # n<m

A=np.linalg.inv(x.T@x)@(x.T)  # n>m
B=y.T@(np.linalg.inv(y@y.T))  # n<m

print(A@x)
print(y@B)
```
**🔍result**
```
[[ 1.00000000e+00 -6.66133815e-15]
 [-3.99680289e-15  1.00000000e+00]]
[[ 1.00000000e+00  1.11022302e-16]
 [-8.88178420e-16  1.00000000e+00]]
```

## 행렬을 통한 선형회귀

- 대부분의 데이터는 변수의 수보다 데이터의 수가 많기 때문에 정확한 답을 구할 수 없음
- 예를 들면, 한 직선에 없는 3개의 점을 찍었을때, 그 세 점을 만족하는 직선을 그을 수 없기 때문(조금은 말장난 같지만..)
- 그러면 우리는 그 세 점 근처를 지나는 직선을 그을 수 있는데 이게 선형회귀로 볼 수 있음
- $X\beta = \hat y$ 일때, 우리는 X의 무어펜로즈 역행렬을 양변에 곱해서 $/beta$를 구할 수 있는데
- 이거는 하나의 기울기라고 생각할 수 있음(상수항 b을 포함한 기울기임)

📌 유사역행렬(의사역행렬, 무어펜로즈)의 선형회귀에 대한 자세한 설명 : [공돌이의 수학정리노트](https://angeloyeo.github.io/2020/11/11/pseudo_inverse.html)

**📰code**
```python
import numpy as np
from sklearn.linear_model import LinearRegression

## data_set
X= np.array([[1,1],[1,2],[2,2],[2,3]]) 
y= np.dot(X,np.array([1,2]))+3
x_test = np.array([[1,0],[1,2],[2,2],[2,2]]) 

# linear Regression in sklearn
model = LinearRegression()
model.fit(X,y)
y_test = model.predict(x_test)

# moore-penrose
x_expand=np.array([np.append(x,[1]) for x in X])
beta = np.linalg.pinv(x_expand) @ y
y_test_MP = np.array([np.append(x,[1]) for x in x_test]) @ beta

print(y_test)
print(y_test_MP)
```
**🔍result**
```
[4. 8. 9. 9.]
[4. 8. 9. 9.]
```

<br>

**📌reference**
- boostcourse AI tech
- [공돌이의 수학정리노트](https://angeloyeo.github.io/2020/11/11/pseudo_inverse.html)

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

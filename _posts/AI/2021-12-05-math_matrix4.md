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

title: "[선형대수] 특이값 분해"
excerpt: "about : 선형대수"
toc: true
toc_sticky: true
toc_label: "Label"
categories: 
  선형 대수
tags:
  - [선형대수]
date: 2021-12-05
last_modified_at: 2021-12-05
---

<br>

# 특이값 분해 

- 정방행렬은 고유분해로 고윳값과 고유벡터를 찾을 수 있음
- 하지만 **정방행렬이 아닌 행렬**은 **고유분해가 불가능**하여, 이를 대체한 분해 방법임


## 특이값과 특이벡터

- NxM 크기의 행렬$A$를 다음과 같은 3개의 행렬의 곱으로 나타내는 것이 **특이분해(singular decomposition)** 또는 **특이값 분해(singular value decomposition)**

    $A = U\Sigma V^T$

    1. $\Sigma \in \mathbf{R}^{N \times M}$ : 대각성분이 양수인 대각행렬, 큰 수부터 작은 수 순서로 배열
    2. $U \in \mathbf{R}^{N \times N}$ : $U$는 N차원 정방행렬로 모든 열벡터가 단위벡터이고, 서로 직교해야함
    3. $V \in \mathbf{R}^{M \times M}$ : $V$는 M차원 정방행렬로 모든 열벡터가 단위벡터이고, 서로 직교해야함
    

위 조건을 만족하는 행렬 $\Sigma$의 대각성분들을 **특이값(Singular Value)**, 행렬 $U$의 열벡터을 **왼쪽 특이벡터(Left Singular Vector)**, 행렬$V$의 행벡터들을 **오른쪽 특이벡터(Right Singular Vector)**

> 특이분해는 모든 행렬에 대해 가능하다. 즉 어떤 행렬이 주어지더라도 위와 같이 특이분해 할 수 있다. 

### 특이값 분해 행렬의 크기

- 특이값의 수는 행렬의 열과 행의 개수 중 작은 값과 같음

![image](https://user-images.githubusercontent.com/77658029/144737358-dbae1ac7-7180-4dba-88f1-8942832be797.png)

### 특이값 분해 축소형

- 특이값 대각행렬에서 0인부분은 사실상 아무런 의미가 없기 때문에, 0 원소 부분과 이에 대응하는 벡터들을 없애고 다음처럼 축소된 형태로 만들어도 마찬가지 행렬이 나옴

![image](https://user-images.githubusercontent.com/77658029/144737429-8901a596-0ed6-4d4d-9ddc-adf8d15eff15.png)

## 파이썬을 활용한 특이분해

### SVD

**📰code**
```python
import numpy as np
from numpy.linalg import svd

A = np.array([[3,-1],
             [1,3],
             [1,1]])
U,S,VT =svd(A)
U @ np.diag(S, 1)[:,1:] @ VT
```
**🔍result**
```python
array([[ 3., -1.],
       [ 1.,  3.],
       [ 1.,  1.]])
```

### 축소형 SVD
```python
import numpy as np
from numpy.linalg import svd

A = np.array([[3,-1],
             [1,3],
             [1,1]])
U,S,VT =svd(A, full_matrices=False)
U @ np.diag(S) @ VT
```
**🔍result**
```python
array([[ 3., -1.],
       [ 1.,  3.],
       [ 1.,  1.]])
```



**📌reference**
- [Datascienceschool](https://datascienceschool.net/02%20mathematics/03.03%20%EA%B3%A0%EC%9C%B3%EA%B0%92%20%EB%B6%84%ED%95%B4.html)

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

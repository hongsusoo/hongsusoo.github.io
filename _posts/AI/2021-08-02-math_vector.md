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

title: "벡터(Vector)"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - AI Math
tags:
  - 
date: 2021-08-02
last_modified_at: 2021-08-02
---
<br>

# 벡터

- 벡터는 숫자를 원소로 가지는 list 혹은 array
- 열벡터, 행벡터 두 가지가 있음

![image](https://user-images.githubusercontent.com/77658029/127809722-f7dd2ae0-c74d-489b-a42e-999e758c0aab.png)

- 원점을 기준으로한 공간상의 하나의 점을 나타냄

## 벡터의 차원

- 

## 스칼라곱

- 벡터에 일정한 상수를 곱해주는 작업
- 벡터의 길이만 변하게됨
- 0보다 작은 값을 곱해주게 될 경우 방향이 반대로 바뀜


## 벡터의 덧셈과 뺄셈

- 벡터의 차원이 동일할때 덧셉과 뺄셈이 가능함

**📰code**
```python
import numpy as np

a=np.array([1,2,3])
b=np.array([5,3,0])
a+b
```
**🔍result**
```
array([-4, -1,  3])
```

## 벡터 성분곱(Hadamard Product)

- ⨀ 기호로 사용됨

**📰code**
```python
import numpy as np

a=np.array([1,2,3])
b=np.array([5,3,0])
a*b
```
**🔍result**
```
array([5, 6, 0])
```

## 벡터의 노름(norm)

- 벡터의 norm은 **원점으로부터의 거리**
- $L_1 norm : ||X||_1$  => 변화량의 절대값을 모두 더함
- $L_2 norm : ||X||_2$  => 유클리드 거리 계산(우리가 평범하게 알고 있는 계산법)


### L1-norm 계산

- 차원의 기준 축의 절편의 크기를 모두 더한 값
- 벡터의 모든 원소에 절대값을 씌우고 더해줌

**📰code**
```python
import numpy as np

def l1_norm(x):
    x_norm = np.abs(x)
    x_norm = np.sum(x_norm)
    return x_norm

x=np.array([-1,2,3])
print(l1_norm(x))
```
**🔍result**
```
6
```

### L2-norm 계산

- 유클리드 거리를 이용한 계산
- 전체의 원소의 제곱합에 루트를 씌운 값

**📰code**
```python
import numpy as np

def l2_norm(x):
    x_norm = x*x
    x_norm = np.sum(x_norm)
    x_norm = np.sqrt(x_norm)
    return x_norm
x=np.array([1,1,0])
print(l2_norm(x))
```
**🔍result**
```
1.4142135623730951
```

### L1-norm과 L2-norm 기하학적 성질

![image](https://user-images.githubusercontent.com/77658029/127811280-b5028b87-8cfa-43bf-b911-2d62feb953ff.png)


## 두 벡터 사이의 거리 

- 두 벡터 사이의 거리를 계산할 때는 벡터의 뺄셈을 이용함
- 순서는 상관없음
- L1,L2 노름 모두 거리를 구할 수 있음


## 두 벡터 사이의 각도

- L2 노름에서만 계산이 가능함
- 제2 코사인법칙을 사용하여 구할 수 있음
- 내적으로 더 쉽게 구할 수 있음

**📰code**
```python
import numpy as np

def l2_norm(x):
    return np.sqrt(np.sum(x*x))

def findAngle(x,y):
    v=np.inner(x,y)/(l2_norm(x)*l2_norm(y))
    theta = np.arccos(v)
    return theta

x=np.array([1,0,0])
y=np.array([0,1,0])
print(findAngle(x,y)) #pi/2
```
**🔍result**
```
1.4142135623730951
```

## 벡터 내적(inner product)

- 두 벡터의 성분곱 원소들의 합으로 내적을 구할 수 있음
- `np.inner(x,y)` 함수가 있음
- 내적은 정상영(orthogonal projection)된 벡터의 길이와 관련 있음
- 두 벡터의 유사도를 측정하는데 사용함

![image](https://user-images.githubusercontent.com/77658029/127812544-4e37bc9f-918d-4398-9b84-b21d01f020f3.png)


<br>

**📌reference**
- boostcourse AI tech

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

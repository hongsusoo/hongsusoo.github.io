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

title: "[AI basic] 경사하강법(gradient descent)_순한맛"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - AI
tags:
  - [python, AI Math, gradient descent]
date: 2021-08-02
last_modified_at: 2021-08-02
---
<br>

# 경사 하강/상승법

## 미분에 대한 이해

- 미분(differentiation)은 변수의 움직임에 따른 함수값의 변화를 측정하기 위한 도구
- 최적화에서 제일 많이 사용하는 기법
- 접선의 기울기를 의미
- 한 점에서의 접선의 기울기를 알면 어느 방향으로 움직여야 증가 or 감소하는지 확인 가능함
- 저차원에서는 눈으로 확인 가능하지만, 고차원으로 갈경우 해석이 어려워지기 때문에 미분을 활용

![image](https://user-images.githubusercontent.com/77658029/127102561-466ffe3d-a63a-446e-a6cb-633b23afbc0c.png)


### 미분 모듈(sympy)

- `import sympy as sym`으로 sympy 모듈을 불러옴
- `from sympy.abc import x` 변수를 x로 지정함

```python
import sympy as sym
from sympy.abc import x

print(sym.diff(sym.poly(x**2 + 2*x + 3),x))
```
```
Poly(2𝑥+2,𝑥,𝑑𝑜𝑚𝑎𝑖𝑛=ℤ)
```

## 미분에서 경사상승법으로

- 특정 점 $x$에서 미분한값($f'(x)$)만큼 점 $x$에 더하거나 빼주는 작업을 진행
- 더 이상 변화가 없거나, 미분값이 미리 정해둔 epslion 이하가 될때까지 반복한다(극값에 도달하거나, 근처에 도착했을 경우)
- 점화식 표현 $x_n=x_{n-1}±f'(x_{n-1})$   $for f'(x_n) > ε$ (+ : 상승, - : 하강)

💡 경사상승법
![image](https://user-images.githubusercontent.com/77658029/127119457-6f18c60a-3e0a-4803-9e18-16f959fb794b.png)

💡 경사하강법
![image](https://user-images.githubusercontent.com/77658029/127120676-05df0b12-adcb-4d39-ad4f-a94003c8fa4d.png)


## 경사법 algorithm

1. 미분 계산 : gradient
2. x_init : 시작점, learning_rate : 학습률, epsilon : 종료조건
※ 학습률의 경우는 미분을 통해 업데이트 하는 속도를 조절하는데, 값을 잘못 설정하면 수렴값에 도달하지 않을 수도 있음

```python
import numpy as np
import sympy as sym
from sympy.abc import x

def gradient_ascent(func, x_init, lr=0.3,epsilon=1e-2): #경사상승법
    cnt=0
    val = x_init
    f_diff = sym.diff(func, x)
    diff = f_diff.subs(x,val)
    while np.abs(diff) > epsilon:
        val = val + lr*diff
        f_diff = sym.diff(func, x)
        diff = f_diff.subs(x,val)
        cnt += 1
#         print("연산횟수 : {}, 좌표 : ({:0.2f}, {:0.2f})".format(cnt,float(val),float(func.subs(x,val))))
    print("경사상승 - 함수 : {}, 최대점 : ({:0.2f}, {:0.2f})".format(func,val,func.subs(x,val)))

def gradient_descent(func, x_init, lr=0.3,epsilon=1e-2): #경사하강법
    cnt=0
    val = x_init
    f_diff = sym.diff(func, x)
    diff = f_diff.subs(x,val)
    while np.abs(diff) > epsilon:
        val = val - lr*diff
        f_diff = sym.diff(func, x)
        diff = f_diff.subs(x,val)
        cnt += 1
#         print("연산횟수 : {}, 좌표 : ({:0.2f}, {:0.2f})".format(cnt,float(val),float(func.subs(x,val))))
    print("경사하강 - 함수 : {}, 최소점 : ({:0.2f}, {:0.2f})".format(func,val,func.subs(x,val)))
    
gradient_ascent(func=sym.poly(-x**2), x_init=10) #경사상승법
gradient_descent(func=sym.poly(x**2), x_init=10) #경사하강법
```
```
경사상승 - 함수 : Poly(-x**2, x, domain='ZZ'), 최대점 : (0.00, -0.00)
경사하강 - 함수 : Poly(x**2, x, domain='ZZ'), 최소점 : (0.00, 0.00)
```
  
## 편미분(partial differentiation)에 대한 이해 

- 기존 미분의 경우 방향은 증가 or 감소 두 가지 방향만 가지고 있음
- 만약 벡터가 입력되는 다변수 함수의 경우는 기존 미분으로 대응이 어려움

🔑 편미분을 사용하여 문제를 해결가능!

- 편미분은 벡터로 입력되는 다변수 함수에서 한 차원을 기준으로 잡고 그 방향으로의 기울기를 구하는 작업
- 모든 차원에 대해서 기울기를 구하게 되면, 하나의 벡터를 구할 수 있는데 그 벡터를 그레디언트(gradient)라고함
- 그레디언트 벡터를 이용하여 미분과 동일하게 경사법을 이용할 수 있음

![image](https://user-images.githubusercontent.com/77658029/127163925-b2643b4e-cebe-45d0-ac23-c3507dd9af8f.png)
  $e_i$는 i번째 값만 1이고 나머지는 0인 단위벡터


## 그레디언트(gradient)

- 모든 차원에 대해서 편미분을 하여 벡터로 만든 것
- 그레디언트 벡터는 한 점에서 기울기가 증가하는 방향 벡터를 의미함
![image](https://user-images.githubusercontent.com/77658029/127168928-11e9ddf8-46d9-461a-b476-a6b497a53685.png)
- $\nabla f$로 표현함
- $\nabla$는 nabla(나블라) 혹은 del(델)이라고 읽음

💡 gradient vector direction
![image](https://user-images.githubusercontent.com/77658029/127168616-c8440173-99e1-4ff3-8834-62c20f3bd947.png)

**📌reference**
- boostcourse AI tech pre-course
- https://ko.wikipedia.org/wiki/%EA%B8%B0%EC%9A%B8%EA%B8%B0_(%EB%B2%A1%ED%84%B0)


## 경사법 algorithm(다변수 함수 gradient)

1. 미분 계산 : gradient(x,y 각 변수로 편미분하여 gradient 계산)
2. x_init : 시작점, learning_rate : 학습률, epsilon : 종료조건
※ 학습률의 경우는 미분을 통해 업데이트 하는 속도를 조절하는데, 값을 잘못 설정하면 수렴값에 도달하지 않을 수도 있음

```python
import numpy as np
import sympy as sym
from sympy.abc import x,y

def gradient_descent(func, x_init, lr=0.3,epsilon=1e-2): #경사하강법
    cnt=0
    val = x_init
    f_x_diff = sym.diff(func, x) # x로 편미분
    f_y_diff = sym.diff(func, y) # y로 편미분
    nabla_f = np.array([f_x_diff.subs(x,val[0]).subs(y,val[1]),f_y_diff.subs(x,val[0]).subs(y,val[1])], dtype = float) # grad 벡터값
    while np.linalg.norm(nabla_f) > epsilon: # grad 벡터값의 크기를 작게하자!
        val = val - lr*nabla_f # 경사하강법
        f_x_diff = sym.diff(func, x) # x로 편미분
        f_y_diff = sym.diff(func, y) # y로 편미분
        nabla_f = np.array([f_x_diff.subs(x,val[0]).subs(y,val[1]),f_y_diff.subs(x,val[0]).subs(y,val[1])], dtype = float)
        cnt += 1
        print("연산횟수 : {},최소점 : ({:0.2f}, {:0.2f}), 최소값 : {:0.2f}".format(cnt,val[0],val[1],func.subs(x,val[0]).subs(y,val[1])))
    print("경사하강 - 함수 : {}, 최소점 : ({:0.2f}, {:0.2f}), 최소값 : {:0.2f}".format(func,val[0],val[1],func.subs(x,val[0]).subs(y,val[1])))

gradient_descent(func=sym.poly(x**2+2*y**2), x_init=np.array([2,2])) #경사하강법
```
```
연산횟수 : 1,최소점 : (0.80, -0.40), 최소값 : 0.96
연산횟수 : 2,최소점 : (0.32, 0.08), 최소값 : 0.12
연산횟수 : 3,최소점 : (0.13, -0.02), 최소값 : 0.02
연산횟수 : 4,최소점 : (0.05, 0.00), 최소값 : 0.00
연산횟수 : 5,최소점 : (0.02, -0.00), 최소값 : 0.00
연산횟수 : 6,최소점 : (0.01, 0.00), 최소값 : 0.00
연산횟수 : 7,최소점 : (0.00, -0.00), 최소값 : 0.00
경사하강 - 함수 : Poly(x**2 + 2*y**2, x, y, domain='ZZ'), 최소점 : (0.00, -0.00), 최소값 : 0.00
```
**📌reference**
- boostcourse AI tech pre-course
- https://ko.wikipedia.org/wiki/%EA%B8%B0%EC%9A%B8%EA%B8%B0_(%EB%B2%A1%ED%84%B0)

<br>
```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

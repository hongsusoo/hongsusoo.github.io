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

title: "경사하강법 매운맛(gradient descent)"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - DL
tags:
  - [gradient descent]
date: 2021-08-02
last_modified_at: 2021-08-02
---
<br>

# 경사하강법을 통한 선형 회귀

- 역행렬과 무어펜로즈(Moore-penrose)역행렬을 통하여 선형회귀가 가능하지만, 선형 모델에 대해서만 적용이 가능함

**🔑 경사하강법을 통한 선형회귀**

- 선형모델을 포함하여 다른 모델도 대응이 가능함
- 역행렬을 통한 회귀법보다 더 powerful한 방법

## 선형회귀에 대한 이해 

- 많은 수의 data가 있을 경우($벡터의 수≥벡터의 길이$), 그 모든 벡터를 만족하는 해답을 구할 수 없음(일직선에 있는 경우는 제외)
- 따라서 선형회귀 모델을 이용하여 데이터들을 아우를 수 있는 최적의 식을 찾아야 함

💡 data -> 행렬식으로 표현

![image](https://user-images.githubusercontent.com/77658029/127202018-d3dff48d-4964-43e8-8b8a-dea17975253f.png)

- 찾고자 하는 최적의 식을 $X\beta = \hat Y ≈ Y$로 정의하여 $Y-\hat Y$를 최소로 만드는 $\beta$을 구해야 한다.
- 무어펜로즈 역행렬을 사용하면, 바로 최소가 되는 $\beta$을 구할 수 있지만, 사용범위가 더 넓은 경사하강법으로 트라이 해보자
- **선형회귀 목적식** $||Y-\hat Y||_2 = ||Y-X\beta||_2$가 최소가 되는 $\beta$ 구하기 위해 gradient vector를 구해보자

🔑 gradient 수식 풀이

![image](https://user-images.githubusercontent.com/77658029/127207989-1e0c5c33-21ad-42f8-9d4d-0089bc31175e.png)

- 점화식 표현 $\beta^{(t+1)} = \beta^{(t)} - \lambda\nabla_\beta||Y-X\beta^{(t)}|| = \beta^{(t)} + \frac{2\lambda}{n}X^T(y-X\beta^{(t)}$


## 선형회귀 algorithm 구현(경사하강법)

**📰code**
```python
import numpy as np

#한평면 상 -> [1,2,3]이 정답
X= np.array([[1,1],[1,2],[2,2],[2,3]]) 
y= np.dot(x,np.array([1,2]))+3

# 0,0 만 다른 평면에 있을 경우 -> [0.7333, 1.8666, 0.7333]이 정답
# X= np.array([[1,1],[1,2],[2,2],[2,3],[0,0]]) 
# y= np.array([3,5,6,8,1])
beta_gd=[10.1,15.1,-6.5] 
X_=np.array([np.append(x,[1]) for x in X])

for t in range(10000): 
    error = y - X_@beta_gd
#     error = error/np.linalg.norm(error) #이부분을 안해주면 learning_rate:0.01에 반영됨
    grad = - np.transpose(X_) @ error
    beta_gd = beta_gd - 0.01*grad
    
print(beta_gd)
```
**🔍result**
```
[1. 2. 3.]
```

## 경사하강법은 만능일까?

- 경사하강법은 결국 미분가능이 가능하고, 최소점을 구할 수 있는 볼록(convex)한 함수에 대해서는 수렴이 가능한다
- 적절한 학습률과 학습횟수를 선택했을 때 수렴이 보장됨
- 선형회귀의 경우는 목적식($||Y-X\beta||_2$)이 회귀계수$\beta$에 대해 볼록함수이기 때문에 수렴가능성이 보장된다
- 하지만 극소값이 여러개거나, 미분 불가능한 경우는 사용하지 못한다(무어펜로즈 역행렬보다는 더 많은 모델을 구축할 수 있다)
- 비선형회귀 문제의 경우 목적식이 볼록하지 않을 수 있으므로 수렴성이 항상 보장되지 않음

![image](https://user-images.githubusercontent.com/77658029/127268266-add97292-b46f-40a7-a05d-0f94e4d1a011.png)

### 경사하강법 gradient vector 계산

<br>

<a href="https://hongsusoo.github.io/categories/GradientDescent"><img src="https://img.shields.io/badge/gradient vector-수식 유도-green"/></a>


<br>

## 확률적 경사하강법(Stochastic Gradient Descent)

- 경사하강법은 non-convex함수에 대해서 최소값이 보장되지 않는다는 문제 있음
- 그걸 보완하기 위한 방법임
- 한 개 혹은 일부 데이터를 활용하여 업데이트(기존 경사하강법은 모든 데이터를 이용하여 업데이트)
- 일부 데이터를 활용하기 때문에 연산자원을 효율적으로 활용 가능함($O(d^2n) -> O(d^2b)$ : 연산량 b/n만큼 감소함)
![image](https://user-images.githubusercontent.com/77658029/127457548-7697a65a-4fbc-4485-8230-cd355c57f433.png)

- 볼록이 아닌(non-convex) 목적식은 SGD를 통해 최적화 가능함
- mini-batch는 10~1000개의 데이터를 가지고 함
- 딥러닝에서는 SGD가 실증적으로 더 낫다는 평가를 받음

![image](https://user-images.githubusercontent.com/77658029/127513594-67c3d399-52a8-41cc-97c6-a4cb95a2ca8a.png)

💡 mini-batch SGD 

![image](https://user-images.githubusercontent.com/77658029/127514342-237efeb8-6344-4358-a818-e9535045f5b4.png)
![image](https://user-images.githubusercontent.com/77658029/127514249-95da0f34-1a68-4189-9822-6a5c85596d29.png)


## 경사하강법 vs 미니배치 SGD

![image](https://user-images.githubusercontent.com/77658029/127515340-fca8d0ed-c7c3-4330-9c2f-f9ef4563bd25.png)


## 경사하강법 vs 미니배치 SGD code 비교

**📰code**
```python
import numpy as np
import sympy as sym
from sympy.abc import x,w,b #추가
from sympy.plotting import plot

train_x = (np.random.rand(1000) - 0.5) * 10
train_y = np.zeros_like(train_x)


def func(val):
    fun = sym.poly(7*x + 2)
    return fun.subs(x, val)

def l2_norm(x): #추가
    x_norm = x*x
    x_norm = np.sum(x_norm)
    x_norm = np.sqrt(x_norm)
    return x_norm    

for i in range(1000):
    train_y[i] = func(train_x[i])

# initialize
lr_rate = 1e-2
w, b = 0.0, 0.0
n_data = 1000
errors_gd = []

# 경사하강법
expand_x = np.array([np.append(x, [1]) for x in train_x])

for i in range(100):
    ## Todo
    # 예측값 y
    _y = w*train_x+b
    
    # gradient
    gradient_w = - np.transpose(expand_x)[0]@(train_y-_y)/n_data #l2_norm(train_y-_y) #값이 작어지며 learning rate를 크게 듦
    gradient_b = - np.transpose(expand_x)[1]@(train_y-_y)/n_data #l2_norm(train_y-_y) 

    # w, b update with gradient and learning rate
    w -= lr_rate * gradient_w
    b -= lr_rate * gradient_b
    
    # L2 norm과 np_sum 함수 활용해서 error 정의
    error_gd = l2_norm(train_y-_y)
    # Error graph 출력하기 위한 부분
    errors_gd.append(error_gd)

print("경사하강법 w : {} / b : {} / error : {}".format(w, b, error_gd))

# initialize
w, b = 0.0, 0.0
n_data = 10
minibatch_size = 10
errors_sgd = []

# 확률적 경사하강법
for i in range(100):
    ## Todo
    #minibatch 10
    minibatch_idx = np.random.choice(train_y.shape[0], minibatch_size, replace = True)
    minibatch_x = train_x[minibatch_idx]
    minibatch_y = train_y[minibatch_idx]
    
    # 예측값 y
    _y = w*minibatch_x +b
    
    # gradient
    gradient_w = -np.transpose(minibatch_x)@(minibatch_y-_y)/n_data    #l2_norm(minibatch_y-_y) #값이 작어지며 learning rate를 크게 듦
    gradient_b = -np.ones(10)@(minibatch_y-_y)/n_data                  #l2_norm(minibatch_y-_y)

    # w, b update with gradient and learning rate
    w = w - lr_rate*gradient_w
    b = b - lr_rate*gradient_b
    
    # L2 norm과 np_sum 함수 활용해서 error 정의
    error_sgd = l2_norm(minibatch_y-_y)
    # Error graph 출력하기 위한 부분
    errors_sgd.append(error_sgd)

print("확률적 경사하강법 w : {} / b : {} / error : {}".format(w, b, error_sgd))
```
**🔍result** 
정답은 w : 7, b : 2
```
경사하강법 w : 7.000429738930361 / b : 1.2742577531192194 / error : 23.181636293256783
확률적 경사하강법 w : 7.039753269083189 / b : 1.2571391750926415 / error : 2.2038064311604137
```

### GD vs SGD 그래프

**📰code**
```python
from IPython.display import clear_output
import matplotlib.pyplot as plt
%matplotlib inline

def plot(errors_gd,errors_sgd):
    clear_output(True)
    plt.figure(figsize=(20,5))
    plt.subplot(211)
    plt.ylabel('errors_gd')
    plt.xlabel('time step')
    plt.plot(errors_gd)
    plt.show()
    
    plt.figure(figsize=(20,5))
    plt.subplot(212)
    plt.ylabel('errors_sgd')
    plt.xlabel('time step')
    plt.plot(errors_sgd)
    plt.show()
plot(errors_gd,errors_sgd)
```
**🔍result** 
![image](https://user-images.githubusercontent.com/77658029/128598620-edeb82e4-64d0-4b49-829a-3e24af5ef3f7.png)


**📌reference**
- boostcourse AI tech
- https://www.kakaobrain.com/blog/113

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

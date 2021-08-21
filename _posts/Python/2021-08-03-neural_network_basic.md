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

title: "[AI basic] 신경망(Neural Network) 개념"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - AI
tags:
  - [python, AI Math, Neural Network, AI Model]
date: 2021-08-03
last_modified_at: 2021-08-03
---
<br>

# 선형모델에서 비선형모델로

❓ 비선형 모델은 어떻게 만들어질까
대표적인 신경망(neural network)에 대해서 알아보자

## 신경망?

![image](https://user-images.githubusercontent.com/77658029/128024885-edd3b7a7-a112-4138-82b6-d202c4cdd719.png)

- 위 그림과 같이 뉴런은 데이터를 받는 Dendrite, 이를 선형 변환 시켜주는 Soma, 비선형 모델로 만들어주는 Axon으로 구성
- Dendrite에서는 전기적 신호를 입력 받는다. 이는 인공신경망에서 데이터 $X$를 의미한다
- Soma는 Dendrite에서 받은 전기적 신호에 가중치($W$)를 곱해 절편($b$) 더해주는 역할을 함, 이때 결과로 $O_{(nxp)}$가 출력됨
- Axon은 Soma에서 선형적으로 계산된 output에 활성함수를 곱해줘 비선형적 결과를 내어줌
- 신경망은 크게보면 `선형모델`과 `활성함수(activation function)`으로 구성됨

### 신경망 구성요소

$X (nxd)$ : 데이터 (데이터를 모아놓은 행렬)
$W (dxp)$ : 가중치 행렬(다른 차원으로 보내주는 행렬)
$b (dxp)$ : 절편
$O (nxp)$ : 생성된 p개의 모델 

![image](https://user-images.githubusercontent.com/77658029/127944167-2a0baf66-3cdc-437c-bf5c-882f04b94a7b.png)

**💡가중치 행렬에 의해 $x_i$가 $o_i$로 매칭됨**

![image](https://user-images.githubusercontent.com/77658029/127944631-9207415a-ffcf-480d-8425-ada1c4bfa52f.png)

## softmax

- 모델의 출력을 확률로 해석할 수 있게 변환해 주는 연산
- 분류문제를 풀때 사용(어떤 분류문제에서 한 부분에 속할 확률을 볼 수 있다)
- 대부분의 선형모델의 결과는 실수값으로 나오기 때문에 이해에 어려움이 있지만, Softmax 함수를 거치면 확률로 보기쉬워짐
- 학습을 하는 경우에 Softmax를 사용함
🚨 추론을 하는 경우 one_hot 벡터를 사용함(추론할 경우 최대값을 가진 주소만 1로 출력하는 연산을 사용)
    ↳ one hot 벡터는 softmax와 다르게 한곳에 확률을 몰아준다고 생각하면 될듯

### softmax 수식

- 단순 Exponential의 함수로 입력값의 크기에 따라 받는 확률의 크기도 커지는 것을 알 수 있다
- 전체 입력의 합을 분모에 두고, 분자에 해당 값을 넣어 확률을 계산한다
- 아래 `code`에서 보면 `np.max(vec)`값을 빼준걸 볼 수 있는데, 지수값에 데이터가 커져 **overflow**되는걸 막아주기 위함이다.

![image](https://user-images.githubusercontent.com/77658029/127944077-f978d125-625a-4bcd-a9a1-1b5da6d55346.png)

**📰code**
```python
import numpy as np

def softmax(vec):
    denumerator = np.exp(vec - np.max(vec, axis=-1, keepdims=True))
    numerator = np.sum(denumerator, axis=-1, keepdims=True)
    val = denumerator/numerator
    return val

vec = np.array([[1,2,0],[-1,0,1],[-10,0,10]])
a=softmax(vec)
print(a)
print(np.sum(a[0]))
print(np.sum(a[1]))
print(np.sum(a[2]))
```
**🔍result**
```
[[2.44728471e-01 6.65240956e-01 9.00305732e-02]
 [9.00305732e-02 2.44728471e-01 6.65240956e-01]
 [2.06106005e-09 4.53978686e-05 9.99954600e-01]]
0.9999999999999999
0.9999999999999999
0.9999999999999999
```

## 활성함수(Activation Function)

- 선형모델을 비선형화 시켜주는 비선형(nonlinear)함수
- 활성함수를 통해서 얻은 값을 잠재벡터(Hidden vector)라고 부름
- 이게 없으면 딥러닝 모델이 아님


![image](https://user-images.githubusercontent.com/77658029/128034973-418e3bae-6b1a-4ee7-b2a3-293b87273374.png)

### 활성함수 종류

- 전통적으로 시그모이드(sigmod), tanh함수를 많이 쓰였지만, 딥러닝에서는 ReLU함수를 많이쓰고있음

![image](https://user-images.githubusercontent.com/77658029/128036233-132dbba7-64fb-49ad-981a-2fb918f916d9.png)

## 다층 퍼셉트론(MLP,Multi-Layer Perceptron)

- MLP는 신경망이 여러층 합성된 함수
- 만약 2개의 layer로 되어 있으면 2층 신경망
- Layer를 타고 올라가는 것을 순전파(forward propagation)라고함

![image](https://user-images.githubusercontent.com/77658029/128039864-699a30e0-f806-471e-9412-6df87cb77491.png)

### 왜 여러 Layer를 쌓을까?

- 이론적으로는 2층 신경망으로 임의의 연속함수를 근사할 수 있음 → Universal approximation theorem
- 하지만, 적은 측을 쓰면 필요한 뉴런의 숫자가 기하급수적으로 늘어나 넒은(wide)신경망이 되어야함
- 층이 깊어질수록 목적함수를 근사하는데 필요한 뉴런(노드)의 숫자가 훨씬 빨리 줄어들어 더 효율적으로 학습이 가능함


## 역전파(Back Propagation) 알고리즘

- 딥러닝의 학습은 역전파 알고리즘을 이용하여 각층에 사용된 파라미터($\{W^{(l)},b^{(l)}\}^L_{l=1}$)를 학습
- 손실함수를 $\mathscr L$이라고 했을때, 역전파는 $\partial \mathscr L/\partial W^{(l)}$를 계산할때 사용
- 각 층 패러미터의 그레디언트 벡터를 윗층부터 역순으로 계산
- 그러다 보니 각층의 그레디언트 벡터를 메모리에 저장이 필요함(메모리 사용↑)

![image](https://user-images.githubusercontent.com/77658029/128045411-26024f13-a1a9-4607-ab66-52b03074f1ad.png)

<br>

**📌reference**
- boostcourse AI tech
- [신경망](https://untitledtblog.tistory.com/141)


<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

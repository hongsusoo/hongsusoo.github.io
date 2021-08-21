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

title: "[AI basic] 확률론(probability theory)"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - AI
tags:
  - [python, AI Math]
date: 2021-08-03
last_modified_at: 2021-08-03
---
<br>

# 확률론

## 딥러닝에서는 왜 확률론이 필요할까?

- 딥러닝은 확률론 기반의 기계학습 이론에 바탕을 두고 있음
- 기계학습에서 사용되는 손실함수(loss function)들의 작동 원리는 데이터 공간을 통계적으로 해석해서 유도하게 됨
- 틀릴 확률(risk)를 최소화 하는 방향으로 훈련하게됨
- 회귀분석 : 손실함수로 사용되는 L2-norm은 예측 오차의 분산을 가장 최소화 하는 방향으로 학습($y-\hat y$)
- 분류문제 : 교차엔트로피(cross-entropy)는 모델 예측의 불확실성을 최소화하는 방향으로 학습
**💡 결론** : 분산 및 불확실성을 최소화 하기 위한 측정 방법을 알아야 하기 때문에 확률론 공부해야함!

<br>

## 확률분포

- 데이터 공간 $\mathscr{X}\times\mathscr{Y}$에서 데이터를 추출해서 만든 분포를 $\mathscr{D}$라고함
- 데이터는 확률변수로 $(X,y)~\mathscr{D}$ 표기
- 확률변수는 이산, 연속 두 가지가 있는데, 확률분포 $\mathscr{D}$에 따라 구분됨(데이터 공간이 아님)
- 만약 데이터 공간이 실수형일때 -0.5~0.5 사이값을 분포의 기준으로 잡으면 이산형이 되기 때문

<br>

### 이산형 확률변수

- 확률변수가 가질 수 있는 경우의 수를 모두 찾아 확률을 더하는 방식으로 모델링
- 그래프는 막대모양 형태로 그려짐
- 분포로 그려지면 확률질량함수와 매칭됨

![image](https://user-images.githubusercontent.com/77658029/127948071-e5cc84fe-e809-4acf-8181-a961d73b1255.png)

<br>

### 연속형 확률변수

- 데이터 공간에 정의된 확률변수의 밀도함수(density)를 적분하는 방식으로 모델링
- 밀도의 경우 누적확률분포의 변화율로 모델링, 확률로 해석하면 안됨
- 분포로 그려질경우 확률밀도함수와 매칭됨

![image](https://user-images.githubusercontent.com/77658029/128599195-a62633ae-4ed0-4a91-8ee5-cbf17eaa6e53.png)

<br>

### 결합확률분포

- 두 가지 이상의 데이터 공간에 대한 확률 분포
- 여러개의 차원이 나눠지고 기준에 따라 확률분포의 모양이 바뀜

![image](https://user-images.githubusercontent.com/77658029/128599160-8fe0a867-6551-45f5-8f87-790aa958bf70.png)

<br>

### 주변확률분포

- 그림에서 보면, $\mathscr{X,Y}$는 연속형 데이터의 성질을 띄지만, 빨간색 box를 만들었을때는 이산형으로 타나날 수 있음
-  $\mathscr{X,Y}$의 결합분포에서 p(x)는 x에 대한 주변확률분포라고 부름, 이때는 y에 대한 정보는 따로 주어지지 않음

![image](https://user-images.githubusercontent.com/77658029/128599178-d02e4c59-1a97-47fb-bd1b-4013e2a4cda0.png)

<br>

### 조건부 확률분포

- 입력변수 x에 대해서 정답이 y일 확률을 의미함(연속확률분포의 경우 단일 값은 0이기 때문에 밀도로 생각해야함)
- P(y|x)로 표현함
- 어떤 값이 일어났을 때의 결과값으로 볼 수 있는데 이런 기능으로 데이터를 넣으면 정답을 배출할 수 있도록 함수를 구성하여 기계학습에서 사용 가능함

![image](https://user-images.githubusercontent.com/77658029/128600039-c6d7c0b0-147f-437b-abab-f5b35db6530b.png)

<br>

## 조건부확률과 기계학습

- 활성함수의 하나인 Softmax를 보면 결과에 대한 확률로 결과가 나오게 되는데, 이 부분을 활용하면 조건부 확률을 통한 기대값을 찾을 수 있음
- 분류함수(classification) : $x$를 넣었을때 $y$가 어디에 속할 확률이 높은지 확인, 특징패턴($\phi$)과 가중치($W$)을 통해 조건부확률 $P(y|x)$로 계산
- 회귀함수(regression) : 회귀란 데이터에 포함되어있는 잔차를 평균으로 되돌리는걸 의미함, 조건부 기대값($E(y|X)$)으로 계산
- 딥러닝 : 다층신경망(MLP)을 활용하여 특정패턴($\phi$)을 추출함

![image](https://user-images.githubusercontent.com/77658029/128608941-8b2b9d9f-c145-45b1-b925-ae81312f7438.png)

<br>

## 몬테카를로 샘플링(Monte Carlo Sampling)

- 기계학습의 많은 문제들은 확률분포를 명시적으로 확인하게 어려운 경우가 대부분임
- 확률분포를 모를때, 데이터를 이용하여 기대값을 계산하는 방식이 몬테카를로 샘플링임
- 독립추출($X^{(i)} ~ i.i.d. P(x)$)이 보장되면, 대수의 법칙(law of large number)에 의해 수렴하게 됨

![image](https://user-images.githubusercontent.com/77658029/128609082-322d0f4c-172b-4a49-a185-247cf35e700c.png)

### 몬테카를로 샘플링을 활용한 $\pi$ 값 계산하기

- $\pi$는 반지름이 1인 원의 넓이 
- 하여 반지름이 1인 원의 반쪽 넓이를 구해 2를 곱해주는 형식으로 구하면 된다. 
- 반지름이 1인 반쪽자리 원의 수식은 $y=\sqrt{1-x^2}$으로 구할 수 있다. 
- 정의역 -1~1 에서 랜덤으로 샘플을 뽑아 함수 $y$의 값들의 평균을 구하면 $\pi$를 구할 수 있다.

**📰code**
```python
import numpy as np

def mc_int(fun, low, high, sample_size = 100, repeat =10):
    int_len = np.abs(high - low)
    stat = []
    for _ in range(repeat):
        x=np.random.uniform(low=low,high=high,size=sample_size)
        fun_x = fun(x)
        int_val = int_len * np.mean(fun_x)
        stat.append(int_val)
    return np.mean(stat),np.std(stat)

def f_x(x):
    return np.sqrt(1-x**2)*2

print(mc_int(f_x, low=-1,high=1, sample_size=100000,repeat=100))
```
**🔍result**
```
(3.1414950042032537, 0.0029135635317170928)
```


**📌reference**
- boostcourse AI tech
- [오차의 과학](https://brunch.co.kr/@gimmesilver/17#comment)

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

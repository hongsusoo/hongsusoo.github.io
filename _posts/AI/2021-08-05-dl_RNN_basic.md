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

title: "순환 신경망(RNN, recurrent Neural Network) 설명"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - DL Basic
tags:
  - 
date: 2021-08-05
last_modified_at: 2021-08-05
---
<br>

# RNN(Recurrent Neural Network)

## 시퀀스 데이터

- 순차적으로 들어오는 데이터를 시퀀스(sequence) 데이터라고 함
- 소리, 문자열, 주가, 시계열(time_series)데이터 등
- 시퀀스 데이터는 독립동등분포(i.i.d.)가 성립하기 어렵기 때문에 순서가 바뀌거나, 과저 정보에 손실이 생기면 확률분포도 바뀜
💡 "개가 철수를 물었다.", "철수가 개를 물었다." 같은 구성의 문자열이지만 순서에 따라 의미가 바뀐다

![image](https://user-images.githubusercontent.com/77658029/128604723-3f72ad49-98a5-4884-98f6-c857ca1d86fa.png)

<br>

## 시퀀스 데이터 확률분포

- 조건부확률을 이용하여 정리해 볼 수 있다
- 시퀀스 데이터를 다루기 위해서는 길이가 가변적인 데이터를 다룰 수 있는 모델이 필요
- 베이즈 정리를 통해 정리할 수 있음

![image](https://user-images.githubusercontent.com/77658029/128621027-c224100d-0a6f-410b-9071-cdf69e86b2c1.png)

<br>

### 시퀀스 데이터 처리 시 문제점

- 시퀀스 데이터 자체적으로 입력 데이터의 수가 변동적임
- 모델을 구성함에 있어 입력 데이터 수의 변동은 모델링하기 어려워짐

**💡 문제를 해결 방법 💡**

1. 고정된 길이의 시퀀스 데이터를 사용(자기회귀모델)
    - 고정된 길이($\tau$) 만큼의 시퀀스만 사용하는 경우 $AR(\tau)$(Autogression Model) 자기회귀모델이라고 함
    - 이 경우 사전에 $\tau$를 정하기 위한 지식이 필요할 수도 있고, 변수로서 지정해줘야하는 번거로움이 있음
    
![image](https://user-images.githubusercontent.com/77658029/128621116-012a05c5-1be2-4f16-93ef-3a91e4ff423d.png)

2. 이전 정보들을 재귀적으로 처리(RNN 방식)
    - 바로 이전정보를 ($X_t$)로, 그 이전정보들을 ($H_{t+1}$)로 인코딩하여 활용하는 AR 모델
    - 따로 $\tau$ 값을 정해주거나, 입력 데이터의 길이에 변동이 없다

<br>

## RNN(Recurrent Neural Network)

- 기본적인 모형은 MLP와 유사함
- 베이즈 정리의 내용처럼 이전 Layer의 사후확률를 현재 Layer의 사전확률로 사용하는 방식으로 Layer를 쌓아감
- foward-propagation
- 여기서 $H_t$는 잠재변수라고 부름
- 이후에 역전파와 순전파를 돌아가며 가중치($w_X, w_H$)를 최적화 시켜 우리가 원하는 방향으로 특징패턴을 뽑아내는게 목적임 

![image](https://user-images.githubusercontent.com/77658029/128621467-e4090d06-31eb-4a2c-b999-02d86129d35c.png)

<br>

## RNN의 역전파 

- 순전파의 반대로 계속 이전 시퀀스로 돌아가며 손실함수가 작아지도록 가중치를 최적화 시켜줌
- 실제결과 $Y$ RNN을 통해 예측된 $Y_t$의 차이를 최소화 하는게 목적임
- 최소화 하기 위해서 Grdient 벡터를 구해서 최소화 하는 $w_X, w_H$를 구해주면됨

![image](https://user-images.githubusercontent.com/77658029/128622175-c27be3ad-284e-48dd-9818-318fab68c825.png)

<br>

### RNN 역전파 gradient 유도

손실함수 : $L(y,y_t)$ → 여기서 $y$는 목표값, $y_t$는 RNN 결과값
잠재함수 : $h_t = X_tw_X+h_{t-1}w_H $

목표는 손실함수를 최소화 하는 $w_H,w_X$를 구하는 것이다. 
그러기 위해서 손실함수가 $w_H,w_X$ 변수에 대한 최소값을 구하기 위해 gradient 벡터를 구해서 최소화 하는 점을 찾아볼 수 있을 것이다.

최종 RNN에 대한 output은 gradout으로 정의할 수 있고,

$$gradout = \frac{\partial L}{\partial h_t}$$

손실함수를 최소로 하는 변수 $w_H,w_X$에 대한 gradient를 구해야함

$$(\frac{\partial L}{\partial w_H}, \frac{\partial L}{\partial w_X})$$

먼저 w_H로 편미분한 값을 구하면
$$\frac{\partial L}{\partial w_H} = \frac{\partial L}{\partial h_t}\times\frac{\partial h_t}{\partial w_H}$$

$$= gradout\times\frac{\partial (X_tw_X+h_{t-1}w_H)}{\partial w_H}$$

곱의 미분으로 풀어주면
$$= gradout\times\left(h_{t-1}+w_H\frac{\partial h_{t-1}}{\partial w_H}\right)$$ 

$$= gradout\times\left(h_{t-1}+w_Hh_{t-2}+w_H^2\frac{\partial h_{t-2}}{\partial w_H}\right)=...$$ 

$$= gradout\times\left(\sum_{i=1}^{N} w_H^{i-1}h_{N-i}\right)$$

동일한 방식으로 w_X로 편미분한 값을 구하면
$$\frac{\partial L}{\partial w_X} = \frac{\partial L}{\partial h_t}\times\frac{\partial h_t}{\partial w_X}$$

$$= gradout\times\frac{\partial (X_tw_X+h_{t-1}w_H)}{\partial w_X}$$

곱의 미분으로 풀어주면
$$= gradout\times\left(X_{t}+w_H\frac{\partial h_{t-1}}{\partial w_H}\right)$$ 

$$= gradout\times\left(X_{t}+w_HX_{t-1}+w_H^2\frac{\partial h_{t-2}}{\partial w_H}\right) = ...$$ 

$$= gradout\times\left(\sum_{i=0}^{N-1} w_H^{i}X_{N-i}\right)$$ 

$$\therefore (\frac{\partial L}{\partial w_H}, \frac{\partial L}{\partial w_X}) = gradout\times\left(\left(\sum_{i=1}^{N} w_H^{i-1}h_{N-i}\right), \left(\sum_{i=0}^{N-1} w_H^{i}X_{N-i}\right)\right)$$

<br>

### 기울기 소실(gradient vanishing)
- 시퀀스의 길이가 길어지는 경우 BPTT를 통한 역전파 알고리즘의 계산이 불안정해짐
- graident를 계속 곱해주기 때문에 0으로 수렴하는 데이터가 존재하게 됨
- 해결책으로 길이를 끊는 것이 필요함(truncated BPTT)
- 이런 문제를 해결하기 위해 나온 네트워크에는 LSTM, GRU가 있음

- Convolution 연산은 Kernel이 모든 입력데이터에 공통으로 적용, 역전파를 계산할 때도 Convolution 연산이 나오게 됨

![image](https://user-images.githubusercontent.com/77658029/128450866-8bc6a9ec-60df-4dd5-bced-48485fe469ff.png)

![image](https://user-images.githubusercontent.com/77658029/128457007-cbcc4dc1-8a43-4698-bdd5-d8ea64689a34.png)

<br>

**📌reference**
- boostcourse AI tech
- [golden planet](http://www.goldenplanet.co.kr/blog/2021/04/27/%EB%B9%85%EB%8D%B0%EC%9D%B4%ED%84%B0-%EA%B3%B5%EB%B6%80-%ED%95%9C-%EA%B1%B8%EC%9D%8C-rnn%EC%88%9C%ED%99%98-%EC%8B%A0%EA%B2%BD%EB%A7%9D%EC%9D%B4%EB%9E%80/)
- [TAEWAN.KIM 블로그](http://taewan.kim/post/cnn/)
- [호롤리한 하루](https://gruuuuu.github.io/machine-learning/cnn-doc/)
- [뇌 외장 하드](https://wjrmffldrhrl.github.io/digital10/)
- [조대협의 블로그](https://bcho.tistory.com/1149)


<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

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

title: "시계열 Model 소개(Naive, RNN, LSTM, GRU)"
excerpt: "about : "
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - DL
tags:
  - 
date: 2021-08-12
last_modified_at: 2021-08-12
---

<br>

# RNN(Recurrent Neural Network)

<br>

## Sequential Model

- Sequential Model의 목표는 현재까지의 데이터를 가지고 미래를 예측하는것
- 현재까지의 데이터는 정확한 기준이 없기 때문에 내가 받아들여야하는 차원을 정확하게 알 수 없음(유동적임)
- 그러기 때문에 차원을 고정시키거나, 차원에 상관없는 모델을 만들어야함

<br>

## Naive Sequence Model

- 유동적인 Input data size로 일반화된 Model 구축이 어려움
- 시간이 지날 수록 데이터가 쌓이기 때문에 데이터 처리가 점점 힘들어짐

![image](https://user-images.githubusercontent.com/77658029/129499490-74a732d6-9e2e-48d4-87cb-8178ac94a6f8.png)

💡 가장 쉬운 해결방법으로 Time Span를 지정해주는 방법(AutoRegressive)

<br>

## AutoRegressive

- 일정 기간동안의 데이터로 현재를 예측함(fixed time span)

![image](https://user-images.githubusercontent.com/77658029/129500015-5c827c91-591d-48cb-b2a6-6d1becf51763.png)

<br>

## Markov Model(first-order autoregression model)

- 가장 기초적이면서 말도안되는 AutoRegression Model
- 1차 AR 모델로 현재는 바로 직전 과거에만 dependant 하다는 가정을 두고 있음 
반례) 내 살은 어제 먹은 음식에으로만 찐 것이다

![image](https://user-images.githubusercontent.com/77658029/129500143-d363f4fd-e536-4d51-bdb7-d8fe3c46d7f8.png)

💡 과거를 전반적으로 대변해 줄 수 있는게 필요함 

<br>

## Latent Autoregressive model

- 기존까지는 과거의 모든 정보를 활용하기 어려운 구조
- hidden state(Latent state)를 추가하여 과거를 요약한 정보를 추가하여 과거 전체를 반영할 수 있도록 함

![image](https://user-images.githubusercontent.com/77658029/129125956-8397820b-e65e-4dd6-94c0-00a82f59e98f.png)

<br>

## RNN(순환신경망, Recurrent Neural Network)

- Latent state를 재귀방식으로 구현한 모델로 한 순간의 과거는 그 이전의 과거들의 요약으로 정리할 수 있음

![image](https://user-images.githubusercontent.com/77658029/129501945-425c6d0c-9683-4ba9-b322-28f50f1cb60c.png)

- RNN의 특징이자 단점은 short-term dependencies로 신경망의 길이가 길어지면 과거의 데이터가 사라지는 현상이 있음
- 과거 데이터의 Vanishing/exploding

![image](https://user-images.githubusercontent.com/77658029/129501744-5208654d-1ba3-47a5-9bd9-feecff8a91b0.png)

💡 데이터를 길게 가져갈 수 있는 모델의 필요함

<br>

## LSTM(Long Short Term Memory)

- LSTM은 Cell state를 통해서 이전 데이터가 흐를 수 있는 길을 만들어줌
- Cell state를 통해서 과거의 data를 지속적으로 관리할 수 있어 Long term data에 대한 관리가 가능해짐
- LSTM 구성 : Cell state, Hidden state, input(X), output(hidden state)

![image](https://user-images.githubusercontent.com/77658029/129566694-e9c003a3-41c0-4906-8fad-e523e0871b19.png)

위 식을 정리하면

![image](https://user-images.githubusercontent.com/77658029/129576138-5b15db46-b036-4861-b154-1b4e885005eb.png)

위와 같은데 

여기서 과거 data 벡터들에 대한 현재의 반영 비율을 곱한 벡터(ⓐ)에 input data 벡터를 반영한 새로운 벡터(ⓑ)를 더해서 Cell State를 업데이트 하게 되고, 여기서 Output을 뽑아내기 위해 update 된 cell state를 조작하여 Output(ⓒ)를 뽑아내게 된다


## GRU(Gated Recurrent Unit)

- LSTM에서는 Output으로 Cell state에 가공을 거쳐 Output으로 조정했다면
- GRU에서는 hidden state(LSTM에 cell state역할)를 바로 Output으로 사용함
- GRU 구성 : Hidden state, input(X), output(hidden state)
- Cell state를 없애면서 LSTM에서 사용했던 마지막 Output Gate를 없앤 형태

![image](https://user-images.githubusercontent.com/77658029/129577667-714745eb-41ce-4b6e-bcf2-eae332cd3c77.png)

<br>

**📌reference**
- boostcourse AI tech
- [Christopher Olah](https://scholar.google.com/citations?user=6dskOSUAAAAJ&hl=en)

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

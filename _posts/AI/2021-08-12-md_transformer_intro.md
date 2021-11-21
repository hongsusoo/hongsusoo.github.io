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

title: "transformer 소개"
excerpt: "about : "
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - AI Model
tags:
  - [transformer]
date: 2021-08-12
last_modified_at: 2021-08-12
---

<br>

# Transformer

- Sequential data를 처리하는 Model
- 요즘은 이미지 분류에도 사용되고 여러 방면으로 사용되고 있음
- Sequential Data의 경우는 중간에 순서의 뒤바뀜, 데이터 누락 등의 문제로 예상/학습에 어려움이 있는데,
- transformer 구조는 self attention을 활용하여 이 문제를 해결하려고 함
- attendtion is all you need(2017)라는 논문에 소개됨


## 모델 구조

- transformer의 경우 여러개의 Encoder와 Decoder로 이뤄져 있음
- RNN의 경우는 재귀적인 함수를 통해서 이전 단어들과의 관계성을 가져왔지만,
- transformer는 한번에 여러 단어를 가져와 벡터화 하여 연산하게 됨
- 여러개의 Encoder와 Decoder를 가지고 있음(단어의 수와 상관 없음)

![image](https://user-images.githubusercontent.com/77658029/129294907-541fb3d2-d1b3-40d8-b5a1-4a545595cb82.png)


## Self Attention

- Self Attention은 각 단어을 벡터로 보고 각 단어들 사이에 유사도를 찾아내는 방식
- 유사도(score)를 구하기 위해 벡터의 내적을 활용
- 1개의 단어를 3가지 벡터로 구성하는데 Queries, Key, Values
- 아래 그림과 같이 Queries와 keys 사이에 유사도를 구하고 이후 Values를 곱하는 방식으로 연산이 진행된다

![image](https://user-images.githubusercontent.com/77658029/129294777-e31ae11c-4d39-4587-821c-3ca90532a4c5.png)

### queries, keys, values 벡터

- 각 벡터에 대한 가중치를 곱해주는 방식으로  queries, keys, values 벡터를 구한다

![image](https://user-images.githubusercontent.com/77658029/129295544-a3ad5181-cd29-4925-a1bf-8440cecff503.png)


## MHA(Multi Headed Attention)

- 한 단어에 여러개의 queries, keys, values 벡터들을 만들어 n번의 attention을 반복하면, n개의 encoding된 벡터를 얻을 수 있음
- 논문에서는 8개의 벡터로 계산
- 8개의 encoding의 벡터를 나열한 다음 다시 가중치를 곱해서 하나의 벡터 크기로 scale을 맞춰주는 작업을 진행한다


## Positional Encoding

- 현재까지 계산한 데이터는 순서에 대한 부분이 빠져있는데 이부분을 추가하기 위해서 맨 처음 input 데이터에 position data를 더해주는 작업을 진행함

![image](https://user-images.githubusercontent.com/77658029/129302445-c7605fd6-0eff-4f14-bad5-082fde499a58.png)


## Decoder

- encoder에서 생성된 queries, keys, values벡터 중 keys,values 벡터만 decoding을 진행하게 됨
- 우리는 언어를 번역해주는 것이기 때문에 keys, values를 가지고 새로운 언어에 대한 queries벡터를 받아 연산을 진행함

![transformer_decoding_2](https://user-images.githubusercontent.com/77658029/129302879-508b1a7c-8050-4484-82ef-de39954efd7d.gif)



## 장단점

- 다른 모델에 비해서 자유도가 높다, 같은 입력이라도 주변 데이터에 따라서 결과값이 다르게 출력한다
- 이로 인해서 더 여러 상활을 표현할 수 있다
- 최근 번역 이외에도 이미지 분류 model로도 사용되고 있음
- 하지만 n개의 데이터를 처리할때, 한번에 $n^2$의 연산을 필요로 하기 때문에, 큰 메모리를 필요로한다.
- 큰 데이터를 처리할때, RNN은 오래 걸려도 결국은 결과값을 얻을 수 있지만, Transformer는 메모리가 부족하면 연산이 어렵다



**📌reference**
- boostcourse AI tech
- [Jay Alammar](http://jalammar.github.io/illustrated-transformer/)


<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

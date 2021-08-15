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

title: "[boostcourse] Day8 학습기록_minibatch28"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - daily
tags:
  - []
date: 2021-08-11
last_modified_at: 2021-08-11
---
<br>

## 학습 내용

<a href="https://hongsusoo.github.io/ai/cnnmodel"><img src="https://img.shields.io/badge/-CNN Model-red"/></a> <a href="https://hongsusoo.github.io/ai/CVapplication"><img src="https://img.shields.io/badge/-CV-red"/></a>


선택2번 추가 공부

<a href="https://hongsusoo.github.io/ai/AAE"><img src="https://img.shields.io/badge/-AAE-blue"/></a>

<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 홍요한

참가자 : 강재현, 권예환, 김준태, 박마루찬, 서광채, 장동건, 홍요한

<br>

### 건의사항

- 강의에서 AlexNet, GoogLeNet에 대해서 다뤘는데, 내용 설명이 아닌 구현으로 해보는건 어떨지?

    논의 item

    1. 알려진 모델에 dataset하나 정해서 Test 후 비교해보기
    2. 직접 구현

    → 모델의 중요한 부분의 code에 대해서 review하는 형식으로 진행하자

    모델의 중요 code에 대해서 Review하는 것으로 얘기됨

<br>

### 과제 리뷰

- 선택과제 2번 설명 AAE (홍요한, 김준태)
- 선택과제 3번 설명 MDN (강재현, 권예환, 장동건)

<br>

### 질문내용

1. 질문 : kaiming(ReLU), xavier(sigmoid) 등 다양한 weight 초기화 방법이 있는데, 어떤 상황일 때 어떤 방법으로 initialization을 하면 좋을지?(재현님)

    답 : activation function하고 관련이 있다 -추가 확인 필요함

2. 질문 : CNN에서는 따로 weight 초기화를 해주면 학습이 잘 되는건 알겠습니다. 근데 단순 MLP같은 경우 weight 초기화를 다르게 해준다고 해서 목적식이 바뀌는 것도 아닌데 초기화를 공들여서 하는 의미가 있을까요?(재현님)

    답 : sigmoid - gradient vanishing 

    [DL Basic 추가정리) Weight Initialize를 하는 이유?](https://velog.io/@hanlyang0522/weight-init%EC%9D%84-%ED%95%98%EB%8A%94-%EC%9D%B4%EC%9C%A0)

3. 질문 : 이미지 분류대회를 했을떄 모델 말고 다른 선택해야할게 있을까?

    답 : activation function, opt, weight init 등 여러 함수들 선택해야함

<br>

## 회고록

오늘 AAE에 대해서 조원들에게 공유하는 시간이 있었다. 시간을 투자한 것에 비해서 생각보다 전달이 안됐던 것 같다. 
요점을 찍어서 알려줘야하는데,, 나 조차도 뭐가 중요한지 어떤걸 궁금해할지 생각할 여유가 없었던 것 같다. 

앞으로 DL 관련 Model를 이해하거나 설명할 때, 

1. 배경 & 흐름을 설명
2. 이전에 모델 대비 개선점
3. Loss Function(어떻게 학습하는지)

상기 3가지를 기억해 놔야겠다. 


<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

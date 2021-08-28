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

title: "[boostcourse] Day15 학습기록_minibatch28"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - daily
tags:
  - []
date: 2021-08-23
last_modified_at: 2021-08-23
---
<br>

## 학습 내용


<a href="https://hongsusoo.github.io/ai/proj_ImageClassify00"><img src="https://img.shields.io/badge/-project 시작-red"/></a> 

<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 홍요한

참가자 : 강재현, 권예환, 김준태, 박마루찬, 서광채, 장동건, 홍요한

<br>

### 4주차 피어세션 진행 방향

- 진도 : special mission  기준으로 진행

    → 각자의 속도에 맞춰서 진행하고, 질문 사항들은 Slack 및 피어세션 활용하여 질문

    → 추가적으로 진행된 내용이나, idea 등 공유하기

- 명일 피어세션 활동

    EDA 

    - class 별 분포(각 feature별로 데이터 편향성 확인)
    - 추가적인 Data 관련 내용 공유
    - 정리한 내용은 github에 각자 folder에 저장(차주부터 PR 로 연습하기)

<br>

### 사전 질문내용

- Q 

        .eval() 어떤 함수 일까

    A  

        1. model 출력 확인용 
    [참고자료](https://bluehorn07.github.io/2021/02/27/model-eval-and-train.html)

<br>

### 모델 리뷰

- 마루찬님
    - 기존 code 기반으로 시작 → EfficientNet-B4
    - 개선 할만한 부분
        1. data 추가 트레이닝
        2. batch size 늘려서 시도
        3. data augmentation → [https://arxiv.org/pdf/2009.08369.pdf](https://arxiv.org/pdf/2009.08369.pdf)
        4. 앙상블 최신 기법 확인 → 모델 돌리고 나면, output 파일을 따로 만들고 처리해서 결과 출력
- 재현님
    - 기존 code 기반으로 → EfficientNet
    - 개선
        - data aumentation 기법
        - WandB연결
        - class  3x3x2 → 다 읽고 18개 로 나타나는게 아니라 class 별로 3개의 모델을만들어서 앙상블


<br>

## 회고록

어떤식으로 시작해야할지 방향성을 못 잡는 하루였다. 

Dataset 구성을 하기전에 EDA를 진행하려고 했는데,  data 다루는게 아직 익숙하지가 않았다. Pandas를 자주 활용해서 익숙해질 수 있도록 꾸준히 연습해봐야 할 것 같다.

천천히 해야지 하는데, 이미 제출한 사람들이 나오다보니 마음이 조급해지는건 어쩔수가 없나보다.

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

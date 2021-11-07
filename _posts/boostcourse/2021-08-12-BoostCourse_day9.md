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

title: "[boostcourse] Day9 학습기록_minibatch28"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - daily
tags:
  - []
date: 2021-08-12
last_modified_at: 2021-08-12
---
<br>

## 학습 내용

<a href="https://hongsusoo.github.io/ai_models/md_transformer_intro"><img src="https://img.shields.io/badge/-transformer-red"/></a> <a href="https://hongsusoo.github.io/ai_models/md_rnnmodel"><img src="https://img.shields.io/badge/-RNN Model-red"/></a>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦


모더레이터 : 강재현

참가자 : 강재현, 권예환, 김준태, 박마루찬, 서광채, 장동건, 홍요한

<br>

### 과제 리뷰

선택 1,2,3 / 필수 1,2,3 관련 질문

- 선택 2 질문(박마루찬님)

    과제코드 맨 아래쪽에 결과 위의 이미지가 입력 노이즈 이미지라고 하는데, 입력의 정체가 잘 이해가 되지 않습니다.

    → 홍요한님, 김준태님 답변

- to_device()의 의미 (홍요한님)

    언제 써줘야 할까요?

    →모델과 데이터를 함께 같은 device에 넣어줘야 함 (권예환님 답변)

- attention에서 Q K의 내적 구현에 대해(강재현님)

    → 실제로 차원 확인해봐야 할 듯 + documentation (박마루찬님 + 홍요한님 답변)

<br>

## 회고록

피어세션에서 과제 리뷰와 질문에 대한 답변이 끝난 후 시간이 남는 경우 알고리즘 문제를 풀기로 했다. 이번에 풀 문제는 [벽 부수고 이동하기](https://www.acmicpc.net/problem/2206) 라는 문제다. 열심히 AI를 공부하고 코테에서 떨어지는 일이 없도록 감을 잃지 않게 조금씩 풀어보는 건 괜찮은 것 같다. 


<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

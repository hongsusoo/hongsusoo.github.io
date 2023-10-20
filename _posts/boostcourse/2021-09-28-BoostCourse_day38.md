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

title: "[boostcourse] Day38 학습기록_팀명뭘로하조"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - boostcourse
tags:
  - []
date: 2021-09-28
last_modified_at: 2021-09-28
---

## 학습 내용

- 2 Stage Detectors

<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 홍요한

참가자 : 박범수, 박준혁, 서희수, 한건우, 홍요한, 황원상, 조혜원

<br>

### 토의 내용

Q 범수님 :  RPN 2k score?

A : 배경인지 Object인지 구분하기 위해 2개로 진행

Q 원상님 :  배경, Object 구분하는데 왜 2개의 인자를 사용하는지?

A :  RPN에서 배경도 아니고 object도 아닌 경우를 구분하기 위해 사용되는 것으로 보임

Q 원상님 : anchor box 가 어떻게 사용되는지..? 질문 이해를 잘 못했어요..

Q : NMS는 학습할때만 사용 가능한 기법인가요?

- GT 와 비교해서 높은 bbox를 기준으로 bbox수를 조절하는 알고리즘으로 이해했는데, 
만약 실제 예측해야할 Data가 들어왔을 경우 어떻게 IoU를 뽑을까요?

A : Score 값으로 IoU값을 대체하여 NMS진행

## 회고록

YOLO V1 논문을 실제로 읽다보니, 블로그나 강의를 보면서 느낌으로 이해했던 내용들과 실제 내용에 차이가 있었다. 느낌을 가져가는 건 좋지만, 그걸 맹신하면 안될 것 같다. 공부하면서 끊임없이 수정/보완 해야할 것 같다. 

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

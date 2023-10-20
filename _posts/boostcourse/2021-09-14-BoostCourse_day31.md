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

title: "[boostcourse] Day31 학습기록"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - boostcourse
tags:
  - []
date: 2021-09-14
last_modified_at: 2021-09-14
---

## 학습 내용

- Instance/Panoptic Segmentation and Landmark Localization
- (선택과제) Human Pose Estimation Using Hourglass Network

<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 박승찬

참가자 : 박승찬, 한건우, 배지연, 강재현, 오하은, 홍요한

<br>

### 토의 내용

강의내용
  1. 승찬님 : Competition에서도 CenterNet, CornerNet 적용 가능한지?
  2. Panoptic Segmentation와 instance Segmentation 차이 
      1. 하은님 : Instance Segmentation은 배경을 예측하지 않지만, Panoptic은 배경도 예측함
  3. 승찬님 : Object region을 모두 합해서 빼면 background가 되는지?
  4. 승찬님 : Box Regression의 구체적 구현 방법
      1. 재현님 : 좌표 형태로 regression함
  5. 재현님 : feature Pyramid 원리란?
      1. backbone block에서 추출된 feature들을 피라미드 형태로 쌓은 것

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

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

title: "[boostcourse] Day37 학습기록_팀명뭘로하조"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - daily
tags:
  - []
date: 2021-09-27
last_modified_at: 2021-09-27
---

## 학습 내용

- Object Detection Overview

<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 서희수

참가자 : 박범수, 박준혁, 서희수, 한건우, 홍요한, 황원상, 조혜원

<br>

### 토의 내용

- validation set을 나누는 방법
    
    stratified하게 나누기
    
    한 이미지에 여러개의 bbox와 label이 존재하기 때문에 train하고 validation에 같은 이미지가 들어가지 않도록 해볼 예정
    
- 협업툴
    
    github kanban dashboard
    
- YOLOv1읽어오기 (29일까지)
    
    [Detection 논문 목록]
    - RCNN
    - fast RCNN
    - faster RCNN
    - YOLOv1
    - YOLOv2
    - YOLOv3
    - SSD
    - DETR
    - YOLOv4
    - scaled-YOLOv4
    - YOLOv5


## 회고록

EDA를 하면서 뭔가 기존 방식으로만 하다보니, 발전이 없는것 같다. 시각화 하는 방법도 조금씩은 공부가 필요할 것 같다. 그리고 아직도 Numpy나 Pandas 사용에 미숙한것 같다. 어떻게 하면 조금 익숙하게 사용할 수 있을까 고민을 해봐야겠다.

P-stage 재활용 데이터

- EDA
    1. 종이와 일반 쓰레기의 구별이 애매함
    2. Labeling 잘못된게 많이 있음
    3. NMS 이외에 다른 방법들

남은 P-stage에선

1. 가설을 세우고, 결과를 봐보자
2. 방법을 사용한 이유에 대해서 고민하면 좋을것 같다

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

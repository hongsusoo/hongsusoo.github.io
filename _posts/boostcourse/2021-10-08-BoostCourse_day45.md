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

title: "[boostcourse] Day45 학습기록_팀명뭘로하조"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - boostcourse
tags:
  - []
date: 2021-10-08
last_modified_at: 2021-10-08
---

## 학습 내용

- Augmentation 실험

<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 황원상

참가자 : 박범수, 박준혁, 서희수, 한건우, 홍요한, 황원상, 조혜원

<br>

### 토의 내용

- Augmentation 평가 시 plain model 보다 현저하게 낮은 LB값이 나옴
- Learning Rate를 너무 크게 줘서 학습이 덜 된 것으로 사료됨 -> 이미지상 초록색으로 돌린게 lr 0.0001, 나머지가 lr 0.02로 LR 차이에 따라 학습 수준이 크게 좌우됨
- baseline : 0.620, 평가 : 0.442

![image](https://user-images.githubusercontent.com/77658029/137635441-7b3d88b5-dad7-4da3-a25a-5b3d5ec4c632.png)

- LR를 줄여서 다시 시도해보기


```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

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

title: "[boostcourse] Day46 학습기록_팀명뭘로하조"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - daily
tags:
  - []
date: 2021-10-12
last_modified_at: 2021-10-12
---

## 학습 내용

- Data augmentation

<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 조혜원

참가자 : 박범수, 박준혁, 서희수, 한건우, 홍요한, 황원상, 조혜원

<br>

### 토의 내용

- Data augmentation 진행결과 공유, 전반적으로 비슷한 수준으로 학습되어 LB 0.619

![image](https://user-images.githubusercontent.com/77658029/137635625-08f07754-db57-4dd2-ad9c-c3700897b450.png)

- Data Cleaning 진행 -> 삭제할 Bounding Box 선정
  1. 영수증 뭉치 제거
  2. 어두워서 안보이는 부분 제거
  3. 전단지에 안보이는 테이프 제거
  4. 종량제 봉투는 모두 plastic bag
  5. 누런 박스 -> paper
  6. 이미지 전체 box친 애들중 클래스 특징이 없는애들 제거

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

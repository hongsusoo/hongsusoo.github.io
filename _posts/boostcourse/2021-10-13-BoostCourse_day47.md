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

title: "[boostcourse] Day47 학습기록_팀명뭘로하조"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - boostcourse
tags:
  - []
date: 2021-10-13
last_modified_at: 2021-10-13
---

## 학습 내용

- 실험 : UniverseNet의 Resize 크기가 일정하게 정해져 있는데, 가로로 큰 사이즈로만 resize를 진행함 → 다른 비율의 객체는 찾기 어려울 것
  다른 크기로 Test 하면 어떻게 될지 실험 (base : (1333, 480), (1333, 960), test1 : (480,1333), (960,1333), test2 : (1333, 480), (1333, 960),(480,1333), (960,1333)

  ![image](https://user-images.githubusercontent.com/77658029/137636822-6511d00d-f2aa-437e-bb10-23bd52a40f26.png)

  결과 : LB 상 test1에서 큰 차이가 있었음 base : 0.451,  test1 : 0.485, test2 : 0.446
  분석 : BBox의 사이즈 비율이 세로보단 가로가 긴 경우가 조금더 많아, base 보단 test1의 성능 향상에 도움이 된 것으로 사료됨

  ![image](https://user-images.githubusercontent.com/77658029/137636842-a247e53d-4a57-4a13-9dfd-8dd23226cc79.png)


<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 박범수

참가자 : 박범수, 박준혁, 서희수, 한건우, 홍요한, 황원상, 조혜원

<br>

### 토의 내용

- Data cleaning와 Data augmentation 진행한 모델로 test 진행


```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

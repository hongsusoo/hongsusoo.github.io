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

title: "[boostcourse] Day85 학습기록_팀명뭘로하조"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - daily
tags:
  - []
date: 2021-12-06
last_modified_at: 2021-12-06
---

## 학습 내용

- 선형대수 공부(<a href="https://hongsusoo.github.io/ai%20math/math_matrix3"><img src="https://img.shields.io/badge/-고윳값분해-red"/></a>)

- 최적화 1,2등 Solution 정리
  - Target Device 확인하기 : 채점 Server는 GPU로 진행하게됨
  - CPU는 작은 연산을 여러번 하는 것이 적합하고, GPU는 한번에 많은 연산에 적합함
  - Layer 별로 GPU에 올려서 연산하게 되는데, Layer 수가 많아지면 결국 속도 저하로 이어지게 됨
  <img src="https://user-images.githubusercontent.com/77658029/144724315-512f5568-00ea-4e08-b608-0d9464586827.png"  width="70%" height="70%"/>
  - 결국 Parameter의 수보다 Layer의 수가 더 큰 변수로 작용하게 됨
  <img src="https://user-images.githubusercontent.com/77658029/144724421-96f93413-b15a-4877-9e37-3be06292e2ed.png"  width="70%" height="70%"/>
  - Knowledge Distillation 적용
    1. Teacher (ResNext: f1 0.8141)
      - Student: 0.7058 -> 0.7272
      - Student: 0.7310 -> 0.7396
    2. Teacher (ViT: f1 0.8755)
      - Student: 0.7670 -> 0.7574
      - Student: 0.7310 -> 0.7294 (T=20) -> 0.7326 (T=6)

<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

- 최적화 대회 정리


## 📝멘토링

1. REAL TIME 가능할까?
    - REAL TIME 포기하고 녹화된 영상 서버로 보내면 서버에서 INFERENCE하고 결과 보내주기
    - 데스크탑 서버로
    
결과 발표 시 real tim을 빼고 sample video 넣어서 inference결과 보여주기

멘토님 프로젝트 예시 : [https://github.com/minsuk-sung/boaz-adv-project](https://github.com/minsuk-sung/boaz-adv-project)

- 실시간 어려움
- 웹 - 장고

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

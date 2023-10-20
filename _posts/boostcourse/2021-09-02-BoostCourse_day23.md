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

title: "[boostcourse] Day23 학습기록_minibatch28"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - boostcourse
tags:
  - []
date: 2021-09-02
last_modified_at: 2021-09-02
---

<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 강재현

참가자 : 강재현, 권예환, 김준태, 박마루찬, 서광채, 장동건, 홍요한


<br>

### 대회 진행상황 공유

- ensemble 진행
    1. soft-voting (재현, 준태, 광채, (준태2 * 1.2))
    2. soft-voting (재현, 준태, 광채, 준태2(1, 4 class에만 *1.1))
    3. soft-voting (재현, 준태, 광채, 준태2, (광채2*0.9))
    4. soft-voting (재현, 광채, 준태2, 광채2)

- 확인 내용
    1. 단일 Model일 경우 50대 후반의 Class를 60대 이상으로 분류하면 F1 score가 높게 나오지만, 
    Ensemble로 할 경우 낮아짐
    2. 동일 모델이라도 Dataset 구성에 따라 값차이가 큼

<br>

## 회고록

1등한 팀에서 진행한 결과를 보니, 다들 비슷한 문제를 가지고 있었던 것 같다. 나이라는 애매한 분류를 위해서 여러 방법들을 시도 했던것 같다. 상위권 팀 대부분에서 사용했던건 pseudo labeling인데, 기존에 주어진 validation data를 가지고 이미 학습된 model로 결과를 뽑은 다음

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

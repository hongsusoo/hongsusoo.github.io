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

title: "[boostcourse] Day20 학습기록_minibatch28"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - boostcourse
tags:
  - []
date: 2021-08-30
last_modified_at: 2021-08-30
---

<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 서광채

참가자 : 강재현, 권예환, 김준태, 박마루찬, 서광채, 장동건, 홍요한


<br>

### 대회 진행상황 공유

- 대회 직전까지 각자의 Model를 구성해보자

<br>

## 회고록

제공된 baseline를 이해하기 위해서 코드를 하나하나 뜯어 보면서 이해하는 시간을 가졌다. 그리고 기존의 Jupyter Notebook에서 작업했던 여러 기능들을 추가해보았는데, 생각보다 baseline code가 잘 갖춰져 있어서 편하게 작업할 수 있었다.

나만의 baseline code를 만들어 보고싶어졌고, 다음 competition 때는 유용한 baseline code를 하나 만들어보고 싶어졌다.

오늘은 face crop을 baseline에 심는 코드를 만들어 github로 팀원들과 함께 사용하였는데, 팀원들에게 도움이 된 것 같아 그 동안 낮아진 자존감을 조금은 챙길 수 있었다. 

앞으로 팀원들을 위한 기초적인 base code를 공유하는 습관을 들여봐야겠다. 

🥄 오늘의 시도


8번째 제출

  - Face Crop을 활용하여 위에 동일한 상황에서 Test 진행
  - batch size 4
  - optim : Adam
  - loss : Cross Entropy loss
  - lr : 1e-4
  - 10 epoch
  - test acc : 81.8

결과
  - f1 : 0.6847
  - acc : 74.39%

기존 Jupyter code와 달라진게 없는것 같은데, 차이가 크게 났다. 뭐가 문제인지 좀더 고민이 필요할것 같다.


<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

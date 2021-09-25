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

title: "[boostcourse] Day33 학습기록"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - daily
tags:
  - []
date: 2021-09-16
last_modified_at: 2021-09-16
---

## 학습 내용

- Multi-modal Learning
- Image Captioning

<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 배지연

참가자 : 박승찬, 한건우, 배지연, 강재현, 오하은, 홍요한

<br>

### 토의 내용

#### Multi-modal Further Question

1. Multi-modal learning에 feature 사이의 semantic을 유지하기 위해서 어떤 학습방법을 사용했나요? 이 질문에서 feature 사이의 semantic이 어떤 의미인가?

    → Matching 방법이 가장 적절한 방법인 것 같다. (Metric Learning) 

    → Matching, Translating, Referencing 모두 해당되는 것 같다

2. Captioning task를 풀 때, attention이 어떻게 사용될 수 있나요?

    → 주변을 어떻게 참조할까?

    → 이미지를 볼 때 순서까지 학습을 하는 것 같다

    → NLP에서 쓰이는 attention과 많이 다른 것 같지는 않음

    → 공간정보에 관한 attention을 weight로 사용해서 feature를 추출

3. Sound source localization task를 풀 때, audio 정보는 어떻게 활용되었나요?

    → Attention 활용, 비지도학습을 활용한다는 점이 흥미로웠음

    → 네트워크를 통과한 image 관련 feature와 audio feature를 내적해서 유사도를 측정한 후, 그 유사도를 나중에 다시 사용한다고 이해함

#### GAN Assignment

1. 과제
    1. training이 안 됨
    2. resize에서 사이즈를 64로 적용함 → 사진 크기 줄이는게 데이터 손실이 많은 것 같은데...
    3. 하얀색으로 계속 나오는 문제가 있음 → 색반전 효과가 없음 
    4. 두 loss가 0.6(0.7) : 0.6(0.7)이 가장 이상적임
    5. 현재 loss 튀는 정도가 심함
    
<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

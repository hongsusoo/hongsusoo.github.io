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

title: "[boostcourse] Day56 학습기록_팀명뭘로하조"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - boostcourse
tags:
  - []
date: 2021-10-26
last_modified_at: 2021-10-26
---

## 학습 내용


- LR 최적화 진행

![image](https://user-images.githubusercontent.com/77658029/139911803-487d9652-15f8-4bf6-a1dc-85560e518048.png)

<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 서희수

참가자 : 박범수, 박준혁, 서희수, 한건우, 홍요한, 황원상, 조혜원

<br>

### 대회 진행

- Pseudo-labeling 해볼까? 
일단 지금 best csv 기반으로
→ json 새로 만드는 것보다 image 기반으로 annotation 만드는게 편할듯..?
→ 원상님: 일요일까지 pseudo data 생성 코드 준비하겠음 (baseline(smp)용, mmseg 용)
- Model, architecture 뿐만 아니라 loss도 어떤게 성능이 좋을지 test가 필요할듯?
DiceCELoss test
- efficientnet-b3  + Unet++ 에 DiceCELoss 40epoch로 학습 예정
- HRNet + OCR module 실험 예정
- HRNet 학습 정리 발표

HRNet은 low level feature(고해상도 정보)를 마지막 단까지 잘 유지하며 비슷한 파라미터 수를 가질때 더 빠른 속도를 가지는 방법

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

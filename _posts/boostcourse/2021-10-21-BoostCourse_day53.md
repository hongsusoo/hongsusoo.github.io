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

title: "[boostcourse] Day53 학습기록_팀명뭘로하조"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - daily
tags:
  - []
date: 2021-10-21
last_modified_at: 2021-10-21
---

## 학습 내용

- K-Fold 구현 및 Data 확인
- FCN의 한계를 극복하기 위한 모델(<a href="https://hongsusoo.github.io/ai/beyondfcn01"><img src="https://img.shields.io/badge/-FCN 극복-red"/></a>)

<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 황원상

참가자 : 박범수, 박준혁, 서희수, 한건우, 홍요한, 황원상, 조혜원

<br>

### 대회 진행

- 범수님 4강 전반 (FCN 문제점, DeconvNet, Transposed Convolution, SegNet) 리뷰
- 요한님 4강 후반(FC DenseNet, DeepLabV1, DilatedNet) 리뷰

- 내일 5강 발표자
    - 건우님 5강 전반 (처음부터 DeepLabV3 까지)
    - 혜원님 5강 후반 (DeepLabV3+ 부터  끝까지)
- 범수님 augmentation
    - CLAHE가 uint8이 아니면 안되는 문제
    - Elastice transform 적용해볼 예정
- 희수님 augmentation 제안 - blur, gaussianBlur, fog - 숟가락이 여러 part가 분리되어 분류된 결과를 보며..
- 준혁님 CRF, mmsegmetation의 HRNet 시도 예정
- 요한님 train/val 나눠서 해봤는데.. 점수가 낮게 나와서 수정을 좀 해보려고 함. 모델이 안좋은 듯
- 희수님 Unet++에 다른 backbone(혜원님 점수 높았던 것)으로 돌려볼 예정
- 원상님 DeeplabV3+ + effnetb8  학습 중, BEiT 돌리기 위해 mmsegmentation 에서 돌아가는 Dataset 클래스 구현 예정 → 준혁님 토론게시판에 누가 구현해서 올려놓았음

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

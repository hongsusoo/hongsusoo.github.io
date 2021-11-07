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

title: "[boostcourse] Day52 학습기록_팀명뭘로하조"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - daily
tags:
  - []
date: 2021-10-20
last_modified_at: 2021-10-20
---

## 학습 내용

- Validation set 구하기
- semantic segmentation의 기초와 이해(<a href="https://hongsusoo.github.io/ai_models/md_seg_fcn"><img src="https://img.shields.io/badge/-FCN-red"/></a>) 강의
- EDA 진행 
  - Class imbalance 가 큼
![image](https://user-images.githubusercontent.com/77658029/139706482-87ad383c-86a7-46ac-b375-404b98d7e1de.png)
  - Segmentation 크기에 따라 분류시 세 부분으로 구분하여 확인시, 20 pixel 이하의 object가 많은 부분을 차지하고 있음
![image](https://user-images.githubusercontent.com/77658029/139706966-88aebf9a-1caa-4852-b039-6b051de234ea.png)

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

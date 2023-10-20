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

title: "[boostcourse] Day51 학습기록_팀명뭘로하조"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - boostcourse
tags:
  - []
date: 2021-10-19
last_modified_at: 2021-10-19
---

## 학습 내용

- Validation set 구하기
- semantic segmentation의 기초와 이해(<a href="https://hongsusoo.github.io/dl/md_seg_fcn"><img src="https://img.shields.io/badge/-FCN-red"/></a>) 강의
- EDA 진행 
  - Class imbalance 가 큼
![image](https://user-images.githubusercontent.com/77658029/139706482-87ad383c-86a7-46ac-b375-404b98d7e1de.png)
  - Segmentation 크기에 따라 분류시 세 부분으로 구분하여 확인시, 20 pixel 이하의 object가 많은 부분을 차지하고 있음
![image](https://user-images.githubusercontent.com/77658029/139706966-88aebf9a-1caa-4852-b039-6b051de234ea.png)

<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 홍요한

참가자 : 박범수, 박준혁, 서희수, 한건우, 홍요한, 황원상, 조혜원

<br>

### 대회 진행

- 희수님 3강 Segmentation 설명 
- 범수님 : Augmentations- Rotate, ResizeCrop, GridDropout Test 진행
- 준혁님 : TIMM에 있는 encoder 있는 모델에서 parameter 많은 모델로 돌려보자
- 희수님 : efficientnet-b7_Unet++ 12시 이후 제출 예정
- 원상님 : Pan Resnet101 0.407 , BEiT(Transformer) 모델 환경설정 진행 중
- backbone - efficientnet B7 좋을 듯
- resnet에 150도 있더라
- SMP에 있는 모델들은 전반적으로 다 돌려봤는데,  추후 어떤 모델을 돌려볼지
    
    Batch는 돌릴수 있을만큼 설정
    
    1. Deeplab 으로 양산하는 방향..?
    2. deeplabv3+ timm-efficientnet-b8 - 원상님
    3. SE-Net  se_resnext101 32x4d - 혜원님
    4. deeplabv3+ DPN131 - 준혁님
    5. resnet152_deeplabv3+ - 희수님
    6. timm-regnety_320 - 건우님
    7. timm-efficientnet-l2(noisy student) - 건우님
    8. timm-gernet_l_DeepLabV3+ - 준혁님

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

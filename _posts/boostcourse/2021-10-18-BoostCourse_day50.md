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

title: "[boostcourse] Day50 학습기록_팀명뭘로하조"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - boostcourse
tags:
  - []
date: 2021-10-18
last_modified_at: 2021-10-18
---

## 학습 내용

- 재활용 쓰레기 Segmentation Competition 진행
- Validation Dataset 구축하기 위한 사전 작업 진행
- overview, introduction, competition overview 강의 듣기(<a href="https://hongsusoo.github.io/ai/seg_overview"><img src="https://img.shields.io/badge/-overview-red"/></a>)

<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 한건우

참가자 : 박범수, 박준혁, 서희수, 한건우, 홍요한, 황원상, 조혜원

<br>

### 대회 진행

- 역할 배분하여 대회 진행하기

  - val dataset 1명
      - 2번 정도 dataset 바꿔가면서 제출
      - LB 보고 dataset 버져닝
      - 후보
          - 요한님 unet / efficientnet b5
          
  - augmentation 1명
      - albumentation, 기타 aug 라이브러리 실험해서 LB 확인
      - 후보
          - 범수님 unet / efficientnet b5
          
  - segmentation model 사용 00명
      - pytorch segmentation 라이브러리 사용해서 실험
      - 다른 라이브러리도 사용
      - 후보
          - 희수님 Unet ++ / resnet101
          - 준혁님 deeplabv3+ /resnet101
          - 원상님 PAN / resnet101
          - 혜원님 DeeplabV3 / resnet101
      - optimizer / lr 및 하이퍼파리미터는 baseline 코드 고정
      - 모델 아키텍처 / 백본만 변경


```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

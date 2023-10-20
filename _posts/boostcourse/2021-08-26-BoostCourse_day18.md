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

title: "[boostcourse] Day18 학습기록_minibatch28"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - boostcourse
tags:
  - []
date: 2021-08-26
last_modified_at: 2021-08-26
---
<br>

## 학습 내용

<a href="https://hongsusoo.github.io/ai/proj_ImageClassify03"><img src="https://img.shields.io/badge/-DenseNet 제출-red"/></a> 
<a href="https://hongsusoo.github.io/ai/proj_ImageClassify04"><img src="https://img.shields.io/badge/-check Point 정리-red"/></a> 

<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 김준태

참가자 : 강재현, 권예환, 김준태, 박마루찬, 서광채, 장동건, 홍요한

<br>

### 대회 진행상황 공유

- 강재현 

     : cutmix, TTA는 오류로 보류, dataset - 마루찬님 코드로 validation 나눔, 클래스 불균형 해소 위해서 가중치를 다르게 줌, Ray도 적용 예정

- 권예환 

     : transform 여러가지 추가해보면서 모델 돌려봄, 나이 60세이상에 다른 데이터들 넣어봤음 → 성능이 떨어짐

- 김준태 

     : ResNet-18, 50, efficientnet-b4 돌려보고, transform 적용. validation 적용 예정

- 박마루찬 

     : validation 오류 해결, transform 추가, 캐글에서 가져온 데이터 추가할 예정 → 추가 데이터를 모델에 넣어볼 수 있게 데이터 처리

- 서광채 

     : validation forder기준으로 분류,  모델링에 weight추가, TTA 실행, cutmix하거나 다른 모델을 할 예정 → 데이터 프레임을 이용하여 데이터셋 구축

- 장동건 

     : inception_v3 fi score가 0.67 정도 나옴, transform 적용, earlyStopping 자동으로 모델 저장 및 성능이 좋은 곳에서 멈춰줌

- 홍요한 

     : inception_v3를 돌려봄, albumentations 추가 했으나 성능차이는 그대로, Normalize 값 조절하면서 사진의 밝기를 맞춰봄

<br>

## 회고록

Inception으로 돌려봤는데, 점수가 너무 낮게 나와서 뭐가 문제일까 고민해봤다. Data 문제라고 생각하고 Albumentations을 사용하여 data에 변형을 줘보았고, Normalize 값을조절하면 사진의 밝기를 맞춰봤지만 결과는 큰 차이가 없었다.

아직 어떤 부분이 중요한지 핀트를 못잡는 것 같다. 

우선 우리팀에 도움이 될 수 있는 다른 idea를 고민해봐야겠다. 당장 내가 할 수 있는 일을 찾아봐야겠다.

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

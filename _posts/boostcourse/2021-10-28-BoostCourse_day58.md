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

title: "[boostcourse] Day58 학습기록_팀명뭘로하조"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - daily
tags:
  - []
date: 2021-10-28
last_modified_at: 2021-10-28
---

## 학습 내용

- Cutmix Test 진행

<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 홍요한

참가자 : 박범수, 박준혁, 서희수, 한건우, 홍요한, 황원상, 조혜원

<br>

### 대회 진행

- 범수님 :
    
    dense CRF 사용 → 잘되는 이미지도 있고, 안되는 이미지도 있음
    
- 준혁님 :
    
    HRNet OCR 성능이 잘안나옴 → lr 줄여서 Test
    
    lr 줄여서 사용해도 수렴은 되지만 점수가 낮음
    
- 원상님 :
    
    mmseg mmcv, cuda 환경설정 공유
    
    swin-b : 전체 데이터 학습 0.733 1등 달성 -16시간정도 소요됨,
    
    추가적으로 seed 바꿔가면서 시도 해보기
    
- 요한님 :
    
    cutmix로 metal, glass, battery, clothing 추가 시 LB 0.02 상승
    
    model visualization 구축 후 공유 예정(confusion matrix, pred_mask image) with 희수님
    
- 희수님 : soft voting 완성해봤는데, Hard voting 도 시도해볼예정

원상님 swin-B로 dense CRF 적용



```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

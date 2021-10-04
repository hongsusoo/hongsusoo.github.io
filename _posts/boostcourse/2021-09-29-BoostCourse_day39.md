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

title: "[boostcourse] Day39 학습기록_팀명뭘로하조"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - daily
tags:
  - []
date: 2021-09-29
last_modified_at: 2021-09-29
---

## 학습 내용



<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 황원상

참가자 : 박범수, 박준혁, 서희수, 한건우, 홍요한, 황원상, 조혜원

<br>

### 토의 내용

- Bag of Freebies
    
    Inference 중에 추가 계산 비용을 발생시키지 않으면서 object detection네트워크의 성능을 향상시키기 위해 조합하여 사용할 수 있는 여러가지 기법들을 통칭
    
- Object Detection 앙상블
    
    WBF(Weighted Box Fusion)
    
    예측의 일부를 단순히 제거하는 NMS, Soft-NMS extension과 달리, WBF는 부정확한 상자를 제외하지 않고, 모든 예측된 사각형을 사용하므로, 결합된 사각형의 품질이 크게 향상될 수 있습니다.
    
- mmdetection custom방법들

- DarkNet
    
    - Yolo 에서 사용한 Library 이름(C언어로 작성된 물체 인식 오픈 소스)
    - Yolo 에서 사용한 pipline model 이름

## 회고록

YOLO V1 논문을 실제로 읽다보니, 블로그나 강의를 보면서 느낌으로 이해했던 내용들과 실제 내용에 차이가 있었다. 느낌을 가져가는 건 좋지만, 그걸 맹신하면 안될 것 같다. 공부하면서 끊임없이 수정/보완 해야할 것 같다. 

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

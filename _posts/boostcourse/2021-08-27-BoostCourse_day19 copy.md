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

title: "[boostcourse] Day19 학습기록_minibatch28"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - daily
tags:
  - []
date: 2021-08-27
last_modified_at: 2021-08-27
---

<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 박마루찬

참가자 : 강재현, 권예환, 김준태, 박마루찬, 서광채, 장동건, 홍요한


<br>

### 대회 진행상황 공유

- 강재현 : 광채님 데이터셋 사용 (validation accuracy 변화 확인)

(배치 사이즈, learning rate 어떻게 쓰세요?) (광채님 - TTA 시간 얼마나 걸리시나요?)

- 권예환 : Transform - Resize, gray 적용했음, 큰 변화 확인(뭐 때문인지는 모름), 모델 변경, Validation 도입.
- 김준태 : 오버피팅 발생, ViT 시도, acc 80%(잇다가 제출해볼게요), validation 도입, 크롭, early stopping 적용 예정
- 박마루찬 :  추가 데이터 작업과정 공유
- 서광채 : 코드 간결하게 모듈화 하였음. 과거에 모델 훈련 과정에 문제 수정하여 다시 시도(learning rate 너무 낮게 했음), b7은 pretrained 모델
- 장동건 : 광채님 데이터셋 코드 사용했는데, validation에 문제 있어 보임. auxiliary 도입 중
- 홍요한 : 광채님 데이터셋 코드와 현재 코드를 합치고 있음. 토론 게시판에 공유된 facenet 사용해서 훈련해보려고 함.

<br>

### 건의사항

- 슬랙에 val set 나누는거 공유
- 모듈화 - 각자 코드를 오늘 업로드 될 베이스라인에 맞춰서 작성하고, 다음주에 합쳐봐요

<br>

## 회고록

광채님이 만들어주신 dataset & dataloader부분을 사용하니 score가 기존 최고 0.4481에서 0.7348까지 올랐다. 

크게 변경된 부분은 아래 3가지가 있는데, 추가적으로 test를 해봐야할 것 같다.

1. data 순서 : 사람을 기준으로 training
2. validationset 구성 : 사람 기준으로 구분
3. batch size : 32 -> 4

그리고 FaceCropNet을 함수화하고 있는데, 주말에 training 시켜서 성능이 얼마나 개선됐을지 확인해봐야겠다.

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

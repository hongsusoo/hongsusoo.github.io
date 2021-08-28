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

title: "[CV Project] 마스크 착용 상태 분류 - check Point 정리🌓"
excerpt: "about : Image Classification Competition"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - AI_project
tags:
  - [CV, Modeling, Pstage-01]
date: 2021-08-26
last_modified_at: 2021-08-26
---

<br>

# Model 구현시 check 사항 정리

<br>

## Problem Definition

1. Target 설정

2. Data 분석
  
  - 데이터 형태 확인
  - 분포 확인

3. Target을 도출하기 위한 Data `약점`을 파악

  - 약점 : Data 불균형, Data 수, Data Miss Matched, Data 누락&훼손

4. Data를 보완할 만한 기법 고민

  - Augmentation 방법 설정, Transform, batch Size 

<br>

## Data Augmenetaion


### 외부데이터 사용

- Kaggle, Dacon 등 외부 대회에서 사용한 Public DataSet 사용

### transform 

1. cutmix -> Cut mix의 경우
2. randaug(albumentation하고는 조금 다름)
3. randerase (50% 일 때 잘 동작)
  -> 쓸만한 거 2~3개 정도 추려서 사용

<br>

## Hyperparameter

### Batch Size

- 커질 수록 `sharp` 하게 수렴, 작아질 수록 `flat` 하게 수렴 
- Batch Size가 작아지면 전체 Data에 대한 설명하는 부분이 작아지기 때문에 Noise가 발생하고, Local minimum에 조금은 더 둔감해짐
- Batch Size가 커지면 전체 Data에 대해서 상대적으로 설명을 잘하기 때문에 Noise가 적어짐
- 작으면 `underfitting` 가능성이 높아지고, 클 수록 `Overfitting` 가능성이 높아짐

### Learning Rate

- scheduler를 활용하여 Learning Rate를 변경하여 사용할 수 있음
- ex : `scheduler = optim.lr_scheduler.CosineAnnealingLR(optimizer, T_max=10, eta_min=0)`

<br>

**📌reference**
- boostcourse AI tech


<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

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

title: "[CV Project] 마스크 착용 상태 분류 - DenseNet 제출🌓"
excerpt: "about : Image Classification Competition"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - boostcourse
tags:
  - [CV, Modeling, Pstage-01]
date: 2021-08-26
last_modified_at: 2021-08-26
---

<br>

# Model 구현

- Model : DenseNet(pre-trained)
- Batchsize : 32
- Learning-rage : 1e-4
- loss : CrossEntropyLoss
- optimizer : Adam

**🎈 acc : 60.5 / f1 score 0.448**

<br>

## DenseNet 선택이유

- Input Data의 정보가 깊은 Layer까지 전달됨
- Dense connection이 regularizing 효과가 있어 적은 데이터 셋에도 과적합을 줄임
- 현재 Dataset의 분포 불균형이 심하기 때문에 불균형된 Class간의 학습 정도를 조절하는게 중요하다고 생각함

## 회고 

- 아직 어떤 factor가 f1 score에 제일 민감하게 반응하는지 파악이 안됨
- 구현 자체가 익숙하지 않아 model 이외의 다른 부분에 신경을 못씀
- 추가적으로 몇까지 모델을 구현해보며 익숙해지는게 우선

<br>

**📌reference**
- boostcourse AI tech


<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

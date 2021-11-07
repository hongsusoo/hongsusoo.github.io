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

title: "[boostcourse] Day12 학습기록_minibatch28"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - daily
tags:
  - []
date: 2021-08-18
last_modified_at: 2021-08-18
---
<br>


## 학습 내용

<a href="https://hongsusoo.github.io/ai_dlbasic/dl_pytorch_autograd_optim"><img src="https://img.shields.io/badge/-Auto Grad & Optimizer-red"/></a> 
<a href="https://hongsusoo.github.io/ai_dlbasic/dl_pytorch_dataloader"><img src="https://img.shields.io/badge/-dataset & dataloader-red"/></a> 

<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 박마루찬

참가자 : 강재현, 권예환, 김준태, 박마루찬, 서광채, 장동건, 홍요한

<br>

### 질문사항

- Q

      gather나 scatter의 작동 원리

  A

      다들 어려움, 과제 풀이 시간 참조

<br>

### 모델 코드 리뷰

- alexnet for cifar 10

  1. pretrained 모델 구조 모사하기 위해 average pooling 추가

  2. momentum 사용했는데 잘 안 돼서 adam 사용 (batch size가 작아서 그럴 수도 있음)

  3. training loss가 줄어도 과적합이 일어나지 않는 점이 인상적이었음

<br>

### 건의사항

- 멘토링 질문 : 이미지 분류 대회 협업을 어떻게 할 수 있을까요?

<br>

## 회고록

어제 다짐한게 하루만에 무너졌다. 욕심을 버리고 당장 이해 안되는 부분을 놓아야 하는데, 끝까지 붙잡고 놓지를 않아서 다른 일들이 더 밀려버렸다. 하루씩 할 일들이 미뤄지니 마음도 조급해져서 코어타임 시간에 집중이 안되는것 같다.

멘탈이 조금씩 흔들리는데, 오늘은 멘탈 회복을 위해 부족했던 수면 시간을 채워야겠다.



<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```


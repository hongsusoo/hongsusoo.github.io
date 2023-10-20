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

title: "[boostcourse] Day27 학습기록"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - boostcourse
tags:
  - []
date: 2021-09-08
last_modified_at: 2021-09-08
---

## 학습 내용

- <a href="https://hongsusoo.github.io/dl/dl_image_augmentation"><img src="https://img.shields.io/badge/-image augmentation-red"/></a>

<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 배지연

참가자 : 박승찬, 한건우, 배지연, 강재현, 오하은, 홍요한

<br>

### 토의 내용

#### 과제 1

- Augmentation 적용

    → 홍요한님 : GaussianBlur

    → 배지연님 : ColorJitter

    색상 조정은 효과가 없는 거 같다. (이미지가 흑백이라서?)

    → 강재현님 : Shiftscalerotate, cutout

- Resize 순서를 바꾸면 에러가 난다

    → Pil image를 batch로 바꿀 때 collate_fn 에러 → ToTensor 추가

    → Totensor 추가했을 때 이미지가 찍히지 않는 문제는 transpose나 permute로 해결

- log soft max에서 중첩되는 값이 어떻게 보존될 수 있을까?

    → soft max()를 취하고 log를 취하므로 - 더라도 값을 가질 수 있음

- soft max에서 학습이 안 됐던 문제

    → log max, soft max를 혼용해서 중첩된 부분이 보존되지 않음

#### Data Augmentation Further Question

1. Quickdraw datatset에서 blur augmentation이 성능 향상에 도움이 되는 이유
2. blur augmentation에서 Resize(224,224) 방식이 작은 원본이미지를 사용하는 것보다 성능이 낮은 이유
    1. overfitting을 방지하기 위해서 사이즈를 줄인다?
    2. 작은 거에서 blur를 먼저 처리하고 resize하면 blur의 효과가 별로 없을 거 같다?
        1. blur는 선모양으로 펼친다?
    3. 인접 픽셀간의 차이가 완만한 편인데 이를 resize하면 날카로워진다.⭐
        1. 날카로울수록 blur가 세게 들어간다.
3. augmentation의 순서에서 blur→ resize 와 resize→blur가 성능이 어떻게 다른지 비교
(Geometric augmentation)의 경우에도 순서가 어떻게 영향을 미치는지
4. augmentation을 적용하더라도 conv layer를 고정하고 linear classifier만 새로 학습하는 fine-tuning을 수행하면 효과가 떨어질 수 있는 이유

#### 과제

- encoder에 input을 어떻게 넣는지? @배지연님

    → OOP, nn.module 동작 과정 한건우님이 설명

- loss를 어떻게
- target과 label은 한칸 차이 (다음에 무엇이 올지 예측)

#### 멘토님께 질문

1. 현재 코드는 `train`, `dev`, `test` 데이터를 모두 dictionary 에 포함하고 있습니다. 이때 발생할 수 있는 문제점은 무엇일까요?
2. 1에서 발생한 문제점을 해결하기 위해서는 어떻게 바꿔야 할까요?

[토론내용]

1. index가 있는 것만으로도 문제가 될까?

> apple이 0번이 아닐 수 있음. dict에서 선언해주는 것이므로 index가 밀리는 것일 뿐 다른 의미가 없지 않을까?

> 안 나왔던 단어가 나왔을 때 이상상황으로 인지해야하는데, 이상점을 느끼지 못 하지 않을까?

> 추가 데이터 작업과정에서 문제가 생기지 않을까?

> **새로운 데이터가 들어오면 out of range가 궁금합니다!!**

> (멘토님께 콜)


Q. Quick draw dataset은 흑백인데 채널이 3차원 입니다. 차원 별로 출력해보니까 색이 바뀌면서 나오는데 인터넷 찾아봐도 흑백은 1차원 채널이라고 나오는거 같은데 다른 분들 의견이 궁금합니다.

A. image load시 grayscale임을 명시해 주지 않을 경우 3채널 이미지 형태로 읽어오게 됩니다. (cv2.imread의 경우, cv2.IMREAD_COLOR/cv2.IMREAD_GRAYSCALE/cv2.IMREAD_UNCHANGED 3가지 옵션이 있음)
이유는 이미지 파일 포맷의 경우 기본적으로 컬러를 기반으로 저장하기 때문에 파일을 읽어올때 헤더에 정보가 없으면 grayscale인지 알 수 없습니다. 일반적으로 3채널 color 이미지로 읽기 때문입니다. 각 채널 별로 컬러채널 값이 있는 이유는 grayscale 이미지 저장시 각 컬러 차원이 인간의 눈에서 밝기에 미치는 영향에 따라 저장되기 때문에 그렇습니다( YUV 색공간 사용)


<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

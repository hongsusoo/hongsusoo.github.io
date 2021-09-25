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

title: "[boostcourse] Day25 학습기록"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - daily
tags:
  - []
date: 2021-09-06
last_modified_at: 2021-09-06
---

## 학습 내용

- Image Classification
- Image augmenation


<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 박승찬

참가자 : 박승찬, 한건우, 배지연, 강재현, 오하은, 홍요한

<br>

### 토의 내용

- require_grad까지 출력되게 해주는 거 궁금
- maxpooling에서 parameter를 가져오는지 궁금
- fine_tuned_train_log.csv으로 바꿔야 한다.
- 취업을 위한 도메인 선택
    - **추천**이 산업에서는 강세인데 이미지를 이용해서 추천을 잘 안한다.
    - 이상탐지가 인기가 많다.
    - segmentation과 object detection이 그 다음으로 높다.
    - 자연어는 시계열 데이터이므로 용이한 거 같다.
    - 이상치랑 시계열 데이터가 취업이 잘 된다.
- segmentation의 산업에서의 사용
    - 현차에서 직접 개발하는 것은 꺼린다.
    - segmentation보다는 lidar를 사용한다.
        - 라이드플럭스에서 사용한다
- 모델러는 갈 곳이 없다.
- 타 부캠에서는 엄청 깊게 들어간다.
    - 예를 들어 CrossEntropy를 일주일동안 공부
        - 중도 포기하는 사람이 많았다.
    - 네이버 부스트캠프는 keyword를 던져주는 느낌
- FCN (Fully Convolutional Network)


Q. 모델 구조 출력 시 requires_grad 출력 방법

<br>

A.

```python
print(f'[layer_name]\t\t[requires_grad]')
for name, param in model_finetune.named_parameters():
    print(f'{name: <20}\t{param.requires_grad}')
```

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

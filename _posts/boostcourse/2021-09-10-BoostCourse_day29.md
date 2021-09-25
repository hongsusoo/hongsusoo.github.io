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

title: "[boostcourse] Day29 학습기록"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - daily
tags:
  - []
date: 2021-09-10
last_modified_at: 2021-09-10
---

## 학습 내용

- <a href="https://hongsusoo.github.io/ai/objectdetection_model"><img src="https://img.shields.io/badge/-object detection-red"/></a>

<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 오하은

참가자 : 박승찬, 한건우, 배지연, 강재현, 오하은, 홍요한

<br>

### 토의 내용

Q. Faster RCNN에서 Classification에 대한 loss는 어떻게 계산될까요?

A. BBox에 대한 Classification이기 때문에 BBox에 들어가 있는 class와 GT의 Class를 비교하여 loss를 산출

<br>

### 멘토링

#### Q & A

Q: background를 augment하면 실제 object에 대해서는 학습을 못할 텐데 focal loss로 가는 것이 맞는지

초기 학습이 많이 진행되지 않았을 때 object가 detect되지 않고 background가 detect된다. 

A: yolo에는 object detect loss가 있다. grid를 나가면 loss가 커진다.

Q: Image Segmentation에서 classifier weight를 FCN에 shape만 맞춰서 복사했는데 어떻게 저게 segmentation이 되는걸까요?

A: Visualization 할 때도 비슷한 테크닉을 사용한다. 몇픽셀 shift해서 진행해도 그 위치를 따라가는지 실험해보면 좋을 것 같다!

Q: Fully connect layer의 weight가 어떻게 위치 정보를 갖고 있는지 궁금하다!

A: 멘토님이 조금 더 확인해 보시고 답변해주신다고 합니다!

Q: 스타트업에서 pretrained 모델을 그냥 가져와서 사용하는 경우가 많아서 회의감이 많이 들었는데 멘토님 회사에서도 하는지 궁금

A: 직접 개발하는 것도 중요하지만 pretrained model을 통해서 해결이 가능하면 이것을 사용하는 것도 좋을 거 같다. 

구현체가 존재하는지가 중요하다. 이 코드를 기반으로 학습을해서 서비스화한다.

Q: 코드를 미리 알고 미리 까보면(reference보기) 개선사항을 알 수 있었을 텐데

면접 질문등을 

A: 궁금해서 까본 적은 없지만, 까야되는 상황이 생긴다. 소스코드를 통해서 많이 배운다.

구글링은 결과만을 알려주는데 소스코드를 보면 과정을 배울 수 있다. 코드 짜는 것, CS적 지식을 많이 배울 수 있다. 깃헙에 있는 코드는 안 좋은 코드들도 많은 데 소스코드들은 좋은 거 같다. 좋은 코드를 보면 많이 배운다.

논문에서 이해가 잘 안되었지만 코드로는 한 줄인 경우가 있다. 

면접은 전략적으로 준비하자

(멘토님은 backpropagation을 칠판에 다 적으신 경우도 있다.)

Q: 개발 분야가 다양하신데 기존에 공부를 다 하신건지 아니면 회사에 가서 하게된건지 궁금

A: 멘토님 성향이 얕고 넓은 것을 좋아하신다.


#### CV쪽으로 어떻게 취업할 수 있는지

- 비전이 취업이 안된다 == AI 전체가 취업이 안된다라고 생각한다.
- GAN쪽이 살아남기 어려운 이유는 돈이 안 되게 때문
- CV가 도메인이 많은 거 같다.
- 추천도 잘 나간다
- CV가 근본이라서 충분히 괜찮지 않을까 싶다. (CV는 삼성같은 느낌)
- NLP가 훨씬 제너럴하게 사용될 수 있을 거 같긴하다.
- NLP를 product에서 사용하기에는 비싼 거 같다.
- 요즘 Transformer로 대동단결되는 느낌이기 때문에 뭐든지 하나를 잘 하면 된다고 생각한다.

처음부터 완벽하게 하려고 하지 말고 계속 생성하다보면 알게 될 거다.


<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

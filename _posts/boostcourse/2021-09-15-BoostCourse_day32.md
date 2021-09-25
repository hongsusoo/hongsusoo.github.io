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

title: "[boostcourse] Day32 학습기록"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - daily
tags:
  - []
date: 2021-09-15
last_modified_at: 2021-09-15
---

## 학습 내용

- <a href="https://hongsusoo.github.io/ai/conditionalgenerativemodel"><img src="https://img.shields.io/badge/-Conditional GAN-red"/></a>
- [필수 과제 4] Conditional GAN

<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 한건우

참가자 : 박승찬, 한건우, 배지연, 강재현, 오하은, 홍요한

<br>

### 토의 내용


Q. GAN PDF 자료 31 page에 나온 perception 관련 내용에서, 위에껀 Edge를 뽑아내는거고, 그 아래는 방향성, 오른쪽 밑에는 color의 difference를 구별하는 filter에 대해서 설명해 주셨는데 이 부분은 직관적으로 생각해볼 수 있는 부분일까요?

![image](https://user-images.githubusercontent.com/77658029/134762691-d52a3707-e355-4bb1-9b49-af69cc49de7d.png)

A. 
일반적으로 3x3 filter를 쓰는데 과제에서 filter size가 큰 것같다
→ Alexnet의 첫번째 layer의 시각화 이미지로 보임
 + image pretrained된 VGG16, VGG19를 통상적으로 많이 사용함

---

Q. GAN에서 아래와 같이 loss 값을 사용해도 문제 없을까?(기존엔 crossentropy의 log형태)

![image](https://user-images.githubusercontent.com/77658029/134762765-d6e01287-a1fe-4f1a-b660-9af7097d6d23.png)

A.
- 확률값이 1을 넘어설 수 있음.
- fake label은 값이 처음부터 0이므로 첫번째 항의 값이 항상 0이 되므로 discriminiator가 fake에 대한 학습이 안 되지 않을까?
JSD를 쓰면 log(-4)에 수렴하는데 값의 비교(유도)가 필요할 것으로 보임
- MSE의 문제점인 과적합이 계승될 가능성이 있음
L1 loss, L2 loss의 문제. manifold가 평면이 아니므로 펴보면 먼 거리인데 MSE로 계산된 값이 정확한 값이 아닐 가능성이 높음
log를 적용하면 실패했을때 -∞로 떨어지는데 MSE로 하면 변동값이 log보다는 작지 않을까?

<br>

### 멘토링

- object detection 대회를 진행해서 object detection을 공부하려고 하는데 무엇부터 시작하는 것이 좋을지
    - YOLO를 많이 사용할 거 같아서 YOLOY를 보면 좋을 거 같다.
    - 하나씩 꼼꼼하게 보면 시간이 오래 걸릴 것이다.
    - PR12 YOLO 관련 유튜브 한번 보고 대회 참가하면 도움이 될 거 같다
        - [https://www.youtube.com/watch?v=eTDcoeqj1_w](https://www.youtube.com/watch?v=eTDcoeqj1_w)
        - [https://www.youtube.com/results?search_query=pr12+yolo](https://www.youtube.com/results?search_query=pr12+yolo)
- 멘토님께서 보시는 repo중에서도 timm처럼 object detection관련해서 pretrained된 것을 사용하는 것이 있는지
    - [https://github.com/AlexeyAB/darknet](https://github.com/AlexeyAB/darknet)
- Detection 빡세다.. data가 말이 안된다..
    - 첫 입문하는 사람들에게 안 맞을 수 있다.
    - vision으로 풀 수 있는 문제인가 싶은 data들도 있다.
- PR[숫자]에서 숫자가 뜻하는 의미는?
    - 시즌
- 다음 대회관련 조언
    - 쓰레기 분류 문제
    - MNMS?를 통하게 되면 후처리를 못 하게 되는 경우가 있다.
    - YOLO가 1stage가 핫하다
    - Fast R-cNN도 좋지만 YOLO만 알면 다 알 수 있다. ⇒ YOLO쪽만 열심히 보면 된다.
    - 관련 기술들을 간단하게 알고 있자.
    - 기술을 사용해보고 간단하게 구현해보자.
    - score보다는 detection에 함류를 한번 해보겠다는 마인드로 참가하자
- 시각화 현업에서 중요한지 궁금
    - vision자체가 시각화여서 따로 시각화를 많이 해본적은 없으시다.
    - 시각화 자체를 잘 하는 것보다는 시각화 관련된 tool을 잘 사용하는 것이 좋지 않을까
- object detection을 paper with code에서 보고 논문을 읽고 있는데 일단 semi-supervised learning을 사용하고 있다. 논문과 paper with code를 얼마나 믿을 수 있는지 궁금하다.
    - 탑 티어에서 publish한거면 믿을 수 있지만 아카이브에서 나온것은 신빙성이 조금 떨어질 수 있다.
    - 논문을 보다보면 비판적으로 보게 된다. (맹신보다 좋은 거 같다.)
    - 저널에서 공개된 것이며 믿을 수 있을 것
    - 코드와 pretrained된것까지 돌려보면 좋은 거 같다.
    - 예전에 Trans GAN관련 논문을 봤는데 작성자가 중국인였는데 논문을 작성해놓고 코드를 작성하고 있었다...ㅋㅋ
- 깃헙 repo에 issue남기는 거 좋은 거 같다.
- 멘토님은 transformer가 inductive bias가 적어서 좀 더 학습이 잘 된다는 의견에 대해 어떻게 생각하시는지
    - inductive bias가 적다: CNN에서 receptive field에 큰 영향을 받아서 이것이 없는 모델 구조가 좀 더 deep하게 쌓으면 성능이 오를 수 있다고 말한다.
    - 건우님도 최근에 transformer모델을 사용해보셨는데 학습이 잘 안되셨다.
    - 멘토님: transformer가 일단 dataset이 엄청 많고 오래 학습해야지 성능이 좋게 나오는 거 같다. 썰이기 때문에 엄청나게 큰 이슈일지 잘 모르겠다. 도움은 될 수 있지만 critical하지는 않은 거 같다.
- Detection은 속도도 중요하다
    - 대회하면 앙상블 많이 하는데 속도가 많이 늦어져서 실제로는 잘 사용하지 않는다.
- 개인 프로젝트를 진행할 때 data를 직접 구하는 것이 신빙성이 있는지 궁금하다.
    - 예: CV이면 직접 촬영, nlp면 문자를 직접 구함
    - 멘토님: 모델의 성능이 잘 나왔다면 신빙성은 따라오는 거 같다.
    - 저작권 이슈만 조심하면 될 거 같다.
- MSE Loss를 GAN에 적용과 관련된 블로그(LSGAN): [http://jaejunyoo.blogspot.com/2017/03/lsgan-1.html](http://jaejunyoo.blogspot.com/2017/03/lsgan-1.html)
- 지연님: 미래에 어떤 특징을 가질 것이다가 분명하지 않은 경우에 이를 추측하는 것이 CV로 접근하는 것이 괜찮은지 궁금하다
    - loss를 어떻게 설계하냐에 따라 달라질 거 같다.
    - supervised learning이 되려면 정답이 unique해야 한다.

<br>


```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

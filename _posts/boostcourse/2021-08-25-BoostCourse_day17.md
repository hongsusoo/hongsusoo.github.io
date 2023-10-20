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

title: "[boostcourse] Day17 학습기록_minibatch28"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - boostcourse
tags:
  - []
date: 2021-08-25
last_modified_at: 2021-08-25
---
<br>

## 학습 내용

<a href="https://hongsusoo.github.io/ai/proj_ImageClassify02"><img src="https://img.shields.io/badge/-Dataset-red"/></a> 

<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 권예환

참가자 : 강재현, 권예환, 김준태, 박마루찬, 서광채, 장동건, 홍요한

<br>


### 질의응답

- 모델이나 다른 건 안 건드렸는데 Out of memory가 떴습니다.

→ kernel이 다른 게 켜져있는게 있는지 확인 or restart 추천

- 학습 시 epoch 마다 확인하려고 tqdm 썼는데 에러가 났습니다.

→ tqdm.tqdm으로 사용해아 함. 그냥 tqdm 아님

<br>

### 대회 진행상황 공유

- 권예환

     : 모델 pipeline 구성 완료, Data augmentation 집중 예정

- 박마루찬

     : validation set의 정확도를 맞추기 위해 random split 부분에 대해, validation set에 들어가는 사람과 training set에 들어가는 사람이 완전히 구분되게 하는 아이디어를 적용함. 이로 인해 validation accuracy가 예측치대로 잘 나오는 것을 확인

    : focal loss 활용

- 강재현

     : mask, 성별, 나이를 다 따로 하는 걸 도전, albumentation 썼지만 성능이 안나오는 부분도 있어 확인 필요

     : validation이 98% 이런 식으로 많이 높게 나왔는데 마루찬님의 아이디어를 참고해 수정할 예정

     : 사람이 봐도 구분을 못하겠는 image가 많다. 특히 나이가 구분이 안된다. mask는 잘 잡는다.

     : ViT도 돌려보고 다른것도 돌려봤지만 efficientNet이 가장 좋았다.

     : cross entropy에서 weight를 줬다. lr.scheduler() 사용했더니 성능 오름

- 홍요한

     : DenseNet161 사용, 전체 pipeline 구축하고 제출해서 accyracy 60% 확인. 

     : model을 inception으로 바꾸고 batch size도 조절해가며 training중

- 장동건

     : 모델을 돌려서 제출을 목표로 함. inception_v3 사용. 

- 김준태

     : labeling 완료, resnet18 사용, 정확도 46% 정도 확인

     : 뒤에 inception_v3를 돌렸더니 40%가 나와서 버림, model 완성 시키는 걸 목표

- 서광채

     : nfnet, efficientNet_b7등 다양한 모델을 사용해봄, 처음부터 학습시키는데 epoch당 시간이 너무 걸려 학습이 오래 걸렸다. 

<br>

## 회고록

팀원들의 model을 참고하여 DenseNet으로 첫 구현하여 제출을 시도했다. 제출은 했는데 이 다음 무엇을 시도해봐야할지 판단이 안서는것 같다. 아직도 흐름을 못잡는것 같고 익숙하지 않은 것 같다. 

다른 모델로 바꿔서 일단 Model 구축하는 것에 익숙해 질 수 있도록 inception model로도 구현해서 돌려봐야겠다.


<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

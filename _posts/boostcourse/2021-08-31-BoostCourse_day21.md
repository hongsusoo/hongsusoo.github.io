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

title: "[boostcourse] Day21 학습기록_minibatch28"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - daily
tags:
  - []
date: 2021-08-31
last_modified_at: 2021-08-31
---

<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 장동건

참가자 : 강재현, 권예환, 김준태, 박마루찬, 서광채, 장동건, 홍요한


<br>

### 대회 진행상황 공유

- 강재현 : mobileNet 사용, TTA 반영 후 hard voting으로 진행했으나, LB점수는 떨어짐, multi-sample drop out도 적용했는데, drop out 확률을 적절히 조정해야 할 듯(0.25 정도), loss function은 f1-loss가 잘 나오는 듯.
- 권예환 : stratification 적용, 학습 과정에서 문제 발생
- 김준태 : baseline으로 train할 때 batch_size 높게해도 잘 학습이 된다. → resize옵션 문제일 듯, DenseNet 학습 시도, 앙상블 모델의 경우 soft-voting이 좋을 듯
- 박마루찬 : 추가 데이터 반영 후 학습 시도(10% 추가), 추가한 데이터의 나이 불균형이 심함.
- 서광채 : efficientNet 최고 점수 받은 모델 재현 시도 중..
- 장동건 : mixup 진행 중, loss 구하는 방법에 대한 issue(train 과정에 개입해야 함.)
- 홍요한 : cutmix 진행 중, 자른 이미지에 대한 labelling 문제, 인물 이미지를 나이들게 만들어주는  모델(더 찾아볼 예정)

<br>


## 회고록


오늘은 cutmix를 도전하기 위해 code를 분석해보았다. 생각보다 code는 어렵지 않았지만, labeling 처리하는게 생각보다 까다로웠다. 기존의 one hot 방식으로 처리되었던 labeling을 확률에 비율을 더해서 계산해야하보니 이런 부분들을 어떤식으로 가져가야 좋을지 고민을 많이 했던것 같다. 

그리고 focal loss에 대해서 공부해보니, 이게 기존 cross entropy를 변형하여 overfitting에 강력한 loss라고 했다. 그 원리를 공부하다 보니 이번 대회에서 문제가 되고 있는 overfitting을 조금 막을 수 있을것 같다 생각이 들어서 focal loss를 좀 변형하여 사용해 보았다. 결과는 조금 떨어졌는데, 이유는 아직 정확하게 파악이 안되어서,, 일단 좀 더 사용해봐야겠다. 


<br>

🥄 오늘의 시도

9번째 제출

  - overfitting의 문제를 줄이기 위해서 new focal loss를 만들어봄
  - New Focal loss는 학습이 된 애들은 그대로 두고 학습이 덜된 애들을 더 학습 시킴
  - Face Crop을 활용하여 위에 동일한 상황에서 Test 진행
  - New Focal loss사용
  - batch size 4
  - optim : Adam
  - loss : New Focal loss
  - lr : 1e-4
  - 3 epoch
  - test acc : 81.0

![image](https://user-images.githubusercontent.com/77658029/133977049-839ff19e-ff60-438e-989e-fcda2ada6c3a.png)

결과
  - f1 : 0.6676
  - acc : 76.8730%


10~12번째 시도는 하나씩 빼먹고 run를 돌림...


13번째 시도

  python train.py--epochs 10 --augmentation AlbuAugmentation --model imgInceptionV3 --criterion new_focal --lr 1e-4 --batch_size 16 --valid_batch_size 64 --dataset datasetSplitByClasses --optimizer Adam --cutmix True --resize 299,299

  - base : pretrained inceptionv3
  - val acc : 0.93571
  - f1 score : 0.9718
  - epoch :  5
  - batch : 16
  - loss : focal loss 수정
  - lr : 1e-4
  - optim : Adam
  - seed = 42
  - Data augmentation:
    - facecrop [310,310]
    - resize [299, 299]
    - Normalize mean = (0.548, 0.504, 0.479)
    - Normalize std = (0.237, 0.247, 0.246)

dataset : 사람 기준으로 나눠서 class 별로 비율나눠서 input

classifier 사용 x, Adam, cutmix 추가(np.random.random()>0.5), faceCrop 설정(이전까진 미설정되어있었음...)


결과
  - f1 : 0.6820
  - acc : 75.67%


<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

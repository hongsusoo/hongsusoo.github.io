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

title: "GoogLeNet model Introduction"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - AI Model
tags:
  - [googlenet]
date: 2021-08-19
last_modified_at: 2021-08-19
---

<br>

# googLeNet(Going deeper with convolutions)

- code name : Inception
- ILSVRC 2014 1등 모델
- 연구팀인원 대부분이 구글 사람
- 특징은 1x1 conv 사용 및 layer 깊이를 늘림
- Embedded나 Mobile에서도 사용 될 수 있도록 가볍게 만들기 위해 노력했다고 함


<br>

## GoogLeNet 구조

- stem
- Inception(NIN, CCCP, Pooling)
- Classifier

![image](https://user-images.githubusercontent.com/77658029/130167521-4e5288e0-edc0-4190-8f9a-540cbeec5c33.png)


<br>

## GoogLeNet 탄생 배경

**🚨 기존 CNN의 문제점**

- CNN의 성능을 높이기 위해서는 크기를 키우면됨
- Layer를 늘려서 깊이를 늘리던, Width를 키우는 방법(고품질의 이미지를 잘게 쪼게는 방식, 이 부분 이해가 안됨)
- 하지만 두 가지 모두 Parameter를 키우기 때문에, overfitting 발생할 수 있고
- 학습할 parameter가 많아지니 computing 자원이 많이 들어가게 됨

- 위 두 가지 문제를 해결하기 위해 Fully Connected 구조에서 Sparsely Connected 구조로 바꾸려는 시도가 있음

![image](https://user-images.githubusercontent.com/77658029/130173370-ece0a692-45d7-48e0-8382-301e58494b4b.png)

- LeNet에서도 sampling을 통한 연산으로 이런 부분을 해결하려고 함

![image](https://user-images.githubusercontent.com/77658029/130173435-f4d55202-5123-4a5f-bfc7-f6f19e771b4e.png)

하지만, 오늘날 컴퓨터는 sparse data 구조를 만들때 비효율적임, 

<br>

**💡GoogLeNet의 시작**

- Inception은 이런 sparse 구조를 실험하기 위해 만들기 시작했다고함

![image](https://user-images.githubusercontent.com/77658029/130173746-a12c6ecf-1b41-4c0a-b72f-fede17cb83d8.png)

- 그래서 제안된것이 여러 사이즈의 convolution 연산을 사용하여 상대적으로 작은 영역부터 큰 역영에 대한 object 정보를 유지할 수 있게 됨


💡 알쓸신잡

1. 1x1 Convolution(Conv1x1) : 연산도 간단하고 픽셀마다의 피쳐를 계산해서 최대한 정보를 보존
2. MaxPooling : 연산량을 대폭 줄여주어 cost도 절약되고 overfitting도 줄여줌 
3. nxn Convolution

위 세 가지를 어떻게 합치면 좋을까?

![image](https://user-images.githubusercontent.com/77658029/130168355-6c0523b8-6a70-491a-85c9-a7f4d6f36c58.png)

![image](https://user-images.githubusercontent.com/77658029/130168450-7f9f4b94-a259-4802-9af5-7af6aae248f6.png)

![Image출처](https://memegenerator.net/instance/81736096/leo-deeper-we-need-to-go-deeper-deeperer)


<br>

## inception

- Googlenet을 만드는 기초적인 블럭
- feature map을 효과적으로 추출할 수 있도록 1 x 1, 3 x 3, 5 x 5 convolution 연산
- Conv연산, Pooling으로 이뤄지고, 각 연산 후 Depth방향으로 붙여줌
- Conv연산 시, 높이와 폭을 맞추기 위해 Padding도 진행됨
- Conv 연산 후 ReLU를 통해 비선형적 특징을 더 추가해줌

![image](https://user-images.githubusercontent.com/77658029/130168071-08076b41-c4fe-4ae1-a89d-db657448fa47.png)

<br>

### NIN(Network In Network)

- LeNet CNN의 표준 구조로, Conv후 FC layer가 뒤따라오는 형태로 되어있음
- NIN은 전체 network안에 micro network으로 구성됨

![image](https://user-images.githubusercontent.com/77658029/130164528-b76c6ea5-09ca-437d-96e7-e82c43ae0400.png)

- NIN 논문에서는 이런 Network 안에 Network에 대해서 설명하고 있음
(이 논문에서 inception이라는 말이 나오는데 이것은 영화 Inception을 모티브로 했다고 함, 
영화 Inception 중 "we need to go deeper"라는 대사가 있음)
- NIN은 신경망의 표현력을 높이기 위해 제안된 방법론(1x1 convolution추가, ReLU activation 사용)

<br>

### CCCP (Cascaded Cross Channel Pooling)

- Channel를 가로질러(Cross) Pooling 연산을 진행하는 방법
- 이 방법이 1x1 Convolution과 닮아 있음

![image](https://user-images.githubusercontent.com/77658029/130166024-ad359fb7-5c6b-445d-bbd1-a987aba340be.png)

<br>


### 1x1 convolution 

- 병목현상을 제거
- 네트워크 크기 제한(paramater 감소)

![image](https://user-images.githubusercontent.com/77658029/130165079-af290cef-41ef-40e1-ac27-a25704c65cba.png)

-> 이 방법을 사용함으로써 Channel(dimension) reduction으로 Parameter를 줄이고, 이렇게 줄어든 Parameter를 filter크기와 layer 깊이를 늘리는데 사용함


<br>

## Classifier

### Auxiliary Classifier

- googLeNet 논문에서 정확한 설명은 빠져있는 내용
- Layer가 깊어질 수 록 gradient vanishing가 발생하고, 끝에서는 학습이 제대로 이뤄지지 않거나 overfitting현상이 발생할 수 있음
- googlenet 중간에 Classifier를 두어 역전파를 생성하여, 최종 역전파와 합쳐서 Gradient vanishing 최소화 시키기 위한 것으로 보임
- 학습시에만 사용하고 이후에는 사용하지 않음
- 학습을 도와주기 위한 도우미 역할

![image](https://user-images.githubusercontent.com/77658029/130165624-86ff2c33-c129-4d97-8dae-fd99c0d64eb5.png)

- 파란색 점선은 Classifier가 없는 경우, 빨간색 선이 Classifier가 있는 경우로 gradient값이 다시 증가해서, 더 안정적인 학습결과를 얻을 수 있게 됨

<br>

### Output Classifier

- 마지막 단계로서 이미지를 인식하는 부분
- average pooling과 softmax연산으로 분류함
- Googlenet에서의 average pooling은 GAP(global Average Pooling)을 의미함
- Gap를 활용하여 따른 가중치에 대한 필요가 없이 바로 연산이 가능함

![image](https://user-images.githubusercontent.com/77658029/130174259-f1390cbe-da8d-4a23-8c59-1eab74014ac2.png)


<br>

## Data augmentation

- 한 개의 사이즈가 아니라 여러 사이즈의 image를 활용하여 training시킴
- 가로, 세로 비율을 3:4, 4:3 사이로 유지하면 본래 사이즈의 8~100%를 포함하여 다양한 Patch를 사용
- photometric distortion 사용하여 학습데이터를 늘림

<br>

**📌reference**

- [라온피플](https://m.blog.naver.com/laonple/220710707354)
- [IMHO](https://hskang9.github.io/various_cnn/2017/11/24/inception/)
- [백광록](https://phil-baek.tistory.com/entry/3-GoogLeNet-Going-deeper-with-convolutions-%EB%85%BC%EB%AC%B8-%EB%A6%AC%EB%B7%B0#recentComments)
- [Time Traveler](https://89douner.tistory.com/62?category=873854)

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

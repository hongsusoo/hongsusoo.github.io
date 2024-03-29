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

title: "Deep Learning이란?"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - DL
tags:
  - 
date: 2021-08-09
last_modified_at: 2021-08-09
---

<br>

# DL Introduction

좋은 Deep learner는 어떤것 일까?

1. 구현 스킬(tensorflow, torch)
2. 수학 능력
3. 현재 DL trend(knowing a lot of recent papers)

## 인공지능(AI)

- 사람의 지능을 모방하는것!
- 인공지능의 한 분야로 ML이 있고, 그 안에 한 모델로써 Deep Learning이 자리잡고 있음

![image](https://user-images.githubusercontent.com/77658029/128651883-e08d6147-2f47-44c6-96d5-2382fb6b261d.png)

### Deep Learning에 필요한 요소

1. Data : 어떤 모델을 학습시킬 수 있는 데이터가 필요
2. Model : Data를 분석해서 어떤 Label화 하는 작업
3. Loss function : 학습시키기 위한 function이 필요함 regression 문제에서 Norm-2 사용하듯
4. algorithm : Loss function을 최소화 시키고자 하는 algorithm

💡 새로운 연구/논문을 볼때 위 4가지를 확인하면서 보면, 논문에 대한 이해도를 높일 수 있음(기존 대비 어떻게 변화했는지)


## Data 

- Data는 우리가 풀려고 하는 문제의 형태와 관련이 있음
    + Classification, Semantic Segmentation, Detection, Pose estimation, Visual QnA
    
    ![image](https://user-images.githubusercontent.com/77658029/128652207-0d2e6787-1f43-4018-98d6-7cea4c4b20fe.png)
    
## Model

![image](https://user-images.githubusercontent.com/77658029/128652228-ab56dd04-04e6-4671-b649-36e07f6c1bfa.png)

## Loss Function 

- 이루고자 하는 Proxy(근사치)에 불과함
- 단순히 Loss function이 줄어드는게 목적이 아님(무조건 줄어든다고 맞는게 아니야)
- 이 Loss가 줄어드는게 진짜 우리가 풀고자 하는 문제의 방향성과 맞는지 지속적으록 고민해야함

![image](https://user-images.githubusercontent.com/77658029/128652276-2f06923a-146e-4842-8e71-6b573b7940e8.png)

## Optimization Algorithm 

- 만든 모델이 단순 test data 뿐만 아니라 실제 data 속에서도 잘 동작 할 수 있도록 하는 skill

![image](https://user-images.githubusercontent.com/77658029/128652470-940b3445-3a39-455d-80b2-f55126553e48.png)


# Historical Review


2012 - AlexNet : 이미지 불류대회에서 처음으로 DL이 우승한 시점
2013 - DQN : 알파고
2014 - Encoder/Decoder
     - Adam Optimizer : 결과가 잘나옴, 왠만하면 잘나온다
2015 - GAN(Generative Adversarial Network) : 술집 이름이 논문 마지막에 들어가 있음(술마시다가 방법이 떠오름)
     - Resnet : Deep Learning을 가능하게 만든것(layer를 깊게 쌓음), 이전까지는 20단정도 쌓으면 더 이상 못쌓는다 생각했는데, 100단까지 쌓을 수 있는 패러다임을 제공함
2016 - 
2017 - transformer(Attention Is All You Need) : 많은 부분이 이걸로 대체되고 있음(RNN등을 대체함)
2018 - Bert(Bidirectional Encoder Representation from Transformers)-fine tuned NLP Models : 여러 말뭉치로 pretraining 시킴
2018 - Big Language Models(GPT-X) : OpenAI, 굉장히 많은 1750억개 parameters를 사용함
2020 - Self-Supervised Learning : simCLR (심시엘알, label이 없는 unsupervied data를 이용함), 비지도학습,


**📌reference**
- boostcourse AI tech


<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

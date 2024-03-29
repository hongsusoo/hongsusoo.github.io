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

title: "CNN Model 소개(AlexNet, VGG, GoogleNet, ResNet, DenseNet)"
excerpt: "about : "
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - DL
tags:
  - [CNN model]
date: 2021-08-11
last_modified_at: 2021-08-11
---

<br>

# CNN model

- ILSVRC 에서 우승했던 몇몇 모델을 정리해보고자 한다.

**📌 ILSVRC(ImageNet Large Scale Visual Recognition Challenge)**

- Classification/Detection/Localization/Segmentation
- 1000개의 카테고리
- 100만장의 이미지
- trainset은 46만장


## AlexNet

- 8 Layer(60M)
- 11x11 convolution 사용
- ReLU(Rectified Linear Unit) activation function을 사용(non-linear) 
    → Gradient가 1이기 때문에 gradient vanishing 같은 문제에 강함
    → 선형적인 성질을 가지고 있음
    → 좋은 generalization
    → 쉽게 최적화 할 수 있음
- GPI implementation(2 GPUs)
- Local Response Normalization, Overlapping pooling _ LRL?
- Data argumenation
- Dropout

![image](https://user-images.githubusercontent.com/77658029/128959801-df0e72ca-ebb6-4385-b626-eccd60553084.png)


## VGGNet

- 총 19 layer(110M)
- 3x3 convolution filter 사용(여러 layer을 쌓아도 parameter의 숫자가 크게 늘지 않기 때문에 작은걸 사용, 요즘 7x7 넘는건 거의 사용안함)
- 1x1 convolution fully connected layers에서 사용
- Dropout(p=0.5)


**❓왜 작을 수록 좋을까?** 

- convolution의 크기를 늘리는게 layer를 늘리는 것 보다 Parameter 숫자가 빨리 늘어남
- 요즘 추세는 convolution의 크기를 줄이고, layer를 쌓음

![image](https://user-images.githubusercontent.com/77658029/128960758-e1d7b420-466f-4d2a-bbf7-20c659f7cbe8.png)

## googLeNet

- 총 22 layer(4M)
- NIN(network in network)

![image](https://user-images.githubusercontent.com/77658029/128961536-a5d98fc2-3573-43c8-a2b0-986cdeeac1bd.png)

- inception Block
    - parameter의 숫자를 줄여줌
    - 1x1 convolution은 channel방향으로 차원을 줄여줌

![image](https://user-images.githubusercontent.com/77658029/128961590-77abb155-f1ac-4ec1-b425-f84329cd5247.png)

![image](https://user-images.githubusercontent.com/77658029/128961854-19571ed5-7d08-4902-a665-75adb20768e2.png)

- 채널 방향으로 차원이 줄어들며 parameter 숫자가 줄어듦

=> 1x1 convolution과 dropout은 좀 비슷한건가?


## ResNet

- 저자 kaiming he
- 차이를 학습시키는 모델(residual)
- input data를 output data 더해주는 방식
- 깊게 쌓아도 효과가 좋아짐
- skip-connection

![image](https://user-images.githubusercontent.com/77658029/128962992-80f8923f-bb08-44fc-8286-d719c3a6bf46.png)

![image](https://user-images.githubusercontent.com/77658029/128962948-359f1031-e6f5-436e-bb97-33c1c4d1a711.png)

![image](https://user-images.githubusercontent.com/77658029/128963172-c326e37a-bf28-4491-9f1f-f0911baa6307.png)

- Bottle Nect구조

![image](https://user-images.githubusercontent.com/77658029/128963439-c13fb529-6ffd-4bdf-a3c6-2f15e3010c07.png)


## DenseNet

- ResNet은 input data를 output data와 더해주는 방식이었고, DenseNet은 그대로 이어주는 형태
- concatenation

![image](https://user-images.githubusercontent.com/77658029/128963217-059c31e1-1995-4c07-9933-6dc880669cb3.png)

<br>

**📌reference**
- boostcourse AI tech

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

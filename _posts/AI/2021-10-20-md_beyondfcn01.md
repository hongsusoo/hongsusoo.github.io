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

title: "Segmentation Model(Deconv,SegNet,Unet,DeepLabV1,DilatedNet) 소개"
excerpt: "about : segmentation"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - AI Model
tags:
  - [Segmentation]
date: 2021-10-20
last_modified_at: 2021-10-20
---

<br>

# FCN 한계점

<br>

- 객체 크기에 따른 한계점
    - 클경우 : 직역적인 정보만으로 예측

    ![image](https://user-images.githubusercontent.com/77658029/137902664-dcf264fb-baad-487b-b0ef-6f942615acf9.png)

    - 작을 경우 : 무시됨

    ![image](https://user-images.githubusercontent.com/77658029/137902700-3c25c4e9-8481-40ba-a510-1de6e9e1662c.png)
    
- 해상도가 떨어짐(디테링한 부분들이 사라지는 문제 발생
    - Skip connection을 적용했지만, Deconvolution 절차가 간단해 경계 학습하기 어려움
    
![image](https://user-images.githubusercontent.com/77658029/137902802-c9dcf29c-9ea6-4f51-801d-642d29056a6e.png)

<br>

# Decoder를 개선한 Model

## DeconvNet(2015)

- 해당 논문에서 FCN의 문제는 bilinear interpolation upsampling에 문제가 있다고 생각, 이 문제를 해결하기 위해서 Unpooling 방법을 제안함

<br>

### Architecture

![image](https://user-images.githubusercontent.com/77658029/137903511-2e81a31e-91e5-4a2e-82ba-ae856ba587cc.png)

![image](https://user-images.githubusercontent.com/77658029/137906367-cd820071-077b-4408-a5c2-a29aefdc4527.png)

- Decoder를 Encoder와 대칭 모양으로 구성함
- **Encoder** : ConvNet은 VGG16을 사용, Conv-Batch Normalization-ReLU로 구성되어 있고, 13개의 층으로 구성함
- **Decoder** : Encoder와 대칭형태로 unpooling(디테일한 경계를 찾음), Deconvolution(Transposed convolution, 전반적인 형태를 찾음)로 구성되어 있음
- Layer깊이에 따라 Feature map에서 뽑아낼 수 있는 물체의 정보가 다른데, Unpooling과 Deconv를 반복적으로 수행함으로써 물체의 구체적인 모습과 전반적인 형태를 모두 잡아낼 수 있도록함
    - 얕은 층 : 전반적인 모습을 잡아냄
    - 깊은 층 : 구체적인 모습을 잡아냄

![image](https://user-images.githubusercontent.com/77658029/137911048-a688aa1e-d062-4db9-82e5-9aab544bafc9.png)

- Unpooling의 경우 Example-specific 한 구조를 잘 잡아냄
    - 자세한 구조
    - 아래 이미지에서 보면 특징이 있는 부분을 작게 잡아냄
- Transposed Conv의 경우 Class-specific 한 구조를 잘 잡아냄(아래 이미지에서 
    - Unpooling으로 비워진 공간을 메꿔줌

![image](https://user-images.githubusercontent.com/77658029/137913173-ec4c9754-ffd0-4cc5-ab4e-3e19c4cbd17e.png)

<br>

### Unpooling

- 기존 Upsampling방식의 문제점은 Encoder에서 Max pooling을 통한 receptive field늘려나가면서 정확한 위치정보가 지워지는 현상이 발생
- FCN에서는 bilinear interpolation 방식으로 사용, 이 경우 하나의 위치정보가 여러 지역으로 나눠지며 blur 효과가 일어남
-  Unpooling은 Max pooling시 뽑은 위치 정보를 저장해 뒀다가 Upsampling시에 활용하는 방법


![image](https://user-images.githubusercontent.com/77658029/137907924-31264802-0cf7-49c1-b619-cc4f7f725244.png)

- Encoder에서 Max pooling을 진행 시 Max를 뽑아낸 위치 정보를 기록해 뒀다 Unpooling시 활용하여 Pooling시 뽑은 위치에 다시 Max값만 복원시키는 방식
- 다른 곳은 0으로 채워넣게 되는데, 이때 Sparse한 Activation map이 나오게 되는데, 이부분을 Transposed Convolution으로 보완해줌
- Pooling의 경우 노이즈를 제거하고 연산량을 줄여주는 역할을 했지만 Segmentation Task에서는 Pooling으로 경계에 대한 정보를 잃게됨

<br>

### Deconvolution(Transposed Convolution)

- Unpooling으로 Sparse해진 Activation map을 보완해줌으로써 전반적인 형태를 잡아줌

![image](https://user-images.githubusercontent.com/77658029/137908985-5391b4e7-313d-4d03-be55-fe336a1d5106.png)
<br>

### FCN vs DeconvNet

- FCN의 경우 특징이 뭉게지는 현상이 보이지만, DeconvNet은 좀 더 구체적인 모습을 잡아내는 것을 확인할 수 있음

![image](https://user-images.githubusercontent.com/77658029/137913988-c5c10a24-4637-4e5a-bde8-e7432a1687cc.png)

<br>

### 구현

1. Convolution & Deconvolution : 대칭 구조로 똑같은 형식으로 구현

![image](https://user-images.githubusercontent.com/77658029/137922925-bfd1a799-a087-4152-9dbd-a4cea61806e7.png)

2. max indices : Unpooling시 Max pooling에서 저장한 indices를 불러와서 연산해줌

![image](https://user-images.githubusercontent.com/77658029/137924318-5ed41bfe-c9ed-4651-8db5-578816a597ec.png)

<br><br>

## SegNet(2016)

- 성능적인 향상보다는 속도적인 향상을 꾀한 모델로 Real time Semantic Segmentation Task를 가능하게 한 모델
- Road Scene Understanding application 분야에서 발전하게됨
- 자율주행에 있어서 차량, 도로, 차선, 건물, 보도, 하늘, 사람 등의 Class를 빠르고, 정확하게 구분하는 특징이 있음
- 자율주행 중 배경이 변한뒤 예측하는건 의미가 없음

<br>

### DeconvNet vs SegNet

- 두 모델 모두 동일하게 VGG 16을 사용하였지만, SegNet의 목적상 속도를 빠르게 하기 위해서 DeconvNet의 중간 FC Layer로 7x7,1x1 Conv,Deconv 영역을 제거하여 연산량을 줄여줬음
- Decoder에서 DeconvNet은 Deconvolution을 사용하였지만, SegNet의 경우 Convolution연산으로 대체됨

![image](https://user-images.githubusercontent.com/77658029/137933754-d5f1b273-9475-45d4-b54c-e60044c53745.png)

![image](https://user-images.githubusercontent.com/77658029/137934021-f80bb287-7c9c-4c0a-b192-26b495cac0a2.png)

<br><br><br>

# Skip Connection 적용한 모델


- 이전 layer의 정보를 활용하여 물체의 전반적인 부분을 구분할 수 있도록 하는 방법
- FCN-32, FCN-16, FCN-8로 Skip Connection 수를 늘릴 수록 성능이 향상되었음

<br>

## FC DenseNet

- DenseNet에 Skip Connection을 적용
- DenseNet을 Backbone으로 Encoder, Decoder를 구성하였음
- FCN의 Skip Connection과 다르게 Summation이 아닌 concatenation하여 Layer정보를 전달해줌

![image](https://user-images.githubusercontent.com/77658029/137941169-4b03b114-adac-4fa1-b6b7-afbbae9d38ac.png)

<br>

## Unet

- Skip Connection 4개,,

![image](https://user-images.githubusercontent.com/77658029/137941813-0d51f7fe-0305-455d-9750-843e9eabbf6e.png)

<br><br><br>

# Receptive Field 확장

## Recpetive Field

- 뉴런이 얼마 만큼의 영역을 바라보고 있는지 나타냄
- Class를 구분한다고 했을때, 어떤 부분만 보는것 보다는 물체의 전체 영역을 봐야 더 정확하게 구분할 수 있음

![image](https://user-images.githubusercontent.com/77658029/137943042-917e072e-9dde-47e8-88ba-7fb9927b4d4f.png)

- 아래 버스의 경우도 Receptive field가 작아 버스 전체를 보지 않고 부분으로 나눠서 보기 때문에 정확도가 떨어지게됨

![image](https://user-images.githubusercontent.com/77658029/137944118-8bd34cc8-d22f-4e8a-8934-bb9fa12d5af4.png)

- Receptive Field를 넓히는게 detection, segmentation Task에서 중요함

<br>

## Receptive Field 넓히기(Maxpooling)

- Conv layer를 통해서 Receptive Field를 조정할 수 있음
- 초기 딥러닝 모델의 AlexNet의 경우 11x11 Conv를 사용하였었지만, Parameter 수가 기하급수적으로 많아져서 요즘은 3x3 Conv를 사용하여 Layer를 깊게 쌓는 모델이 많음
- 결국 Layer가 많아지면 모델이 무거워짐
- 간단하게 Conv layer사이에 pooling을 넣어주면 Receptive field를 넗힐 수 있음

![image](https://user-images.githubusercontent.com/77658029/137947459-59b43e91-5fa2-48d3-a1c1-9e6eec8dccee.png)

- 하지만 Max pooling을 반복하다보면 Low Feature Resolution을 가지는 문제가 발생함

<br>

## Receptive Field 넓히기(Dilated Convolution)

- 기존 Max pooling의 단점인 Resolution 문제를 해결하기 위해 고안됨
- 이미지 크기를 보존하고, 파라미터수도 비슷하게 Receptive Field만 넓히는 방법

![image](https://user-images.githubusercontent.com/77658029/137949523-b6a2a7a6-6850-4cbe-8d16-4a06928ca537.png)

- Parameter의 수는 9개로 동일하지만, 바라보는 영역은 기본 Convolution(3x3)대비, Dilated Convolution(5x5)로 동일한 것을 확인할 수 있음
- Dilated Conv의 kernel은 9개의 weight와 비어있는 중간을 0으로 채운 형태임
- Dilated Conv의 0으로 채워진 부분이 있어서, Max pooling + Conv와 비슷하게 생각했지만 Max pooling을 하면 4칸중 한칸의 정보만 가져오게 되지만, Dilated conv는 4개의 정보를 모두 사용하기 떄문에 Max pooling + Conv 보단 해상도가 덜깨짐

<br>

## DeepLabV1

![image](https://user-images.githubusercontent.com/77658029/138027957-1426d026-31b0-4b97-a5cb-bf395ed9f92d.png)

**DeepLabv1 (backbone:VGG)의 구조**
```python
conv1 : "conv→relu→conv→relu→3x3 maxpool(stride=2,padding=1)" 이미지 크기 input의 1/2
conv2 : "conv→relu→conv→relu→3x3 maxpool(stride=2,padding=1)" 이미지 크기 input의 1/4
conv3 : "conv→relu→conv→relu→conv→relu→3x3 maxpool(stride=2,padding=1)" 이미지 크기 input의 1/8
conv4 : "conv→relu→conv→relu→conv→relu→3x3 maxpool(stride=1,padding=1)" 이미지 크기 input의 1/8
conv5 : "conv(r=2)→relu→ conv(r=2) →relu→ conv(r=2) →relu→3x3 maxpool(stride=1,padding=1)" 이미지 크기 input의 1/8
FC6,FC7,Score : "conv(r=12)→relu→dropout→conv(1x1)→relu→dropout→conv(1x1,Classifier)"
Bilinear Interpolation : 1/8가 된 이미지를 선형적으로 8배 키워 원본 사이즈로 복원
```
- 3x3 Max pooling 사용 : FCN의 경우 2x2를 사용하여 1/2로 줄이는 연산을 진행하였지만, DeepLabv1의 경우 3x3 Max pooling에 Stride 2를 적용하여 1/2로 줄여줌
- Conv5 Layer에서는 Dilated Conv에 rate=2 사용하여 Receptive Field를 넓힘
- FC6 Layer에서는 Dilated Conv에 rate=12 사용하여 Receptive Field를 넓힘
- Upsampling의 경우 Bilinear Interpolation을 진행

<br>

**Bilinear Interpolation**

![image](https://user-images.githubusercontent.com/77658029/138028808-36e9f34d-e71a-48b7-a428-d312cdc63b44.png)

<br>

### Dense CRF(Conditional Random Field)

- Bilinear Interpolation의 경우 빈공간을 선형적으로 채워나는데, 이럴경우 Pixel 단위의 정교한 Segmentation이 불가능하게 됨
- 이를 보완하기 위한 방법으로 Dense CRF 알고리즘을 사용함

![image](https://user-images.githubusercontent.com/77658029/138029052-9c87609a-f69a-4767-958c-fe59b5d648fa.png)

- 사용 방법은 원본 이미지와, 예측한 segmentation(pixel의 확률)결과를 사용하여 후처리하는 방식

![image](https://user-images.githubusercontent.com/77658029/138029421-2a81397c-9646-4b5b-a6df-4829547f4c25.png)

- 알고리즘 원리
    - 색상이 유사한 픽셀이 가까이 위치하면 같은 범주에 속함
    - 색상이 유사해도 픽셀의 거리가 멀다면 같은 범주에 속하지 않음
    
- Dense CRF의 경우 논문에서는 10회 정도 사용하게됨

![image](https://user-images.githubusercontent.com/77658029/138029739-db85b6e7-82f2-4f43-b27d-2aca38601217.png)

<br>

## DilatedNet

![image](https://user-images.githubusercontent.com/77658029/138030633-3b95cb92-ef38-456c-9db8-02e0e589de59.png)

```python
DilatedNet (backbone:VGG16)의 구조 (Front)
conv1 : "conv→relu→conv→relu→2x2 maxpool(stride=2,padding=0)" 이미지 크기 input의 1/2
conv2 : "conv→relu→conv→relu→2x2 maxpool(stride=2,padding=0)" 이미지 크기 input의 1/4
conv3 : "conv→relu→conv→relu→conv→relu→ 2x2 maxpool(stride=2,padding=0)" 이미지 크기 input의 1/8
conv4 : "conv→relu→conv→relu→conv→relu"` DeepLabv1의 Maxpooling영역 제거 
Conv5 : "conv(r=2)→relu→ conv(r=2) →relu→ conv(r=2)→relu" paddin을 조정해 Dilated conv이후에도 이미지 크기 변화 없음
FC6~Score : "conv(7x7,r=4,padding=12)→relu→dropout→conv(1x1)→relu→dropout→conv(1x1,Classifier)"
Deconv: "convTransposed2d(num_classes, num_classes, karnel_size=16, stride=8, padding=4)" 1/8가 된 이미지를 선형적으로 8배 키워 원본 사이즈로 복원
```
- 2x2 Max pooling 사용 : DeepLabv1의 경우 3x3를 사용하여 1/2로 줄이는 연산을 진행하였지만, DilatedNet에서는 2x2 Max pooling을 사용함
- Max pooling 제거 : DeepLabv1에서 Conv4,5 Layer의 Max pooling 부분이 DilatedNet에서 빠짐
- FC6 Layer에서는 7x7 kernel size의 Dilated Conv에 rate=4 사용하여 Receptive Field를 넓힘
- Upsampling의 경우 Transposed Convolution을 이용함

<br>

### DilatedNet - Basic Context Module

![image](https://user-images.githubusercontent.com/77658029/138031579-5d736820-6826-4ba8-bb29-df9f839a05da.png)

- Front 뿐만 아니라 성능을 개선하기 위한 Basic Context Module를 추가함
- 단순히 Dilated Conv 8개로 이뤄져있고
- Score 이후 추가적으로 연결하여 사용함
- 여러 크기의 Dilated Conv를 사용하여 여러 Receptive Field를 생성하여 이미지의 작은 물체부터 큰 물체까지 구분할 수 있도록함 

```python
Basic Context Module : 
"conv(r=1)→relu→conv(r=1)→relu→conv(r=2)→relu→conv(r=4)→relu→conv(r=8)→relu→conv(r=16)→relu→conv(r1)→relu→conv(1x1,Classifier)"
```

![image](https://user-images.githubusercontent.com/77658029/138031878-a5347326-08a5-4d1b-b981-b8de7966e963.png)

<br><br>

**📌reference**
- boostcourse AI tech
- [DeConvNet](https://deep-learning-study.tistory.com/565)
- [bilinear Interpolation](https://darkpgmr.tistory.com/117)

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

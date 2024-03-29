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

title: "합성곱 신경망(CNN, Convolution Neural Network)"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - DL
tags:
  - 
date: 2021-08-04
last_modified_at: 2021-08-04
---
<br>

# CNN

## CNN 용어 설명

### Kernel(Filter)

- 데이터의 특성을 뽑기 위해 Filter 사용함, CNN의 학습의 대상이 됨
- 셀카찍을때 어떤 효과를 넣는 그 필터

![image](https://user-images.githubusercontent.com/77658029/128345577-7e145408-ed13-482a-b378-dc0b3128b694.png)

<br>

>  Sobel Filter 소개

![image](https://user-images.githubusercontent.com/77658029/128351126-714489ea-8224-452a-b6da-ba11af5807b1.png)

<br>

### 액티베이션 맵(Activation Map, feature map)

- filter 연산의 결과로 이루어진 출력 행렬

<br>

### 스트라이드(Strid)

- kernel과 데이터를 convolution하고 이동하는 거리
- 아래 그림은 stride가 1인 그림이고, 만약 2면 두 칸씩 이동하여 곱해짐

![image](https://user-images.githubusercontent.com/77658029/128346187-e87a0eda-fd28-44ef-92a2-d1b00659e4de.png)

<br>

### 패딩(Padding)

- 기존 데이터에 kernel를 convolution해줄 경우 결과(feature map)의 크기는 입력데이터보다 작아짐
- 이런 현상을 방지하기 위해 원본데이터 주변에 픽셀을 추가해 연산을 하게 되는데 이런 작업을 Padding이라고 함
- 대부분 0으로 채워넣음
- 추가하는 크기는 kernel의 차원에서 한 차원 뺀 크기만큼 padding 해줌

💡입력 데이터(5x5), kernel 행렬(3x3)을 합성곱한 결과는 
(5(입력)-3(kernel)+1)차원의 행렬이 나오기 때문에 kernel의 차원에서 한 차원을 뺀 크기만큼 feature map의 크기가 줄어든다

<br>

### 풀링(Sub sampling or Pooling)

- sub sampling이라고도 하며, convolution layer를 거쳐 추출된 특징에서 sampling(pooling)을 거쳐 activation map을 인위적으로 줄여줌
- max pooling, average pooling, L2-norm pooling 종류가 있음

<br>

## Convolution 연산

- Convolution 연산은 kernel을 입력벡터 상에서 움직여 가며 계산
- CNN에서의 Convolution은 Kernel(filter)는 그대로 두고 데이터를 움직이며 겹치는 부분을 곱해서 더한는걸 의미함(연속함수의 경우는 적분)
- 신호(kernel)를 이용해 국소적으로 증폭 또는 감소시켜, 특징을 뽑아내거나 Filtering 하는 것을 의미함
- 연산 후 출력의 크기 :
  입력크기 : ($H,W$) / Kernal 크기 : ($K_H,K_W$) / 출력크기 : ($O_H,O_W$)
  
  $O_H = H - K_H +1$
  
  $O_W = W - K_W +1$

### **💡convolution 수식**
![image](https://user-images.githubusercontent.com/77658029/128447299-c82e8083-6c8a-4d5d-8b4c-f9e19546524a.png)

### **💡 convolution 연산**

- Kernel은 정의역내에서 움직이지만, 변하지 않고(translation invariant) 주어진 데이터에 국소적(local)으로 적용

![convolution](https://user-images.githubusercontent.com/77658029/128343785-b787df24-2737-418f-96d1-3ed1e44890a5.gif)

- 파란색 : 데이터
- 빨간색 : kernel
- 검은색 : 결과 
- 노란색 : convolution 연산(넓이가 검은색 그래프로 그려짐)

<br>

### **차원에 따른 Convolution**

![image](https://user-images.githubusercontent.com/77658029/128449300-1ec95814-368c-4291-989d-6ac0bc677d85.png)

- 채널이 여러개인 2차원 입력의 경우2차원 Convolution을 채널 개수만큼 적용
- 3차원 입력부터는 행렬이 아닌 Tensor라고 부름

![image](https://user-images.githubusercontent.com/77658029/128450408-0c92de2d-38f7-4ebc-a1f2-a6b934334e13.png)

💡 만약 출력의 차원을 여러개 만든다고 하면 kernel를 여러개 사용할 수 있음

![image](https://user-images.githubusercontent.com/77658029/128450705-7349de64-466c-43b9-b83f-b19f3010922a.png)

<br>

## CNN(Convolution Neural Network)

- 기존 MLP의 경우 데이터 x에 차원과 동일한 차원의 행벡터의 집합으로 가중치 행렬이 필요
- CNN에서는 kernel을 입력 벡터 상에서 움직여 가며 계산하기 때문에 더 작은 행렬로 가능함

![image](https://user-images.githubusercontent.com/77658029/128445976-b8115400-d142-4902-b140-95b67d739e37.png)

- MLP는 선형 모델과 활성함수로 모두 연결된 Fully connected 구조
- CNN은 이와 달리 Kernel을 입력벡터 상에서 움직여 가며 선형모델과 함성함수를 적용함

![image](https://user-images.githubusercontent.com/77658029/128345577-7e145408-ed13-482a-b378-dc0b3128b694.png)

<br>

## Convolution 연산의 역전파 이해하기 

- Convolution 연산은 Kernel이 모든 입력데이터에 공통으로 적용, 역전파를 계산할 때도 Convolution 연산이 나오게 됨

![image](https://user-images.githubusercontent.com/77658029/128450866-8bc6a9ec-60df-4dd5-bced-48485fe469ff.png)

![image](https://user-images.githubusercontent.com/77658029/128457007-cbcc4dc1-8a43-4698-bdd5-d8ea64689a34.png)

<br>

**📌reference**
- boostcourse AI tech
- [TAEWAN.KIM 블로그](http://taewan.kim/post/cnn/)
- [호롤리한 하루](https://gruuuuu.github.io/machine-learning/cnn-doc/)
- [뇌 외장 하드](https://wjrmffldrhrl.github.io/digital10/)
- [조대협의 블로그](https://bcho.tistory.com/1149)


<br>
```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

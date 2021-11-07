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

title: "CV(Computer Vision) model 소개(FCN, Deconv, R-CNN, YOLO)"
excerpt: "about : "
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - ai_models
tags:
  - [CV model]
date: 2021-08-11
last_modified_at: 2021-08-11
---

<br>

# computer vision application

- computer vision은 시각적인 정보를 컴퓨터가 이해할 수 있도록 하는 deep learning 분야
- Computer Vision에서 이미지에 대한 카테고리를 분류할 수 있는 여러 모델들이 있음
- 단순 분류(Classification) : 이미지에서 중심이 되는 하나의 객체의 Label를 정의함 - AlexNet, ResNet, Xception
- 지역 분류(Localization/Detection) : 객체에 대한 label 뿐만 아니라 위치까지 정의해줌 - YOLO, R-CNN
- Pixel 분류(Segmentation/Dense) : Pixel 단위로 Label를 예측 - FCN, SegNet, DeepLab

![image](https://user-images.githubusercontent.com/77658029/129435013-cedee175-0928-411d-9b78-77959cfceaf2.png)

💡 Semantic Segmentation

    - dense classification
    - 자율주행에 많이 활용됨
    - Pixel 단위로 분류

![image](https://user-images.githubusercontent.com/77658029/129435184-37e7bf82-79af-4153-9843-46e263d1ec78.png)


## FCN(fully Convolution Network)_segmentation

- 기존에는 Convolution연산으로 나온 벡터를 Flatten하여 1차원 dense layer로 만들고, softmax 함수로 분류를 진행하여 위치에 대한 정보를 잃어버림
- FCN의 경우 Convolution 연산을 사용하여 마지막 분류작업을 시킴
- 사용하는 parameter 수는 동일 하지만, 이미지에 대한 위치 정보를 잃지 않음으로써 heatmap를 그릴 수 있다는 장점이 있음
- 이 부분은 Convolution연산의 shared parameter 성질 때문으로 Image의 사이즈에 상관없이 동일한 parameter로 연산을 하기 때문에 coarse한 heatmap 구현이 가능함

![image](https://user-images.githubusercontent.com/77658029/129475920-29b019fb-2b48-4ee8-9b42-a1df7b2478d0.png)

- FCN 진행하게 되면 coarse한 output dimension을 갖게 되는데, Segmentation 처럼 pixel 단위로 분류하기 위해서는 원본 이미지로 다시 만들어주는 작업이 필요함

💡 처음 Image Segmentation을 진행할 때, input dimension의 크기를 유지하기 위해 padding 하면서 convolution을 진행하는 방법을 사용했는데, parameter수가 급격하게 늘어나는 문제가 발생해서 기존 CNN 방식으로 크기를 줄이고 다시 늘리는 아이디어로 deconvolution 개념이 나옴


### Deconvolution

- convolutions transpose 혹은 unsampling 으로도 불림
- Pixel 단위 분류를 위해서 convolution으로 작아진 output image를 복원시켜주는 개념
- 하지만 convolution을 되돌리는 작업은 불가능함

![image](https://user-images.githubusercontent.com/77658029/129476754-f4260a27-e090-428c-bb4f-ec017b235bcc.png)

**📌Deconvolution Idea**

1. pooling layer 복원 방식

![image](https://user-images.githubusercontent.com/77658029/129476872-4b33a249-8729-4110-83e5-0584e2572f0e.png)

2. convolution transpose

![image](https://user-images.githubusercontent.com/77658029/129476966-69625ad7-b232-45ab-8bdb-e8152717ab30.png)



## R-CNN(Region-based CNN)_Detection, Localization

- pixel 단위가 아닌 bound box를 만들어냄
- 1)image에서 2)수 많은 Region(약 2000개)을 뽑아내서 똑같은 크기로 맞춘 후 3)분류모델(AlexNet)을 돌려 Feature를 뽑아 4)SVM으로 구분
- 특정 영역을 뽑아낸 image를 RoI(Region On Interest)라고 함
- 특정 영역을 뽑아내는 것은 Selective Search 알고리즘을 이용


![image](https://user-images.githubusercontent.com/77658029/129477391-2d20150a-f54b-4651-9ea7-70dc5eeda8d8.png)

- RCNN의 단점

1. 2000개의 crop image를 다시 처리해야하기 때문에 1장의 이미지 구분 시 시간이 오래 걸림(59s/image on CPU)
2. Crop image를 뽑은 후 image 크기를 조절하며 image의 특징이 변경됨
(CNN를 하기 위해서는 FC layer의 size를 맞추기 위해서 input image의 크기를 맞춰줘야함)
3. FC layer 이후에도 SVM, bounding box regression를 따로 학습이 필요함(CNN까지 포함하여 총 3구간의 학습이 필요함) → Multi-stage pipline


## SPP-Net(Spatial Pyramid Pooling)

- R-CNN의 단점을 없애기 위해 CNN을 먼저 진행한 이후 crop feature값 pooling 하는 방식으로 FC layer를 맞춰줌
- crop된 feature를 pooling하여 FC layer의 input 차원을 맞춰주는 작업이 필요한데, 그 작업이 SPP
- SPP는 미리 feature맵을 나누는 여러 개의 분할 방식을 정한 후 그 분할 된 1칸(bin)을 한 원소로 하는 벡터(Feature Vector)로 Classify를 진행함 → 이 방식으로 피라미드라는 이름이 붙음
- SPP 논문에서는 4개의 피라미드 layer를 사용(1x1,2x2,3x3,6x6)
- 1번의 CNN만 진행함

    R-CNN : ① image input → **② extract crop image(RoI) → ③ resize crop image → ④ CNN** → ⑤ Classify

    SPP-Net : ① image input → **② CNN → ③ extract crop feature(RoI) → ④ SPP** → ⑤ Classify

![image](https://user-images.githubusercontent.com/77658029/129479633-4a165da2-0744-47d7-8c27-d7a734e145cc.png)

- SPP-Net의 단점

1. SPPNet도 결국은 여러개의 tensor를 뽑아내서 하나의 벡터로 만들고 다시 분류하는 작업 필요하기 때문에 시간이 오래걸림(end-to-end 방식이 아님)
2. R-CNN과 동일하게 Multi-stage pipline 형태가 유지됨

## Fast R-CNN

- SPPNet과 동일하게 Conv Feature Map에서 Feature RoI를 정하고
- 1개의 pyramid Layer를 사용하여 Feature Vector를 구함
- RoI Pooling 방식을 통하여 CNN부분과 분류, Bounding box regression을 한번에 loss function으로 잡아서 학습시킬 수 있게됨

💡 RoI Pooling으로 Crop image feature를 Neural Network 안으로 끌어드림

![image](https://user-images.githubusercontent.com/77658029/129481619-c2da7843-9fbd-418f-b52c-c9d501c03978.png)

- Fast R-CNN의 단점

1. Selective search를 이용하여 결국은 2000개의 region를 무작위로 뽑아서 학습하게됨

## Faster R-CNN

- Fast R-CNN를 그대로 계승하지만 Selective Search를 이용하여 무작위하게 추출하던 RoI를 학습시켜서 사용함
- 2K image → 0.8k image
- RPN(Region proposal Network)을 사용하여 객체가 있을 만한 곳의 위치도 학습시킬 수 있게 함
- RPN에서는 Anchor box를 활용하여 Classification과 Bounding Box regression을 학습시키고 이 부분을 RoI Pooling을 진행함
- Anchor box는 미리 정해놓은 크기

💡 외부 알고리즘(Selective Search)으로 뽑던 RoI 방식을 Neural Network 안으로 끌어드림

![image](https://user-images.githubusercontent.com/77658029/129484185-0439fe64-01bd-48ea-9ec5-b5eb73346d5d.png)


## R-CNN vs SPPNet vs Fast R-CNN vs Faster R-CNN

![image](https://user-images.githubusercontent.com/77658029/129484941-e391370d-1d31-4380-9b93-d3c4254091ee.png)

## YOLO(You Only Look Once)

- Faster R-CNN보다 7배가량 속도가 빠름
- Faster R-CNN에서는 Region Proposal과 Classification 두 영역으로 나눠져 있었지만, YOLO는 한번에 진행함
- Real Time으로 처리하나, 정확도는 약간 떨어짐 
- Grid를 나눠서 위치에 따른 객체가 있을 확률을 보고 box를 정하게됨(x,y,w,h,c)-B개의 bounding box를 뽑음(논문에서는 2개를 뽑음)
- NMS(Non-Maximum Suppression)방식을 사용하여 최종결과를 이미지에 그려줌

![image](https://user-images.githubusercontent.com/77658029/129485947-eda52b4c-6902-41bf-b9ee-acff2781d944.png)

<br>

**📌reference**
- boostcourse AI tech
- [Zyl Story](https://medium.com/zylapp/review-of-deep-learning-algorithms-for-object-detection-c1f3d437b852)
- [Hyunjulie](https://medium.com/hyunjulie/1%ED%8E%B8-semantic-segmentation-%EC%B2%AB%EA%B1%B8%EC%9D%8C-4180367ec9cb)
- [분석벌레의 공부방](https://analysisbugs.tistory.com/104)
- [Jaeyun's AI LAB](https://m.blog.naver.com/jaeyoon_95/221785990158)
- [갈아먹는 머신러닝](https://yeomko.tistory.com/17?category=888201)
- [약초의 숲으로 놀러오세요](https://herbwood.tistory.com/10)


<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

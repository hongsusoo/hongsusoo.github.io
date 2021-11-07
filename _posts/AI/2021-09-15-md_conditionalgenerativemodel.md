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

title: "Conditional Generative Model"
excerpt: "about : Generative Model"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - ai_models
tags:
  - [Generative model, GAN]
date: 2021-09-15
last_modified_at: 2021-09-15
---

<br>

# Conditional Generative model

- 일반적인 Generative Model의 경우는 random sample에 대해 생성 하지만
- Conditional Generative Model은 특정 condition이 주어진 상태에 대해서 생성함
- Generative model은 확률 변수를 학습 신킨다고 이해할 수 있음

![image](https://user-images.githubusercontent.com/77658029/133353872-a78836e5-0905-4d33-82d4-b3497a5bdf67.png)

<br><br><br>

## 응용 분야

- vision task
- 저 퀄리티 오디오 -> 고퀄리티 오디오
- 번역
- 뉴스기사(타이틀 주어졌을때 내용 작성)

<br><br><br>

## GAN

- 위조지폐범(Generator) vs 경찰(Discriminator)
- 적대적 학습법으로 불림


![image](https://user-images.githubusercontent.com/77658029/133353936-a9cc0288-1a53-448a-bf4d-08a126e18dd5.png)


<br><br><br>

## Conditional Gan 응용

- image to image translation
- Input image가 주어졌을때, 다른 형태로 바꿔주는것
- 저해상도 -> 고해상도
- 흑백사진 -> 칼라 사진


![image](https://user-images.githubusercontent.com/77658029/133354073-70dc559c-1d3e-4d6c-a092-a40d810d8451.png)

<br><br><br>

## Example 1. Super Resolution

- 저해상도 image 입력, 고해상도 image 출력
- 일반적인 Naive Regressor Model의 경우 L1(MAE),L2M(MSE) loss를 활용하여 학습진행

+) 해상도는 높아지는것 같은데, 구분성이 떨어짐

+) 전반적으로 Loss는 적지만, 특성에 대한 이해도가 떨어짐

- Gan의 경우는 Real data와 비슷하게 학습했기 때문에, 특성에 대한 이해도가 높음

![image](https://user-images.githubusercontent.com/77658029/133354571-0c9a26f3-182d-4e26-999b-7a2522e2bbd7.png)

- Regressor model과 Gan의 차이

![image](https://user-images.githubusercontent.com/77658029/133364435-b9d72c1c-6328-4607-a2ca-15858cb9fd80.png)


<br><br><br>

## Image Translation

- image를 특정 방법으로 변형해줌

<br><br>

### Pix2Pix

- Loss Function으로 L1 Loss와 Gan loss를 모두 사용
- L1 Loss로 blurry한 Image에 Gan을 추가해 realistic 하게 바꿔줌
- Gan Loss Function으로 원본 이미지가 많이 바뀌는 것을 L1 Loss로 최소화 시켜줌

![image](https://user-images.githubusercontent.com/77658029/133365255-7b3ee53e-0336-4a82-9bad-9808ed398e20.png)

![image](https://user-images.githubusercontent.com/77658029/133365163-3174d6b3-fc33-4705-aa93-60d7106d09bc.png)

🚨 하지만 Pix2Pix의 경우는 훈련을 위해 Paired된 Image가 필요하나 이런 dataset 구축이 어려움

![image](https://user-images.githubusercontent.com/77658029/133365411-eac33c2a-9218-4154-830f-9e895de08cce.png)

<br><br>

### CycleGAN

- Pix2Pix2의 Paired된 dataset이 아닌 unpaired된 dataset으로 학습 가능하게 하는 시도가 CycleGAN에서 이뤄짐

- CycleGAN loss = GAN loss(2개 방향으로) + Cycle-Consistency loss
- GAN을 통해 X -> Y, Y -> X 한번 Cycle을 거친 대상은 원본(input)과 동일해야함
- 이 동일한 정도를 Consistency loss로 추가함


🚨 Mode Collapse 현상이 발생 -> 하나의 output만 나와서 Generator가 훈련이 안되는 현상

![image](https://user-images.githubusercontent.com/77658029/133366966-8ee707de-eae4-4e6c-a5e7-592dfae3fee0.png)

💡 이런 현상을 해결하기 위해 Consistency loss를 추가, realistic 한 정도 뿐만 아니라 Content 보존에 대한 loss임

![image](https://user-images.githubusercontent.com/77658029/133367247-5d322878-b4a7-4599-8d38-b83d7b416f83.png)

<br><br><br>

## Perceptual Loss

- resolution을 높이기 위한 Loss
- 기존 Adversarial loss(GAN loss)의 경우 argmax,min이 번갈아가며 Discriminator와 generator 하나씩 학습시켜 training이나 code구현이 어려움
- any pretrained network가 필요없음 -> 다양한 어플리케이션에 사용가능함

- Perceptual Loss는 쉽게 training 시키고, code구현이 가능하나 pretrained model를 필요로함

- 아래와 같은 pretrained perception을 사용함
- 이 부분이 사람의 시지각과 비슷한 역할을 함
- image를 perceptual space로 변경시켜줌

![image](https://user-images.githubusercontent.com/77658029/133368190-b8e80eb6-da71-4e8f-8019-e2602d0a6419.png)

<br><br>

### Perceptual Loss Network

- pretrained VGG16를 활용하여 image의 semantic content를 관찰하여 비교하여 loss를 구함
- 이때 VGG는 fixed되어 있고, Generator만 학습시켜 원본 이미지가 생성 될 수 있게함

![image](https://user-images.githubusercontent.com/77658029/133368707-6ed15c21-c605-4690-8701-5598d10a799e.png)

![image](https://user-images.githubusercontent.com/77658029/133368679-2802f60c-b117-4c4e-a685-5022060e517e.png)

<br><br>

### Style Reconstruction loss

- 우리가 Translation 하고 싶은 Style Target과 우리가 바꾸려고 하는 원본 Image를 input으로 함
- 두 image를 VGG에 돌려 feature map을 출력
- 바로 loss를 계산하지 않고 Style를 남기기 위해 Gram Matrices를 사용하여 이미지 전반적인 (경향성)통계적인 특징을 담을 수 있도록 함
- Feature map이라는건 Image를 해석하는 작은 단위기 때문에 Feature 사이들의 전반적인 경향성이 Style로 반영되게됨
- 이런 feature들의 상호 영향력을 수치화 하기 위해 고안한 것이 Gram Matrices
- Gram Matrices는 feature Map 사이의 내적을 통해 feature간 상관성을 비교하는 matrix
- 이 matrix를 사용하여 loss를 산출함
- 크기가 1인 vector로 변경이 필요할듯?

![image](https://user-images.githubusercontent.com/77658029/133370151-70a943c1-e0b4-4610-b9aa-fee4660d4d8f.png)

![image](https://user-images.githubusercontent.com/77658029/133371159-1bbe28ef-2657-4f1d-ac96-d07f04b1af23.png)

<br><br><br>

## GAN응용 분야

- deepfake : 얼굴, 목소리, 얼굴에 대한 애니메이션 생성 -> Fake president speeched
- deepfake를 detect할 수 있는 도전들도 나오고 있음
- privacy 보호를 위해 사용
- 윤리적인 부분도 같이 생각해봐야함
- 외형을 빌려 pose를 입힐 수 있음
- video를 게임에 사용
- 목소리 변조

<br><br><br>

**📌reference**
- boostcourse AI tech

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

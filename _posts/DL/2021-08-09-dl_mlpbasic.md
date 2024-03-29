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

title: "MLP(Multi-Layer Perceptron) 개념"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - DL
tags:
  - 
date: 2021-08-10
last_modified_at: 2021-08-10
---

<br>

# Neural Network & Multi-Layer Perceptron

- 동물의 뇌에서 영감을 받아 만들어진 Computing System
- NN이 왜 성능이 좋을까?에 대한 대답으로 사람의 뇌를 모방해서 라고 대답하긴 애매하다.
- 날고싶다고 새처럼 비행기를 만들지 않는것 처럼, 사람의 뇌를 모방하기 위해서 똑같은 구조를 갖는건 아니다
- 그 자체의 모델을 보고 수학적으로 분석하는게 좋은 생각인것 같음

## Neural Networks

- Neural Networks are function approximators that stack affine transformations followed by nonlieaner transformations
- NN은 비선형 변환 행렬을 쌓아서 함수를 근사시키는 모델


## Beyond Linear Neural Networks

- 우리는 행렬을 통해서 차원을 변화 시킬 수 있는데 이런 단순한 선형변환으로는 특징값을 뽑아내기가 어려움
- 이런 선형변환에서 어떤 특징을 극대화하여 뽑아내기 위해 activation function(sigmoid, tanh, ReLU)을 사용하게됨

![image](https://user-images.githubusercontent.com/77658029/128654909-9e6bc61c-6d13-4eff-9008-3724f087b50f.png)

🎈 Activation Function

![image](https://user-images.githubusercontent.com/77658029/128654951-2c5af08d-b1fa-49c8-a8f5-02750f80bd5a.png)

## Multi-Layer Perceptron

- 여러번의 행렬 변환을 통해서 Loss function을 최소화하는걸 목적으로 함

![image](https://user-images.githubusercontent.com/77658029/128655080-aff7e6ab-713b-407f-95ce-43bcc0e69731.png)

- Loss Function 중 기본적으로 아래 3가지가 있음
- Loss Function은 결국 우리가 풀어야할 문제와 Align이 맞아야된다. 
- 만약 MSE 방식을 사용하는데, 특이한 한 점을 맞추기 위해서 전체적인 데이터가 shift될 수 있음을 생각해야한다

![image](https://user-images.githubusercontent.com/77658029/128655477-be5aff1a-1956-472f-9b1f-bb1c4564240e.png)

<br>

**📌reference**
- boostcourse AI tech

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

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

title: "Autoencoder 기초(1/5)"
excerpt: "about : Autoencoder"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - DL
tags:
  - [autoencoder]
date: 2022-03-01
last_modified_at: 2022-03-01
---

<br>
> 해당 글은 이활석님의 오토인코더의 모든 것 유튜브 영상을 바탕으로 제작되었습니다.

<iframe width="885" height="498" src="https://www.youtube.com/embed/o_peo6U7IRM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

--- 

**AutoEncoder**

딥러닝을 하다보면 가공된 데이터를 만들기 위해 많은 에너지를 쏟고 있다.

하여 최근 딥러닝 연구는 이런 데이터가 필요없는 비지도 학습으로 무게중심을 옮겨가고 있는데, Autoencoder는 비지도학습(**Unsupervised Learning**)의 대표적인 방법이다.

Autoencoder는 아래와 같은 구조를 가지고 있는데,

 <img src="https://user-images.githubusercontent.com/77658029/156111234-aad23ae9-d571-4ac7-b7ca-47aeacb5d2cd.png"  width="70%" height="70%"/>

Encoder를 통해 차원을 축소시키는 역할을 해주고(**Manifold Learning**), Decoder를 통해 차원을 복원하며 데이터를 생성하는 역할을 해준다.(**Generative Model Learning**)

학습의 경우는 **Negative Maximum Likelihood Estimation을 통한 Loss최소화**를 목적으로 학습하게 된다.

**main keywords**

1. Unsupervised Learning
2. ML(Maximum Likelihood) Density Estimation
3. Manifold Learning
4. Generative Model Learning

Autoencoder에 대한 정확한 이해를 위해 DNN과 Manifold learning에 대한 기초 지식을 쌓고(Chapter 1,2), Autoencoder에 대한 설명(Chapter 3,4), 그리고 어떻게 활용되는지(Chapter 5) 순서로 정리할 예정이다.

---

# 1. Deep Neural Networks 기초

전통적인 Machine Learning은 크게 4가지 영역으로 나눠서 생각할 수 있다. 

1. 데이터 취합 (Data Collection)
2. 모델 및 목적함수 정의 (Define Functions)
3. 학습 (Learning/Training)
4. 예측 (Prediction/Testing)

영상에서 말하고 있는 건 모델 정의와 학습 부분(2,3번)에 대해서 두 가지 접근 방법을 설명해주고 있다. 

하나는 Gradient Descent 관점, 또 다른 하나는 Maximum Likelihood 관점이다.

## 모델 및 목적함수 정의 (Define Functions) - Gradient Descent

Machine Learning의 구성을 보면 아래와 같이 볼 수 있는데, 여기서 크게 2가지를 정의해야한다. 

 <img src="https://user-images.githubusercontent.com/77658029/156113068-857de2b5-cecc-4381-9356-0c38e45af98d.png"  width="70%" height="70%"/>

첫 번째는 상황에 맞춰 모델($f_\theta (.)$)을 정의해야한다. 시계열 데이터를 다루기 위해서는 RNN, 이미지 데이터의 경우 CNN 모델 등 상황에 맞춰 필요한 모델을 정의해야한다. 

두 번째는 목적함수($L(f_\theta (x),y)$)를 정의하는 것이다. Deep Learning에서 Loss Function이 목적함수 중 하나의 종류라고 할 수 있는데, 모델의 예측과 실제 값과의 차이를 최소화 하는 Loss를 목적으로 하는 특정 함수를 정의해야 한다. 


## 학습 (Learning/Training) - Gradient Descent

학습이란 정의한 모델의 $\theta$를 추정하는 작업이다. 

우리의 목적함수(여기선 Loss Function) $L(f_\theta (x),y)$을 최소화하기 위해서 가장 대중적인 Gradient Descent 방법이 있다.

Gradient Descent 방식은 Iterative Method로 조금씩 $\theta$를 Update하는 방식이다. 

이때 3가지 전략이 필요하다

첫 번째는 $\theta$를 Update하는 조건이다. Gradient Descent 방법에서는 Update한 $\theta$의 Loss값이 기존 Loss값보다 작으면 Update를 진행한다.

두 번째는 Update를 멈출 시점을 정하는 것이다. 
<br>여기서는 Update한 Loss값과 현재의 Loss값이 변화가 없을 때 Update를 멈추는 방법을 사용했다. 

세 번째는 $\theta$를 Update하는 방법이다. 
<br>정해진 $\theta$에서 Update를 하기 때문에 Taylor 급수를 이용할 수 있다. 일반적으로 Taylor 급수에서 2차 근사식을 이용한다. 이때 아래 식에서 보면 $\eta$(에타)가 있는데, Taylor 급수의 경우 함수의 전반적인 예측이 아닌 정해진 구간에서의 근사식이 되고, 2차 근사식을 사용했기 때문에 근사 범위가 상당히 작기 때문에 학습 속도를 조정하기 위한 상수로 $\eta$를 사용하게 된다(작은 값으로 선정).

<img src="https://user-images.githubusercontent.com/77658029/156122119-25a024a0-4ae2-468b-a283-b5ece6491638.png"  width="90%" height="90%"/>

### Loss Function

> 여기서 Loss Function을 정의할 때, Backpropagation 연산을 위한 중요한 2가지 가정이 있다. 

**Assumption 1** : Total Loss는 데이터 각각의 Loss를 모두 합한 값이다.
- 곱하거나, 나누기와 같은 연산은 제외

각 데이터에 대한 gradient값을 계산할 때, 합으로 되어 있는 경우에 쉽게 값을 구할 수 있게 된다. 아래 식에서 보면, 학습을 위한 Loss 계산시 각 Sample에 대한 Loss값의 Gradient값을 구하게 되는데 만약 곱으로 구성되면, 모든 Sample의 결과를 메모리에 저장해둬야 하기 때문에 비효율적인 연산이 된다.

<img src="https://user-images.githubusercontent.com/77658029/156128908-93f67a3b-4e00-48b2-a975-d51548de2b6b.png"  width="70%" height="70%"/>


**Assumption 2** : 마지막 출력단에서의 Loss를 의미한다.
- 중간 Layer에서의 Loss는 활용할 수 없음

마지막 layer의 Error를 구하기 위해서는 Loss Function은 Output에 관련된 함수여야 미분이 가능하게 된다. 만약 이 가정이 없다고 하면 모든 미분값은 0이 되어 Update가 일어나지 않게 된다.

<img src="https://user-images.githubusercontent.com/77658029/156135087-ec2fc318-8582-4a08-bdc0-2c5bb5386817.png"  width="70%" height="70%"/>


위 식을 보면 Activation function의 미분값이 Layer가 깊어질 때마다 곱해지게 된다. 만약 Activation Function으로 Sigmoid를 사용할 경우를 관찰해보면, Sigmoid의 도함수의 최대값을 보면 0.25의 값을 가지는데, 이 값이 지속적으로 곱해지다보면 Gradient Vanishing 현상으로 일정 수준 Layer가 깊어지면 Update가 안되게 된다. 이러한 현상을 막기 위해 도함수 값을 1로 만든 ReLU를 사용하게 되면 이론적으로 이런 현상을 줄일 수 있다.

### Loss Function Test 

위 두 가정을 만족하는 Loss Function으로 MSE(Mean Square Error)와 CE(Cross Entropy) 두 가지가 있다. 

어떤 상황에 어떤 Loss Function을 써야할까?

상황에 맞는 Golden Rule이 있을까?

이를 실험하기 위해서 두 관점으로 두 Loss Function을 비교해 보자


<img src="https://user-images.githubusercontent.com/77658029/156141041-ac24d09e-2870-4ada-a659-d096be74d600.png"  width="50%" height="50%"/>

아주 기본적인 Neural Network를 구성해서 Test를 진행했다. Input으로 1.0이 들어가면 Output으로 0.0이 출력된다.

**Mean Square Error 계산**

<img src="https://user-images.githubusercontent.com/77658029/156142407-ea6d9581-883b-4e7b-8740-5e00140d88fe.png"  width="50%" height="50%"/>

- Activation Function의 도함수가 남아 있음

**Cross Entropy 계산**

<img src="https://user-images.githubusercontent.com/77658029/156142793-4a7c268e-a31e-49a8-97af-9222ec458da9.png"  width="50%" height="50%"/>

- Activation Function의 도함수가 제거됨

**비교**

두 경우에 대해서 비교해보면, Activation Function항이 제거된 Cross Entropy Loss Function이 더 빠르게 학습하는 것을 알 수 있다.

<img src="https://user-images.githubusercontent.com/77658029/156142923-6a70406b-37a1-4748-8039-4d5128e0bdca.png"  width="90%" height="90%"/>
<br><br>


## 모델 및 확률분포 정의 (Define Functions) - Maximum Likelihood

Gradient Descent 관점에서는 목적함수, 즉 Loss Function을 최소화 하는 관점으로 접근하였다.

<img src="https://user-images.githubusercontent.com/77658029/156146591-b72f3506-209c-44bb-b59d-179cff7b5a50.png"  width="70%" height="70%"/>

모델을 정의하는 부분은 동알하게 진행되지만, Maximum Likelihood 관점에서는 목적함수가 아닌 확률분포를 정하여 Output값이 나올 확률을 계산하게 된다. 주어진 데이터를 제일 잘 설명하는 모델($p(y|f_\theta (x))$의 값이 최대)을 찾기 위한 학습을 진행한다. 


## 학습 (Learning/Training) - Maximum Likelihood

학습이란 정의한 모델의 $\theta$를 추정하는 작업이다. 

Gradient Descent 관점과 동일하게 모델을 학습시키기 위해서 Loss Function이 필요한데, 위와 동일한 형식을 맞추기 위해 

Max -> min으로 바꾸기 위한 `-`

확률의 곱연산을 합의 연산으로 바꾸기 위해 `Log`를 붙여준다. 

수식으로 표현하면 $-log(p(y\mid f_\theta (x)))$


💡 Maximum Likelihood는 샘플의 확률값이 곱으로 표현되는데, 이를 위해 i.i.d Condition을 만족시켜야 한다.(independence Identical Distribution, 독립, 동일 분포)

이렇게 정의하게 될 경우 Backpropagation을 위한 조건 2가지를 모두 만족 시킬 수 있게 된다. 

이때의 결과값은 Likelihood 값이 아닌 처음 정의한 확률분포의 모수(Parameter)가 된다. 

<img src="https://user-images.githubusercontent.com/77658029/156150866-8f6b10fe-546f-414c-a1a4-24ab68c87d3b.png"  width="70%" height="70%"/>

### Loss Function 계산

분포에 따른 Loss Function을 구하게 되면,

Gaissian 분포의 경우 MSE와 동일하고, Categorical(Bernoulli) 분포의 경우 CE와 동일한 식인 것을 알수 있다.

<img src="https://user-images.githubusercontent.com/77658029/156151395-66c2150f-4f53-4c62-856e-88c6a8fd8268.png"  width="70%" height="70%"/>

### Log Likelihood 정리

<img src="https://user-images.githubusercontent.com/77658029/156151902-26db9754-ce0f-4848-a2c2-cca1566694e9.png"  width="70%" height="70%"/>


## 정리

기존 Deep Learning에서 Gradient Descent 관점을 통하여 단순 분류예측에 사용하는 방법만 알고 있었다. 
하지만 Autoencoder는 Maximum likelihood를 활용하여 확률분포를 구함으로써 새로운 분야에 적용될 수 있는 가능성을 볼 수 있었다.


**📌reference**
- [오토인코더의 모든 것](https://www.youtube.com/watch?v=o_peo6U7IRM&t=3176s)

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

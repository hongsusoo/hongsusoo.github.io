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

title: "Autoencoder 기초(4/5)"
excerpt: "about : Autoencoder"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - DL Basic
tags:
  - [autoencoder]
date: 2022-03-08
last_modified_at: 2022-03-08
---

<br>
> 해당 글은 이활석님의 오토인코더의 모든 것 유튜브 영상을 바탕으로 제작되었습니다.

<iframe width="885" height="498" src="https://www.youtube.com/embed/rNh2CrTFpm4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

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

[chapter 1 정리](https://hongsusoo.github.io/dl%20basic/dl_autoencoder1)


---

# Variational Autoencoder

실질적으로 지금까지 공부했던 Autoencoder와 Variational Autoencoder는 다른 개념으로 이해가 필요하다. **Autoencoder**는 **Manifold learning**을 **unsupervised Training**을 하기 위해서 **decoder를 추가**해 입력과 출력이 동일한 형태로 만들었지만, **Variational Autoencoder**의 경우는 **Generative Model**로 **Decoder를 학습**시키기 위해 **Encoder를 연결**하게 되었고, 그 모양이 Autuencoder와 비슷한 모양인 것이다.

여기서 말하는 Generative Model은 모든 Training DB의 샘플들이 나올 확률을 최대화 하는 하나의 확률분포를 구하는 작업이다. 


Latent space가 굉장히 복잡할것 같은데, 단순한 Normal distribution이나 uniform distribution을 사용해도 p(x)-(train DB를 만족하는 확률분포)를 구할 수 있을까?

-> 하나의 network만 진행해도 많은 부분이 변경되는 것을 알 수 있다. 아래와 같이 가우시안 분포를 하나의 수식만 거쳐도 다양하게 바꿀 수 있기 때문에, Layer를 깊게 쌓으면 상관 없어진다.

<img src="https://user-images.githubusercontent.com/77658029/157209965-7564656a-17fc-409e-bd60-f650764246d9.png"  width="70%" height="70%"/>


다시 Variational Autoencoder의 내용을 보면

<img src="https://user-images.githubusercontent.com/77658029/157210224-51717b35-dc89-4538-9c36-95976d7f62c1.png"  width="70%" height="70%"/>

train DB에 있는 x들을 생성하기 위해서 확률분포 $p(z)$ 에서 z를 입력으로 넣게 된다. 이때 generator($g_\theta (\cdot )$)를 학습해 z를 입력으로 받아 $p(x)$가 최대가 되게 하는 확률분포를 구하는 것이 목적이다. 

이렇게 확률분포를 구하게되면, z를 변경하면서 기존 Train DB에 없었던 새로운 샘플들을 만들어 냄과 동시에 Train DB의 샘플들과 유사한 경향을 가지게 된다. 

이런 Generator를 학습하기 위해서는 어떻게 해야할까?

우선 기본적인 Maximum Likelihood 방법으로 학습을 진행해보자

## Basic Maximum likelihood 학습

<img src="https://user-images.githubusercontent.com/77658029/157211575-e27fcdd8-cea0-4d92-9529-3f7c39ccb6e2.png"  width="50%" height="50%"/>

생성기에 대한 확률분포는 likelihood로 가정하면, MSE 관점으로(chapter 1) Loss가 만들어지게 된다.
하지만 Image의 차이를 MSE로 비교하게 될 경우 문제가 발생하게 되는데, Image의 의미적 유사도와 Loss의 크기의 차이 사이에 관계가 없다. 

예를들어 밑에 있는 자료에서 (a)는 가지고 있는 샘플이고, (b),(c)가 생성된 샘플이라고 생각해보자

(b)는 (a)에서 특정 부분이 지워진 형태이고,

(c)는 (a)가 옆으로 shift된 이미지이다. 

여기서 pixel에 따른 MSE를 계산하게 되면, (b)가 (c)보다 더 작은 값을 가지게 되고 (a)와 더 비슷한 이미지로 학습하게 될 것이다. 

<img src="https://user-images.githubusercontent.com/77658029/157212415-efc397fe-c8c2-454b-8c6c-f97397b45271.png"  width="50%" height="50%"/>

어떻게 하면 이런 부분을 조정할 수 있을까?

## Variational Inference

여기서 한가지의 아이디어를 적용해보자, 

위 상황에서 문제가 된 상황은 (b)와 같은 이미지가 들어오는 것이었다. 

학습 데이터와 크게 다른 z들이 들어오면서 문제가 발생했다.

이전까지는 Random variable하게 z를 추출하였는데, z를 분포와 비슷한 녀석으로 학습하면 어떨까? 

하여 이상적인 확률분포 $p(z|x)$에 대해서 생각하게 되었다. 

train DB의 Data가 주어졌을때의 z값을 생각하는 것이다. 

<img src="https://user-images.githubusercontent.com/77658029/157224482-9acd9b95-5708-412d-8b9e-1cb92112aa2c.png"  width="70%" height="70%"/>

이상적인 $p(z|x)$를 구할 수는 없기 때문에 Gaussian Distribution를 활용해 Likelihood가 최대가 되는 새로운 분포를 구하려고 한다. 

구하고자하는 분포를 $q_\phi (z)$ 로 정의하면

- 실질적으로 구하고 싶은 분포 : $p(x)$
- 분포의 안정성을 주기 위한 latent 분포 : $q_\phi (z|x) \approx p(z|x)$ 

두 가지로 줄일 수 있을 것이다. 

이 두 가지의 관계를 이끌어 내기 위해 두 가지 방법이 있는데 

첫 번째는 Jensen's Inquality를 활용해 증명하는 방식으로 아래와 같이 증명한다.
<img src="https://user-images.githubusercontent.com/77658029/157226922-afd1c4e0-bd21-4c7f-a630-f6a56ec1835a.png"  width="70%" height="70%"/>
(여기서 수식이 반대로 되어야 할것 같음)

두 번째는 확률의 합은 1, 베이지안 정리를 사용하여 정리한 식이다.
(여기서 $p(x,z) = p(x\cap z)$ 로 사용한 것으로 보임)

<img src="https://user-images.githubusercontent.com/77658029/157228195-ac0651fc-1ae4-45fc-97f3-7cc5bea8b861.png"  width="70%" height="70%"/>
<img src="https://user-images.githubusercontent.com/77658029/157228280-e5ac2f90-2fb5-4d3c-8a4e-75dfb44295ac.png"  width="70%" height="70%"/>

지금까지 이미지를 생성하기 위한 분포를 측정하는 수식들을 유도하였는데, 

network를 학습하기 위해서는 Loss Function으로 만들어주는 작업이 필요하다.

## Loss Function

Variational Autoencoder의 원리에 대해서 생각해보면, 특정 latent vector로 부터 샘플 x를 생성하기 위한 decoder와 그 latent vector를 추정하기 위한 encoder로 구성된다. 

수식적으로 봤을때는 Autoencoder와 차이점이 있지만 구성자체는 동일한 형태를 가진다. 

아무튼 우리는 encoder와 decoder에 대한 최적화가 필요하게 되고 두 수식을 정리하면 아래와 같다

<img src="https://user-images.githubusercontent.com/77658029/157228846-930b5b5b-e2fb-405f-9f81-c3d562100cc9.png"  width="50%" height="50%"/>
<img src="https://user-images.githubusercontent.com/77658029/157228979-bd073da1-ce65-4d65-abe7-a812a665cb46.png"  width="50%" height="50%"/>
<img src="https://user-images.githubusercontent.com/77658029/157229033-431c996a-a2a0-4582-839e-b5d5529d550a.png"  width="50%" height="50%"/>

Loss에 대한 term은 regularization과 reconstruction 두 가지로 구성된다. 

### Regularization

KL Divergence로 표현되는 부분이다. 

KL Divergence는 두 확률분포의 차이를 계산하는데 내부 수식을 살펴보면 cross entropy와 동일한 형태로 이뤄져, 기준이 되는 분포(여기선 normal distribution)와 예측하고자하는 분포($q_\phi (z|x)$)의 차이를 cross entropy적으로 구한 것이라고 생각하면 편할 것 같다.

분포를 추정하는 것이기 때문에 우리는 구하고자하는 분포의 모수를 구하는 것이 목적이 된다(여기서는 가우시안 분포로 추정하기 때문에 평균과 분산을 추정하게 된다)

수식으로 살펴보면 아래와 같다.

<img src="https://user-images.githubusercontent.com/77658029/157230482-3e85bd8e-894e-49f3-a10a-cea784bc69ac.png"  width="50%" height="50%"/>

### Reconstruction Error

이 부분은 위 Regularization에서 추정한 분포 $q_\phi (z|x)$ 에서 추출한 샘플을 입력으로 했을때, $p(x)$를 추정하는 것이다. 하여 단순한 Maximum likelihood로 접근할 수 있다. 

수식으로 살펴보면 아래와 같다.

<img src="https://user-images.githubusercontent.com/77658029/157230905-62dfb0fb-0475-4efb-a184-a3da5c65e54e.png"  width="50%" height="50%"/>

### Reparameterization Trick

위와 같은 방식으로 적용하게 되면, backpropagation을 바로 사용할 수 없는 곳이 생기게 된다.

바로 latent space에서 샘플을 추출하는 작업이다. Random하게 계산이 되기 때문에, backpropagation을 적용할 수 없게 된다. 이 부분을 수정하기 위해서 Reparameterization Trick를 사용하게 된다. 

아래와 같은 방법으로 가우시안 분포에서 평균과 분산을 따로 떼어내어 parameter화 진행하는 방식이다. 

수식상으로는 동일하기 때문에 분포를 정규화하여 parameter를 추출한 것이라고 생각할 수 있을 것 같다.


<img src="https://user-images.githubusercontent.com/77658029/157231429-97f12ad7-4f94-4f48-8db5-738d9df1ebcf.png"  width="50%" height="50%"/>




**📌reference**
- [오토인코더의 모든 것](https://www.youtube.com/watch?v=rNh2CrTFpm4)
- [KL-divergence]](https://hwiyong.tistory.com/408)

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

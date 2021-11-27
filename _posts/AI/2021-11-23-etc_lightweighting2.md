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

title: "경량화 모델 찾기 : AutoML"
excerpt: "about : 경량화"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - AI ETC
tags:
  - [경량화, AutoML]
date: 2021-11-23
last_modified_at: 2021-11-23
---

<br>

## 기존 Deep Learning 과정

- 최적의 모델과 Hyperparameter를 구하기 위한 끊임없는 반복의 과정

![image](https://user-images.githubusercontent.com/77658029/142879225-5874b114-46a3-449d-825e-4fa3b11b9bea.png)

**❗❓ 이런 단순 반복적인 작업을 자동적으로 할 수 없을까?**

## 경량화 모델 찾기 : AutoML

- 모델을 경량하기 위해 2가지 접근 방법이 있음
    1. 주어진 모델을 경량화 : Pruning, Tensor Decomposition
    2. 새로운 경량화 모델 찾기 : NAS, AutoML
    
- AutoML은 Search를 통한 경량 모델을 찾는 기법

![image](https://user-images.githubusercontent.com/77658029/142881549-550ea946-2eb3-4014-be01-f8fade181dc5.png)

### AutoML 문제 정의(HPO)

- HPO : Hyperparameter Optimization
    - Loss를 최소화하는 Configuration $\lambda^{*}$를 탐색하는 문제
![image](https://user-images.githubusercontent.com/77658029/142880658-27fd886f-4a03-4c16-b6f3-4e3e8bd8a8e0.png)
- Search Space
    - Categorical : Optimizer(adam, SGD), Module(Conv, BottleNeck, InvertedResidual)
    - Continuous : Learning Rate, Regularize Parameter
    - Integer : Batch size, Epochs

### Bayesian Optimization(BO)

![image](https://user-images.githubusercontent.com/77658029/142881690-a7a3cf40-1ac9-4ca4-aaf5-b3da55a626cb.png)

- Surrogate Function : $f(\lambda)$의 Regression model
- Acquisition Function : 다음 확인할 Point 선정

### Bayesian Optimization(BO) 과정 설명 - GPR

![image](https://user-images.githubusercontent.com/77658029/142886007-4fb9167c-9f0c-4bd6-aa86-bbec4de00ec0.png)
- GPR : Gaussian Process Regression
- Regression의 경우 주어진 Data로 에측하고 싶은 f에 가장 가깝게 근사시키는 것
- 기존에 주어진 $(X,Y)$와 새롭게 주어진 $X_{\ast}$를 활용하여 $Y_{\ast}$ 추정
- 단점은 High-dim(O(N^3)), Continuous, Discrete가 혼재된 경우 적용 어려움

#### 추정 과정

1. 함수들의 분포를 가정함(여기서는 Multivariate Gaussian Distribution)
    - $Y_{*} = f(x)$를 Random Variable로 보고 다른 Random Variable들도 모두 Multivariate Gaussian Distribution관계에 있다고 가정
    - $f(x)$는 Gaussian Process를 따름

⭐$Kernel$은 두 가지 벡터의 유사도를 나타내는 함수로 내적과 비슷한 의미를 가짐


### Bayesian Optimization(BO) 과정 설명 - TPE

- TPE : Tree-structured Parzen Estimator
- 연산 : GPR는 GPR($p(f\vert\lambda)$)연산을 하지만, TPE는 $p(f\vert\lambda)$와 $p(\lambda)$를 계산함
- 현재까지의 Observation들을 특정 Quantile(inverse CDF)로 구분
- KDE(Kernel Density Estimation)으로 Good Observation 분포(p(g)), bad Observation의 분포 (p(b))를 각각 추정
- p(g)/p(b)는 EI(Expected Improvement, Acquisition Function중 하나)에 비례하여 높은 값을 가지는 $\lambda$를 다음 Step으로 설정

![image](https://user-images.githubusercontent.com/77658029/142892429-f074b290-f8ad-4be4-8106-a55129e10da0.png)


## 한계점

- 소요 시간이 크고 Scalability 등의 문제가 있음

![image](https://user-images.githubusercontent.com/77658029/142894044-6c96312b-ee90-4d55-a6cb-7e324b7d6bbf.png)

## 극복하기 위한 노력

- Hyperparameter Gradient Descent(탐색과 학습을 동시에 진행)
- Meta-Learning(Auto "AutoML")
- Multi-Fidelity Optimization
    - Data의  Subset만을 활용
    - 적은 Epoch
    - RL을 활용한 적은 Trial
    - Image Downsampling
- RandomAugmentation을 통한 시간 절약

⭐어느정도 Prior 개입, 적은 Search space, 대표성을 가지는 Subset 활용, early terminate(ASHA Scheduler, BOHB(Bayesian Optimiation & Hyperband) 등등 기법을 활용하여 좋은 결과를 얻을 수 있음

![image](https://user-images.githubusercontent.com/77658029/142959858-12d6ad77-b3ed-43c1-a876-6b0288dc7dcd.png)

- Search space : module block 7개, Hyperparameter고정, batch 128, epoch 200, SGD, Cosine annealing, Randaug 적용


**📌reference**
- boostcourse AI tech
- [Kernel](https://sonsnotation.blogspot.com/2020/11/11-1-kernel.html)
- [GPR](https://sonsnotation.blogspot.com/2020/11/11-2-gaussian-progress-regression.html)
- [시각화 Exploration Gaussian Process](https://distill.pub/2019/visual-exploration-gaussian-processes/)
- [[Gaussian process 참고자료] Bayesian Deep Learning; 최성준 교수님](https://www.edwith.org/bayesiandeeplearning/lecture/24811?isDesc=false)
- [A Visual Exploration of Gaussian Processes](https://distill.pub/2019/visual-exploration-gaussian-processes)
- [Towards automating machine learning - Dr Thorben Jensen](https://www.youtube.com/watch?v=7lvwCZsrTn4)
- [Algorithms for Hyper-Parameter Optimization](https://papers.nips.cc/paper/2011/file/86e8f7ab32cfd12577bc2619bc635690-Paper.pdf)


<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

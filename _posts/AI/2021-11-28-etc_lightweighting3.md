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

title: "경량화 방법 : Pruning"
excerpt: "about : 경량화"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - DL etc
tags:
  - [경량화, pruning]
date: 2021-11-28
last_modified_at: 2021-11-28
---

<br>

# 경량화 - Pruning

- Pruning : 중요도가 낮은 파라미터를 제거하는 방법

## Pruning 종류

- Pruning 단위에 따라 크게 두 가지(Structured, UnStructured)로 구분 가능함
- Structured : Group 단위
- UnStructured : fine grained 단위

### Structured Pruning
 
- 파라미터를 그룹 단위로 Pruning 진행
- 그룹 단위 : Channel, Filter, Layer Level 등으로 정의하여 진행 가능함
- Masked (0으로 Pruning 된)된 그룹으로 실질적인 연산 횟수를 줄일 수 있어 속도 향상에 직접적인 영향이 있음

#### **🔍관련 논문**

1. Learning Efficient Convolutional Networks Through Network Slimming(ICCV 2017)
    - 단위 : Structured
    - 기준 : BatchNorm Scaling Factor $\gamma$
    - 적용 : Global
    - Phase : 학습된 모델
    - 각 filter에 BN의 Scaling Factor $\gamma$가 곱해지기 때문에, Scaling Factor $\gamma$가 커지면, filter weight 크기는 일반적으로 커질 것으로 예상
    - Scaling Factor $\gamma$ 크기를 기준으로 p%의 채널을 pruning 진행
    - Scaling Factor $\gamma$에 L1-norm을 Regularize로 사용하여 Insignificant Channel들을 자연스럽게 Prune 되도록 유도함
    - ImageNet 기준, VGG11,  50% Pruning, FlOPS 30.4%, 파라미터 수 82.5% 감소
    
<img src="https://user-images.githubusercontent.com/77658029/143731866-35e7121f-7509-4e5c-93bf-3312c9f60878.png"  width="70%" height="70%"/>
<img src="https://user-images.githubusercontent.com/77658029/143732381-50dc4a96-1a9c-46f8-9a7b-da903de94e8d.png"  width="50%" height="50%"/>

2. HRank:Filter Pruning using High-Rank Feature Map(CVPR 2020)
    - 단위 : Structured
    - 기준 : Feature map filter SVD Rank
    - 적용 : Local
    - Phase : 학습된 모델
    - Weight가 아닌 Feature map output을 보자
    - Feature map output의 각 Filter SVD를 적용하여 Rank를 계산함
    - **But, Feature map output은 이미지에 따라 달라지지 않나?**
    - 해당 논문에서는 **Random한 image들의 Feature map output**을 계산하여 Rank를 구해보니 실험적으로 **차이가 없음**을 확인함    
    - ResNet50, ImageNet 기준 약 44%의 FLOPS 감소, 1.17% 성능 하락
    <img src="https://user-images.githubusercontent.com/77658029/143770018-0334d6a9-b69a-43c5-b748-f9f9b25e7e2e.png"  width="70%" height="70%"/>
    - 계산은 torch에 matrix rank 계산 함수를 이용하여 사용 가능함
    
### UnStructured Pruning

- Parameter 하나하나를 독립적으로 Pruning 진행
- 행렬이 점점 Sparse 해지게 되지만 Filter의 수가 없어지는게 아니기 때문에 실질적인 속도가 계선되진 않음
- 하지만 Sparse Representation에 대해서 연산 가속이 가능하면 속도가 계선될 수도 있음
<img src="https://user-images.githubusercontent.com/77658029/143770659-54e61a09-1726-4c30-8400-389e43520fce.png"  width="70%" height="70%"/>

#### **🔍관련 논문**

1. The Lottery Ticket Hypothesis : Finding Sparse, Trainable Neural Networks(ICLR 2019)
    - 단위 : Unstructured(fine grained)
    - 기준 : L1 Norm
    - 적용 : Global
    - Phase : 학습된 모델
    - 방법 : 약간의 Prune → 재학습 → 약간의 Prune → 재학습 ...(iterative pruning)
    - Prune된 Sparse한 모델들은 일반적으로 학습이 어려움
    - Lottery Ticket Hypothesis : Dense하고, Randomly-initialized된 feed-forward Net은 기존 original Network와 필적하는 성능을 갖는 sub-networks(winning tickets)을 갖는다는 가정(Pruning-obtained network들 중 original network만큼 학습이 잘되고, 높은 accuracy를 갖는 sub-networks가 있을 것을 가정)
    - 이런 Lottery Ticket(sub network)를 찾기 위한 방법론을 제시하였고, 10~20%의 Weight만으로 원 network와 동일 성능을 냄
    - Identifying Winning Tickets 구하는 방법
        1. 네트워크 초기화 $f(x;\theta_{0})$
        2. 네트워크를 학습하여 parameter $\theta$를 구함(j번째 학습하면 $\theta_{j}$)
        3. parameter $\theta_{j}$를 $p\%$ 만큼 pruning 진행 → mask $m$를 생성(p는 보통 20%)
        4. 살아남은 Parameter(Mask되지 않은 애들)를 초기 Parameter($\theta_{0}$)로 되돌림, 이때 나온 결과를 Winning Ticket($f(x;m\odot\theta_{0})$, mask된 영역은 0으로 나머지는 $\theta_{0}$(초기화)로 정의함)이라고 함
        5. Target Sparsity(e.g. 90%)에 도달할때까지 B - D 반복 진행(10회 진행할 경우 $(1-0.2)^{10} \approx 10.7\%$)

    - **간단한 Idea로 좋은 성능**을 뽑아내고, Pruning 후 Fine tuning하는 방식을 고집하던 기존 틀을 깨고 **새로운 패러다임**을 제시함
    - **하지만**, **매우 느린 학습시간**

2. Stabilizing the Lottery Ticket Hypothesis(arXiv 2019) ; Weight Rewinding 
    - LTH(Lottery Ticket Hypothesis)의 경우 데이터셋이나, 네트워크의 크기가 커졌을때 불안정한 모습이 있었음
    - 그래서 기존 LTH에서 Parameter를 **초기화 하여 재학습하는 것이 아닌** **k번째 Epoch의 학습 Parameter를 사용**하여 안정화 시킴
    - 논문에서는 총 Iteration의 0.1~7% 지점을 Rewinding point로 언급함
    - Weight와 Learning Rate 모두를 Rewind(되돌려)서 Pruning → Retrain 진행함
<img src="https://user-images.githubusercontent.com/77658029/143775056-9d71ff40-82fd-4482-b2a9-c5d0ea9b7f0c.png"  width="85%" height="85%"/>
    
3. Comparing Rewind And Fine-Tuning In Neural Network Pruning(ICLR 2020); Learning Rate Rewinding
    - 2번 논문에서 사용한 Weight Rewinding는 하지 않고 Learning Rate만 Rewinding하여 진행함
<img src="https://user-images.githubusercontent.com/77658029/143775088-bafd9e97-f7d9-4651-99be-28bbf55fde59.png"  width="85%" height="85%"/>    

**💡 LTH** 
- 왜 아직 잘되는지 설명이 안됨(But, RL, NLP 등등 다양한 분야에서 적용이 가능함이 Report되고있음)
- 특정 initialization에 대해서, 학습 후 도달하는 공간이 유사? → 네트워크의 학습 및 수렴 관련 연구와 접목되는 부분

4. Linear Mode Connectivity and the Lottery Ticket Hypothesis(ICML 2020)
    - 네트워크의 학습 및 수렴 관련된 실험
    - 특정 학습 시점(epoch at 0,k)에서 seed를 변경하여 두 개의 Net을 학습 후 비교해봄(SGD를 통한 계산 결과가 다르기 때문에 다른 곳으로 수렴)
    - Seed를 통해 다른 Weight를 학습한 후 두 Net Weight의 Linear interpolation을 사용하여 weight간의 어떤 관계성을 확인해 보고자함
     
    - $W_0$를 사용하였을 경우에는 Weight값이 수렴 자체를 안하는 경향성이 보였지만,
    <img src="https://user-images.githubusercontent.com/77658029/143775480-07976360-68df-4a15-9f3e-cd0a732ac82f.png"  width="85%" height="85%"/>
    - $W_k$를 사용한 경우 특정 **k번째에서 수렴**하는 결과가 나오기 시작함
    <img src="https://user-images.githubusercontent.com/77658029/143775773-8d49a7a1-e0d3-48c4-8207-7a3b956c1e30.png"  width="85%" height="85%"/>
    - 두 가지 결과를 비교해보고 생각해 봤을때 어느 정도 학습이 진행되면 한 Plate위에서 학습되는게 아닐까?라는 의문을 남겼고, 이 부분이 LTH와 어떻게 관련이 있는지 많은 연구들이 진행되고 있음
    <img src="https://user-images.githubusercontent.com/77658029/143775822-485fd25a-d3f2-4ddd-9298-fdc188253c9e.png"  width="85%" height="85%"/>
    
5. Deconstructing Lottery Tickets:Zeros, Signs, and the Supermask(NeurIPS 2019)
    - LTH의 경우 $w_f$를 L1 norm으로 줄세워 Masking 진행하게 되는데, 이때 $w_i$를 함께 비교하는 방식을 제안함
    <img src="https://user-images.githubusercontent.com/77658029/143776050-7e6717b9-a249-4ed8-8dd4-a2ee50752f8d.png"  width="85%" height="85%"/>



## 정리 

### 아쉬운점
 
- Structured/Unstructured 모두 간단한 Architecture 벤치마크를 수행함(MobileNet, EfficientNet, NASNet 등 Modern한 Architecture는 잘 다루지 않음)
- 다양한 Architecture에 적용하려면 여러가지 예외처리, 추가 검증을 필요로함(Transformer는 그래도 덜한 편)
- 파라미터 수, FLOPs로 비교를 많이 하지만, 실질적으로 Latency 향상 정도와는 거리가 있음, 아직까지 Unstructured에서 연산 가속이 되는 HW가 많지 않음, 지원하는 추세이지만 아직 제약사항이 많음
- 연구 복잡도가 복잡해지는 정도에 비해 효과는 크지 않은 것 같음

### 강점

- 여전히 연구적 가치가 높고, 여러 분야와의 접목이 일어나는 추세
- 

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

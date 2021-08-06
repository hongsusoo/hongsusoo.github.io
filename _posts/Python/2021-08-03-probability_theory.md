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

title: "[AI basic] 확률론(probability theory)"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - AI basic
tags:
  - [python, AI Math]
date: 2021-08-03
last_modified_at: 2021-08-03
---
<br>

# 확률론

## 딥러닝에서는 왜 확률론이 필요할까?

- 딥러닝은 확률론 기반의 기계학습 이론에 바탕을 두고 있음
- 기계학습에서 사용되는 손실함수(loss function)들의 작동 원리는 데이터 공간을 통계적으로 해석해서 유도하게 됨
- 틀릴 확률(risk)를 최소화 하는 방향으로 훈련하게됨
- 회귀분석 : 손실함수로 사용되는 L2-norm은 예측 오차의 분산을 가장 최소화 하는 방향으로 학습($y-\hat y$)
- 분류문제 : 교차엔트로피(cross-entropy)는 모델 예측의 불확실성을 최소화하는 방향으로 학습
💡 분산 및 불확실성을 최소화 하기 위한 측정 방법을 알아야 하기 때문에 확률론 공부해야함!

## 확률분포

- 데이터 공간 $\mathscr{X}\times\mathscr{Y}$에서 데이터를 추출해서 만든 분포를 $\mathscr{D}$라고함
- 데이터는 확률변수로 $(X,y)~\mathscr{D}$ 표기
- 확률변수는 이산, 연속 두 가지가 있는데, 확률분포 $\mathscr{D}$에 따라 구분됨(데이터 공간이 아님)
- 만약 데이터 공간이 실수형일때 -0.5~0.5 사이값을 분포의 기준으로 잡으면 이산형이 되기 때문



### 이산형 확률변수

- 확률변수가 가질 수 있는 경우의 수를 모두 찾아 확률을 더하는 방식으로 모델링

![image](https://user-images.githubusercontent.com/77658029/127948071-e5cc84fe-e809-4acf-8181-a961d73b1255.png)

### 연속형 확률변수

- 데이터 공간에 정의된 확률변수의 밀도함수(density)를 적분하는 방식으로 모델링
- 밀도의 경우 누적확률분포의 변화율로 모델링, 확률로 해석하면 안됨

![image](https://user-images.githubusercontent.com/77658029/127948691-24250148-c268-4907-acd1-3098f49ef26a.png)


### 결합확률분포

- 두 가지 이상의 데이터 공간에 대한 확률 분포

![image](https://user-images.githubusercontent.com/77658029/127949308-4983be70-02b4-429c-9eb3-29f8a6ee041e.png)

### 주변확률분포

- 그림에서 보면, $\mathscr{X,Y}$는 연속형 데이터의 성질을 띄지만, 빨간색 box를 만들었을때는 이산형으로 타나날 수 있음
-  $\mathscr{X,Y}$의 결합분포에서 p(x)는 x에 대한 주변확률분포라고 부름, 이때는 y에 대한 정보는 따로 주어지지 않음

![image](https://user-images.githubusercontent.com/77658029/127950293-2783b1dc-7fe2-4e73-9455-bf1df3c23dd2.png)

### 조건부 확률분포

- 입력변수 x에 대해서 정답이 y일 확률을 의미함(연속확률분포의 경우 확률이 아니라, 밀도임을 잊지말자)
- P(y|x)로 표현함



## 조건부확률과 기계학습

- 



<br>
```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

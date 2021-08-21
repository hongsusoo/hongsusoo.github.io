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

title: "[DL Basic] Optimization"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - AI
tags:
  - [python, AI Model, optimization]
date: 2021-08-10
last_modified_at: 2021-08-10
---

<br>

# Optimization

## Optimization 용어 정리 

### Generalization

- Train data에서 error를 줄일 수 있지만 
- Test data를 넣어 반복하면 error 가 커질 수 있다 
- 이때 Train data error와 Test data error의 차이를 generalizaion gap 이라고 한다
- 좋은 Generalization가 좋다 라고하면, Train data와 Test data 사이의 차이가 작다

![image](https://user-images.githubusercontent.com/77658029/128792998-954a64ef-72ef-4741-8530-3204d4e258f3.png)

<br>

### Under-fitting vs Over-fitting

- 이론적인 얘기로 컨셉으로 알고 가면 좋음
- train data가 test data의 일부를 가졌왔다고 가정했을때
- Over-fitting : Train data의 세세한 부분까지 fitting되어 test data를 잘 설명하지 못하는 경우
- Under-fitting : 학습량이 부족하거나 너무 일반화하여 Train data 자체를 잘 만족하지 못하는 경우
- Balanced : 적절한 경우
 
<br>

### Cross Validation

- train data를 여러개로 나눠서, 그 중 일부를 학습시키고 남은 train data로 validation을 진행한다
- 다음 시도해서는 다른 일부를 학습시키고 다시 남은 train data로 validation을 진행한다
- 이런 작업들을 통해 Hyperparameter를 최적화
- hyper parameter : learning-rate, loss function, batch size, training 횟수(epoch) 등 우리가 정하는 값
- 예시로 k-fold 방법이 있음
- 우리는 절대로 test data를 사용할 수 없다!

![image](https://user-images.githubusercontent.com/77658029/128794259-00507c8a-e44c-471e-b884-cbb3cec0f05c.png)

<br>

### Bias - Variance tradeoff

- variance : 동일한 입력을 넣었을 때 출력이 얼마나 일관적인가
- variance가 커지면, 한곳으로 모이고, 작아지면 펼쳐짐
- Bias : 동일한 입력에서 평균적으로 True Target과 얼마나 차이가 있는지
- Bias가 크면 True Target과 멀리 떨어진 상황이고, 작으면 가까운 상황임

![image](https://user-images.githubusercontent.com/77658029/128794533-a3781c71-840d-4775-ab61-42aa241d0e76.png)

**💡 trade off **

- 어떤 error를 최소화 할 때, 이것은 $Bias^2, Variance, Noise$ 3가지로 구성할 수 있는데, 
- 하나가 작아지면, 다른 항목이 커지는 Trade off관계가 있음

![image](https://user-images.githubusercontent.com/77658029/128794917-bd523592-24a0-47ec-9a0e-ab7ff9fb83b7.png)

<br>

### Bootstrapping(in statistics)

- train data에서 전체를 다 사용하는 것이 아니라 일부를 뽑아서 여러개의 train data를 만들어주는걸 bootstrapping이라고 함
- 이렇게 만들어진 모델의 consensus를 확인하여 모델의 정확도를 확인함

<br>

### Bagging and Boosting

- Bagging(**B**ootstrapping **agg**regat**ing**)
    - bootstrapping한 data로 여러 모델을 훈련시킴
    - 이렇게 나온 결과값을 투표하거나, 평균을 내서 결정하게됨
    - ensemble이 이런것이고, 이렇게 했을 때 결과가 좋은 경우가 있음(Kaggle에서 많이 사용함)
- Boosting 
    - 약한 learner를 여러개를 sequential하게 연결하여 하나의 강한 learner를 만들어주는 것
    - 한 모델을 만들었는데, 100개중 60개만 구별할 수 있다면, 나머지 40개에 대한 다른 모델을 만들어 연결해주는 방식을 반복해서 연결함

![image](https://user-images.githubusercontent.com/77658029/128797271-9ff37893-9857-407b-b476-d4495bfb2dfe.png)

<br>


## Practical Gradient Descent

- Stochastic Gradient Descent : single sample
- Mini Batch Gradient Descent : subset(minibatch : 128,256.. 등 사용)
- Batch Gradient Descent : whole data

<br>

### Batch-Size Matters

- Bathc Size에 따라서 training function의 경사도가 달라짐
- Large batch Method를 사용할 경우, Sharp Training Function을 얻을 수 있어 약간의 오차에도 크게 반응을 하여 성능이 Test 상황 시 성능이 떨어질 수 있음
- Small batch Method를 사용할 경우, Flat Training Functing을 얻을 수 있어, 약간의 오차에도 작게 반응을 하여 Test 상황 시성능에 큰 변화가 없을 수 있음

![image](https://user-images.githubusercontent.com/77658029/128798611-7bc50e96-5e3a-45f8-9a1c-341e4cd55af6.png)

<br>

### Gradient Descent

- gradient값에 learning rate를 곱해줘서 다음 항으로 넘겨줌
- learning rate에 따라서 크게 좌우된다는 단점이 있음

![image](https://user-images.githubusercontent.com/77658029/128799663-1328008a-8e9a-4631-987e-d0a5d6603bb5.png)

<br>

### Momentum

- Gradient값에 Momentum이라는 이전 Gradient에 대한 부분을 일정부분 반영하여 다음항으로 넘겨줌
- 만약 local minimum 부분을 지나치면, 바로 다시 돌아오지 못하고 좀더 올라 갔다가 내려와서 좀 더 늦게 수렴하게 됨

![image](https://user-images.githubusercontent.com/77658029/128800100-e5849494-eab7-4a25-936d-6c846a97197f.png)

<br>

### Nesterov Accelerate

- 이번에 계산된 gradient와 다음으로 갈 곳을 미리 연산하여 두 가지 벡터를 더해줌
- local minimumer에 수렴하는 속도가 빠름

![image](https://user-images.githubusercontent.com/77658029/128800345-7aaf111d-0358-434d-95e5-647f3b951071.png)

![image](https://user-images.githubusercontent.com/77658029/128800440-698079d5-b0a1-4f93-bd7f-9b967f5b84a2.png)

<br>

### Adagrad

- 아다그라드
- 수정량이 자동으로 조정되는데 그 값이 $G_t$라는 Gradient 제곱합으로 늘어나기 때문에 시도 횟수가 늘어날 수록 변화율이 적어지게됨
- adapted learning이 진행됨
- 자동으로 learning rate이 변화되는 장점이 있지만
- 횟수가 늘면서 변화량이 줄어들어 수렴이 안되는 경우가 발생함

![image](https://user-images.githubusercontent.com/77658029/128802006-22ff1bd2-b0da-4d75-a91f-17da303e158f.png)

<br>

### Adadelta

- Adagrad에서 $G_t$값이 계속 커지는걸 방지하기 위해서 만든 모델
- learning rate가 없어서, 실제로 조정할게 많지 않아 자주 사용되지 않음

![image](https://user-images.githubusercontent.com/77658029/128807185-f941c17f-34dd-4005-a1eb-1cf528724971.png)

<br>

### RMSprop

- 정식 논문은 없지만 Geoffrey Hinton이 코세라 강의에서 제안
- 아다그라드에서 learning rate가 줄어드는걸 보완해줌

![image](https://user-images.githubusercontent.com/77658029/128807282-b041c70c-ec44-4dfa-a5db-fc251e281253.png)

<br>

### Adam(Adaptive Moment Estimation)

- Momentum과 adapted 두 가지를 모두 사용한 방식

![image](https://user-images.githubusercontent.com/77658029/128807647-cdcb69ec-7533-496b-a1bf-df15084e3ed5.png)


## Regularization

**Early Stopping** : Generalization performance가 나빠지기 전에 멈추자

![image](https://user-images.githubusercontent.com/77658029/128808228-3ab13e3f-f884-471b-89aa-8aa04316bcfe.png)

**parameter Norm Penalty** 

    - 부드러운 함수일 수 록 Generalization performace가 좋을 것이다라는 가정하에서
    - 학습시킬 때, weight도 함께 줄여나가는 방법( weight decayed)
    
![image](https://user-images.githubusercontent.com/77658029/128809166-17019e0d-08ad-4c59-8744-aed91cc61c81.png)

**Data Augmentation** 

    - data는 많을 수록 좋다
    
![image](https://user-images.githubusercontent.com/77658029/128809285-49c16225-11e3-4815-b77f-e93684c812f9.png)

    - 하지만 대부분의 경우 Training data는 한정적임
    - 그렇기 때문에 데이터를 돌리고 바꾸며 새로운 데이터를 생성해냄
    
![image](https://user-images.githubusercontent.com/77658029/128809357-f4065a9f-f66c-4b99-889f-62b0a00380a7.png)


**Noise Robustness**

    - input과 weights에 Noise를 넣고 학습시키면, 더 성능이 좋아짐
    
![image](https://user-images.githubusercontent.com/77658029/128809576-8de1f352-34c7-4545-9f12-b3b4656b523c.png)

**Label Smoothing**

    - 데이터 2개를 뽑아서 섞어주는 작업
    - 분류문제를 풀때, decision boundary를 찾게되는데 이때는 이거 아니면 이거 선이 확실하게 그어져 있는데
    - 이 decision boundary를 부드럽게 만들어주는 작업

![image](https://user-images.githubusercontent.com/77658029/128809837-23b52bec-0c7c-4bb6-8fef-8843d3f581b0.png)

**Drop Out**

    - 몇몇 뉴런의 값을 zero 바꿔주는것
    - 명확하게 수학적으로 밝혀지진 않았지만, 성능향상됨
   
![image](https://user-images.githubusercontent.com/77658029/128810056-d083f0bb-1ec9-4418-9aee-6119edb6fa98.png)

**Batch Normalization**

    - Layer마다 정규화를 진행함(평균을 빼서, 표준편차로 나눠줌)
    - Layer가 깊게 쌓일 수록 성능이 좋아지는 현상을 보임

![image](https://user-images.githubusercontent.com/77658029/128810486-273f6424-8115-433b-8b4a-fa9639becbf1.png)

<br>

**📌reference**
- boostcourse AI tech
- [from the bottom](https://hyeonnii.tistory.com/232)

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

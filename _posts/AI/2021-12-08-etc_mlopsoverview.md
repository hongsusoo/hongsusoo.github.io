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

title: "MLOps 개론"
excerpt: "about : "
toc: true
toc_sticky: true
toc_label: "Label"
categories: 
  - AI ETC
tags:
  - [MLOps]
date: 2021-12-08
last_modified_at: 2021-12-08
---

<br>

# MLOps 개론

## MLOps란?

- MLOps : ML(Machine Learning) + Ops(Operations)
- 머신러닝 모델을 운영함에 있어서 반복적인 업무를 자동화하는 과정
- 머신러닝 엔지니어링 + 데이터 엔지니어링 + 클라우드 + 인프라를 총 망라하는 의미
- 비즈니스적인 가치를 창출하거나 올리기 위하여 ML dev.과 ML Ops에서 발생하는 문제나 반복적인 업무를 최소화하는 방법을 찾아가는 것!

## 어디서, 어떻게 사용할까?

- 모델 개발 프로세스  
    - Research : 문제정의 → EDA → Feature Engineering → Train → Predict
    - Production : 문제정의 → EDA → Feature Engineering → Train → Predict → Deploy

🚨프로세스로만 보면 큰 차이는 없어보이지만, 학습된 모델을 앱, 웹 등의 서비스에서 사용할 수 있는 Real World 혹은 Production 환경으로 배포하는 부분에 큰 차이를 발생시킨다. 이 차이에서 발생하는 Loss를 줄이기 위한 방법으로 MLOps가 사용될 수 있다. 


### Research vs Production

- **Research 🌏 :**
    - 환경 : 제한적이고 일관적인 **실험 환경**
    - Data : **고정적인 Data**사용(예외변수에 대한 처리가 굳이 필요 없음)
    - 학습 : 고정적인 환경, Data로 인하여 학습의 결과의 편차가 크지 않음
- **Production 🌏 :**
    - 환경 : **Real world**로 어떤 환경에서 Test 될지 예상하기 힘듦
    - Data : inference가 어려운 **새로운 Data**가 입력으로 주어질 수 있음
    - 학습 : 새로운 type의 data, 변동성 있는 환경으로 학습의 결과의 편차가 커짐
        → 배포상태에서 **새로운 데이터로 추가 학습**이 필요할 수도 있고, 추가 학습으로 인한 **성능 저하**가 생길 수 있게되어, backup을 위한 방안 등 **추가적인 기능 필요**

<img src="https://user-images.githubusercontent.com/77658029/145130385-95aab773-30b7-4530-b381-6430ff0a1fed.png"  width="70%" height="70%"/>


## 접근법(학습법)

- MLOps를 접근하는 방법은 하나의 Task의 목적을 이루기 위한 수단으로 보는 것이 좋음
- MLOps에서 나오는 모든 라이브러리나 기능을 학습하는 것보단, MLOps의 각 Component에서 해결해야할 문제을 해결하기 위한 방식을 고민하고 학습하는 것이 좋음
- 현재 MLOps에서 많은 라이브러리들이 생성되고 죽어가고 있어 더 좋은 Tool이 나와 현재 쓰고 있는 라이브러리를 대체할지 모르기 때문에 내 상황에서 알잘딱 쓸 수 있는 방법을 학습하는 것이 중요함
- 모델을 코딩하는 것은 Production Serving 중에 정말 작은 부분에 해당하기 때문에 전반적인 흐름을 깨닫는 것이 중요함 

<img src="https://user-images.githubusercontent.com/77658029/145127574-9b2601af-9700-4665-abd7-2f5c58585ee8.png"  width="70%" height="70%"/>


## MLOps Component(피자집 비유)

집 - Research
가게 - Production
피자 - 모델

<img src="https://user-images.githubusercontent.com/77658029/145135454-450ba50c-e172-4f0c-bd2e-c8cfdb5c216f.png"  width="70%" height="70%"/>

1. 집에서 만들어 먹던 피자가 너무 맛있어서 장사를 시작함

2. 장사에서 사용할 재료들 선정(**data/feature**)
    - 집 : 대형마트, 동네마트에서 재료를 수집
    - 가게 : 재료 도매업체를 확인, 재료 검수 필요
    
3. 장사를 하기 위한 장소 선정 및 가게 Open(**H/W 구축**)
    - 집 : 이미 정해져 있음(Local GPU)
    - 가게 : 유동인구(예상 트래픽), 가게 평수(서버 CPU, Memory 등), 장소 구매/월세(자체 서버-온 프레미스, 클라우드), 점포확장 가능성(스케일업, 스케일 아웃)
        - 클라우드 : AWS, GCP, Azure, NCP 등
        - 온 프레미스 : 회사나 대학원의 전산실에 서버 직접 구축 

4. 피자 가게 Open(**Serving**)
    - 집 : 혼자 만들어서 먹음
    - 가게 : 현장 판매(실시간 Online Serving), 구독서비스(일정 주기로 Batch Serving) 등 판매 방식 선정
        - Batch Serving : 특정 주기(1일,1주,1달)에 맞춰서 모델 결과를 제공(Serving할 모델의 결과를 전달)
        - Online Serving : 실시간으로 모델 결과를 제공, 병목이 없어야하고 확장 가능하도록 구성되어야함


### 실험과 모델 관리(mlflow, wandb)

- 맛있는 피자를 만들기 위해서 여러 시행착오를 겪으며 요리를 진행함
- 머신러닝도 동일하게 성능이 좋은 parameter, 모델을 찾기 위해 여러 조건에서 실험을 하게 됨
- 여러 모델에 대한 여러 실험들에 대한 기록과 관리가 중요함

<img src="https://user-images.githubusercontent.com/77658029/145137566-ea041d0e-50f5-4bf0-bf91-875a93bffec6.png"  width="70%" height="70%"/>
<img src="https://user-images.githubusercontent.com/77658029/145137739-f0509e7b-66f3-4993-8cef-cc61d6d3f1b7.png"  width="70%" height="70%"/>

### Feature 관리(FEAST)

- 빠른 Serving을 위해서는 많이 사용되는 재료를 미리 손질하고 관리하는 것이 좋음
- 머신러닝에서도 이런 Feature 값들을 관리하면 보다 질좋은 서비스를 빠르게 제공할 수 있음
<img src="https://user-images.githubusercontent.com/77658029/145138204-d9424377-3e4d-468b-9614-720bceca3153.png"  width="70%" height="70%"/>
<img src="https://user-images.githubusercontent.com/77658029/145138241-da4d13ed-a325-4a7f-af05-fc565602ab10.png"  width="70%" height="70%"/>

### 품질관리(TFDV_Tensorflow Data Validation)

- 날씨에 의해서 재료가 바뀌거나, 대량 유통으로 재료의 상태가 괜찮은지 확인이 필요함
- 머신러닝 또한 새로운 데이터에 적응하는 품질 개선/관리가 필요하게 되는데, Feature분포 등을 통해서 관리가 필요함

### 품질 개선

- 피자는 시간이 지나면서 맛과 가치가 떨어지게됨
- 머신러닝 또한 시간이 지나며 새로운 데이터가 나오게 되며 성능이 점차 떨어짐
- 서빙을 하며 처음과 동일한 품질의 서비스를 제공하기 위해서 모델 retrain이 필요함
- 특정 주기를 정하여 Retrain을 시도하여 성능 유지/개선이 필요함
    1. 새로운 데이터가 생겼을때
    2. 정해진 기간(매일, 1주, 1달, 1년)
    3. 갑자기 매출 떨어진 경우(metric 기반)
    4. 요청에 의한

<img src="https://user-images.githubusercontent.com/77658029/145138858-de6ed1f0-f56b-4d2d-b17b-514a77067ddf.png"  width="70%" height="70%"/>
<img src="https://user-images.githubusercontent.com/77658029/145139127-afc1a098-1c5a-417d-8bc7-b582356bb1cf.png"  width="70%" height="70%"/>

### Monitoring

- 전체적인 사업이 잘되고 있는지, 돈의 흐름이나 유입인구 등 종합적으로 기록/분석하여 위에 component를 반복함

### AutoML(NNI - microsoft)

- 이제는 이런 일련의 과정을 자동으로 해주는 Tool이 나옴

<img src="https://user-images.githubusercontent.com/77658029/145139705-b074ba63-ef37-4523-ba42-d2a0a89fe03f.png"  width="70%" height="70%"/>

**📌reference**
- boostcourse AI tech
- [구글 클라우드](https://cloud.google.com/resources/mlops-whitepaper)
- [Superb AI 실리콘밸리의 MLOps](https://www.superb-ai.com/ko-ebooks/mlops-guide)

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

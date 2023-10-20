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

title: "Product Serving 방식 - Online, Batch"
excerpt: "about : "
toc: true
toc_sticky: true
toc_label: "Label"
categories: 
  - DL etc
tags:
  - [Product Serving]
date: 2021-12-09
last_modified_at: 2021-12-09
---

<br>

# Product Serving

- Production(Real World) 환경에 모델을 사용할 수 있도록 배포하는 행위
- ML 모델을 개발하고 사람들이 서비스를 이용할 수 있도록 하는 것 

## Serving 도구

### 웹 서버(Web Server)

- HTTP를 통해 웹 브라우저에서 요청하는 HTML문서나 오브젝트를 전송해주는 프로그램을 칭함
- 크게 Request(요청)와 Response(답변)의 대화로 이루어짐

<img src="https://user-images.githubusercontent.com/77658029/145324306-1c0d0af2-c559-4f5b-b475-3d37e398e532.png"  width="70%" height="70%"/>


### API

- API : Application Programming Interface
- 운영체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스를 통칭하는 말
- 특정 서비스를 배포할 목적으로 외부에 노출시켜둔 API가 있음
    - ex : 기상청 API, 지도 API, Python 라이브러리(Pandas, Pytorch, ...) 등등

<img src="https://user-images.githubusercontent.com/77658029/145327323-4e42c19d-67b6-4d30-abb6-2b1e1ecd9b8b.png"  width="70%" height="70%"/>


## Serving 방법

**※ 간단 용어 정리**
- Serving : 모델을 웹/앱 서비스로 배포하는 과정, ML 모델을 활용하고 서비스 하는 방식
- Inference : ML 모델에 데이터가 제공되어 예측
- 위 두 용어는 혼재되어 사용되는 경우도 있음(ex. Online Serving, Online Inference)

### Online Serving

- 요청(Request)가 올때 마다 실시간으로 서비스를 진행함
- ML 모델 서빙을 예시 : Client → 서버로 HTTP 요청(Request) → 서버 내 ML 모델 inference → 예측값 반환(Response)
- 실시간 예측이 필요한 상황
    - 기계 고장 예측 모델 : 센서로부터 실시간 데이터를 받아 고장을 예측
    - 음실 배달 소요시간 예측 : 과거 배달 이력, 교통정보, 음식 데이터를 기반으로 배달 소요시간 예측

<img src="https://user-images.githubusercontent.com/77658029/145339406-5d8cfb90-4c56-4aea-ac3b-4fd3d508cd1b.png"  width="70%" height="70%"/>

#### 구현 방법

1. 직접 API 웹 서버 개발 : Flask, FastAPI 등
2. 클라우드 서비스 활용 : AWS의 SageMaker, GCP의 Vertex AI 등
    - 장점
        - 직접 구축해야하는 MLOps의 다양한 부분이 만들어짐
        - 사용자 관점에선 Pytorch 사용하듯 학습코드만 제공하면 API서버가 만들어짐
    - 단점
        - 서비스에 익숙해져야 잘 활용가능함
        - 자체 제작보다 높은 단가
3. Serving 라이브러리 활용 : Tensorflow Serving, Torch Serve, MLFlow, BentoML 등

#### Latency 문제

실시간 예측이기 때문에 Latency(지연시간)를 최소화가 필요함

**Latency를 늘리는 요소**

1. 데이터 Input 시간 : Database에 있는 데이터를 추출하여 사용하는 경우가 있을 수 있고 이로인한 쿼리 및 결과를 받는 시간이 걸릴 수 있음 
2. 순수 모델 연산 시간 : RNN, LSTM 등의 무거운 모델일 수록 시간이 오래 걸리게됨, 복잡한 모델 보단 간단한 모델로 사용하여 줄이는 경우도 많음
3. 결과값에 대한 추가적인 보정 : 결과값을 단순 숫자나 유효하지 않은 값이 출력될 수 있기 때문에 보정하는 코드가 필요할 수 있음

**Basic한 해결 방법**

- 데이터 전처리 서버 분리(Feature 선 가공 - Feature Store)
- 모델 경량화
- 병렬처리(Ray)
- 예측결과 캐싱

### Batch Serving

- 어떤 시간이나, 개수 단위의 Batch 묶음의 데이터를 처리하는 방식(Workflow Scheduler에 맞춰서 진행)
- Online Serving과 다르게 따로 라이브러리가 있진 않음, 단순하게 개수나, 정해진 시간이 되면 Python main.py 형식으로 결과값을 출력함
- 데이터를 한 번에 처리하기 때문에 Latency에 영향이 적지만, 실시간 결과 출력은 어려움
- 추천 알고리즘, 수요 예측 등에 사용됨

<img src="https://user-images.githubusercontent.com/77658029/145339578-a3a35cd0-fb5a-4b5c-a910-77d765ce0150.png"  width="70%" height="70%"/>

**Workflow Scheduler - Airflow**
- 데이터 엔지니어링에서 자주 활용됨
- Linux의 Cron job

<img src="https://user-images.githubusercontent.com/77658029/145340484-f8ce393a-ff73-497d-a1b6-709e3b2990c1.png"  width="70%" height="70%"/>

### Edge Serving

- Device에 ML 모델을 올려서, 직접 Input을 받아 모델을 돌려 결과값을 출력하는 하나의 완성 되어있는 환경
- 라즈베리파이에 얼굴인식 모델을 구현하여 Display로 출력

### Online vs Batch

- Output 관점으로 Serving 방식을 선택하게 됨
    - Online : API 형태로 바로 결과 반환이 필요한 경우, 서버와 통신이 필요한 경우
    - Batch : 결과가 바로 필요하지 않은 경우(1시간에 1번씩 결과가 주어져도 괜찮은 경우)

**개발과정**

- 처음부터 Online으로 만드는 것보단, 실시간 모델 결과가 어떻게 활용되는지 보고, 점차 API형태로 변환하는 방식으로 진행

**📌reference**
- boostcourse AI tech-

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

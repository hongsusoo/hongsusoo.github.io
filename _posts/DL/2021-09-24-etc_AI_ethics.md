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

title: "AI와 윤리학"
excerpt: "about : Ethics for AI"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - DL etc
tags:
  - [AI Ethics]
date: 2021-09-24
last_modified_at: 2021-09-24
---

<br>

# AI와 Ethics

<br><br>

## 편향(Bias)

- 인공지능은 Data에 큰 영향을 받게 되는데 Data에는 편견이나 선입견이 이미 들어가 있을 확률이 높음
- 사회적으로 가지고 있는 이런 편향들을 학습하여 알고리즘을 사용할때 의도하지 않았던 부분들이 나올 수 있음
- ex)이루다, COMPAS

<br><br>

### COMPAS

- 현실판 마이너리티 리포트
- 미국의 '노스포인트'社가 개발한 빅데이터 분석 인공지능으로 유사한 다른 범죄자들의 기록과 특정 범죄자의 정보를 빅데이터 분석해 범죄자의 재범가능성을 계량화


**🚨 문제점**

- 인종차별에 대한 부분이 인공지능의 학습 pattern에 녹아들어갈 가능성이 있음
- 인공지능이 학습하는 pattern을 사람이 제어할 수 없는데, 이 blackbox영역에서 차별이 pattern화 되어 있으면 앞으로 우리가 인지하지 못한 상황에서 차별이 더 심해질 수 있음
- Data로 사용한 판례 data에 판사에 의한 사회적 편향이 들어가 있을 수 있음

![image](https://user-images.githubusercontent.com/77658029/134764067-4de12ea6-b00f-4069-b394-222a976c6c2c.png)

<br><br>

### Bias source

1. Class Defining
    - Data를 구성 시 Class에 대한 Labeling과 Target 변수를 정의할때 모호한 경우가 있음
    - 정의하기 모호한 부분에 의해서 편향이 발생할 수 있음
    - 좋은 직원을 뽑자 → 어떤 직원이 좋은 직원일까? → 오래 남아 있는 직원?, 생산성이 좋은 직원?

2. Training Data : Labeling 
    - Labeling 할때 Data를 만드는 사람의 편향이 들어갈 수 있음(성별, 나이, 지역 등에...)

3. Training Data : Collection
    - problem of Underrepresentation : Data의 Unbalanced, 지역적차이, 시스템적인 누락
    - smartphone의 가속도기를 사용하여 도로를 수리하고자 했는데, smartphone이 없는 사람들이 많은 지역은 도로 수리가 안될 수 있음
    - problem of overrepresentation : 소수에 변화에 민감하게 반응함

4. Feature Selection
    - 어떤 대학, 어떤 지역을 기준으로 만들어지는 Feature
    - 이 대학교를 다니면 일을 잘하겠지?
    - 이 동네에 살면 돈이 많겠지?
    
5. Proxies
    - 인공지능이 의도하지 않은 Pattern을 찾아내서 bias를 만들어내는 경우
    - 의도적으로 어떤 이득을 위해 bias를 만들어 내는것


<br><br>

## 사생활(Privacy)

- COVID19 상황에서 방역 vs 사생활 두 가지 Trade off가 있음
- privacy를 유지하면서 할 수 있는 방법들이 많이 제안되고있음


<br><br>

## Society Inequality

- AI를 사용하여 중요한 결정을 할때, Bias들이 Amplified 될 수 있음
    - 중요 결정들 : housing, Health insurance, Credit rating, Employment, Legal decisions
    - bias : Recial, Gender, Education, Regions
- AI는 결국 AI에 대해서 Access가 있고, 지식이 있는 사람들에게 이익을 가져올 것임

<br><br>

### Labor

- 자동화 시스템으로 기존 직업들이 대체됨
- 단순하고 수동적이고 반복적인 업무들부터 대체되고 있음

<br><br><br>

## misinformation

- GPT-3의 글쓰기 : 잘못된 News paper를 만들어 낼 수 있음
- Deepfake 

![image](https://user-images.githubusercontent.com/77658029/134765860-2703bbe0-d98c-451a-bbe7-e7c5b1ad06ba.png)

- 이런 Manipulation을 Detection하는 연구들이 많이 진행되고 있음
- typing하는 성향을 파악해서 누가 작성했는지 확인하는 기술들도 연구되고 있음

<br><br>

## Human Health

- 당뇨 환자들을 빠르게 Detection하는 기술(어떤 사람들에게서 발생할지 예측)
- 의학 영상을 보고 진단하는 기술 → 전문가보다 진단을 잘함
- 지속적인 Health care가 필요한 경우
- COVID-19 같은 

<br><br>

## Enviraonmental

- -) AI 모델을 학습시킬때 사용되는 CO2(이산화탄소) emissions Cost가 많이 사용됨
- +) 공장, 발전소의 효율성을 증가시킬 수 있음
- +) transportation의 효율 증가시킬 수 있음

**💡 AI의 학습에 많은 전력(CO2 Emission cost)가 들어가지만, AI를 활용하여 여러가지를 효율적으로 사용하여 이런 전체적인 cost를 줄이기 위한 노력들이 지속되고 있다**

<br><br><br>

**📌reference**
- boostcourse AI tech
- [나무위키-COMPAS](https://namu.wiki/w/COMPAS)
- [privacy](https://arxiv.org/pdf/2003.11511.pdf)
- [AI-now](https://ainowinstitute.org/AI_Now_2016_Report.pdf)

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

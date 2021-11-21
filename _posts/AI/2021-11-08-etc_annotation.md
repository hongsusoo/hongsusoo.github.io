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

title: "Annotation Guide 만들기"
excerpt: "about : segmentation"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - AI ETC
tags:
  - [annotation]
date: 2021-11-08
last_modified_at: 2021-11-08
---

<br>

# Annotation Guide 

- 좋은 데이터를 확보하기 위한 과정을 정리해 놓은 문서
- 좋은 데이터란?
    1. 골고루 모여있고 → imbalance하지 않도록 주의(특이한 Case를 발견하여 샘플을 확보하기 위한 노력 필요)
    2. 일정하게 라벨링된 데이터 → 노이즈 최소화(1번을 포함하는 라벨링 가이드를 통하여 노이즈 최소)
    
    
## 데이터셋 제작 파이프라인

- Dataset의 경우 결국 서비스 요구사항를 기준으로 제작됨
    - ex) 영수증 인식에 사용할 OCR 엔진 개발
        1. 종류 : 모든 영수증, 이마트, 식당 등등
        2. 인식 글씩 : 전체 글씨, 가격, 메뉴 등등
        3. 글씨 인식 정도 : 물에 젖은 영수증 글씨, 모든 언어, 거울에 비친 글자 등등
        4. 모델 구조 선정 : 검출기 + 인식기 구분 or 같이, input information format
        5. Raw Image 수집 : 크롤링, 크라우드 소싱
        
![image](https://user-images.githubusercontent.com/77658029/140727597-9e5801b0-b0b3-4097-9f86-7b9b774c05ae.png)


### Raw Image 수집 방법
  
- 크롤링
    1. 검색어 입력
        - 결과에 중요한 영향을 미침, 검색어의 집합으로 글자가 등장하는 상황을 크롤링 진행
    2. 조건설정
        - image 사이즈 설정 : 용량이 된다면 이미지는 클수록 좋음
        - 상업적 사용 가능한 Image로 추리기(google에 사용권 선택)
![image](https://user-images.githubusercontent.com/77658029/140731832-701415c5-3b40-4824-9fd6-3434f065dd42.png)
![image](https://user-images.githubusercontent.com/77658029/140739235-c1dbdbc8-233a-4ffd-9f1a-436351205efd.png)

- 크라우드 소싱
    - 수집용 가이드라인 제공하여 사람이 data를 제작함
    - 시간, 비용이 많이 들어 일반적으로 크롤링된 이미지에 추가하는 방식으로 진행
    - Edge case 수집에 유리(구하기 힘든 이미지)
        - 원하는 특성 명시
        - 좋은 예, 나쁜 예를 직접 사람에게 학습시킬 수 있음
    - 개인정보, 저작권 이슈에서 자유로움


### 가이드라인 제작 과정

![image](https://user-images.githubusercontent.com/77658029/140741023-c8bbdc92-4514-4338-ad2b-bef934deec59.png)

- 초기 라벨링/라벨링 검수 시 정말 많은 QnA가 발생하기 때문에 소량의 데이터로 우선 Pilot 라벨링 작업을 진행하여 가이드라인 완성도를 빠르게 높여두는 게 중요함
- AI팀에서 데이터 검수를 하게 될 경우 Model 변경에 따른 라벨링 방식 변경 or 데이터 추가 수집 등의 요청이 이뤄짐(데이터 분포 및 라벨링 노이즈 관점에서 데이터를 보게됨)
- 라벨링 방식에서 여러번의 탐색과정(feedback)이 많거나, 작업자에게 익숙하지 않은 데이터의 경우 가이드의 작성/수정/교육에 대한 비용이 커지기 때문에 외주보단 내부 인력으로 진행하는 것이 효율적일 수 있음




## Annotation Guide에 필요한 내용


### 명확한 학습 목적 정의

- 글자 영역을 찾아보자 하였을때 아래와 같이 여러 방법으로 찾을 수 있음
- 구축 목적에 맞게 annotation 될 수 있도록 정의가 필요함

![image](https://user-images.githubusercontent.com/77658029/140694490-17a72906-6628-4661-a2a4-14a3cc024e2a.png)


### 3가지 중요 요소

- 특이케이스
    - 글씨형태의 다양성, 특수문자와 같은 글씨 등 여러 케이스 포함
    ![image](https://user-images.githubusercontent.com/77658029/140725337-4187c98a-b9a1-46ee-95e0-d3868ddfabea.png)
- 단순함
    - 모든 케이스를 다 넣는다고 좋은게 아님
    - 작업자들이 다 숙지하기 어렵게 되면 결국 Noise가 발생하게 됨
- 명확함
    - 일관성 있는 데이터를 만들기 위하여 명확한 작업 Guide 필요함
    ![image](https://user-images.githubusercontent.com/77658029/140727312-8e25c3ee-1d04-413b-87e7-e139d3eda011.png)
    


### 기본적인 용어

- 기본적인 용어 정의(bbox, 전사, 태그)
- 일관성 있는 Annotation 규칙
    - 작업불가 이미지 정의 
    - 작업불가 영역 정의
    - bbox 작업 방식 정의

![image](https://user-images.githubusercontent.com/77658029/140693537-09208061-fafd-4c2f-a3e7-c40c98870adb.png)

1. Hold 이미지
    - 이지내 글자 영역이 존재하지 않는 이미지, 글자를 알아보기 어렵거나, 같은 글자 혹은 패턴이 5회이상 반복되는 이미지, 영어, 한국어가 아닌 외국어가 1/3인 이미지, 개인정보가 포함된 이미지, 촬영한 이미지가 아닌 디지털 형태의 이미지(born-digital)
2. Annotation 규칙 : 
    - BBOX 제작시 최소한 해당 글자를 포함하되, 느슨한 박스는 지양
    - 단어가 심하게 꺾여 있는 모양일 경우 짝수개의 점들로 이뤄진 Polygon 형태로 지정(최대 12개)
    - 좌표 시작점은 첫글자의 좌상단으로 진행
    - 어디까지를 하나의 글자 영역으로할지 정하기
3. 작업 불가 영역 : 
    - 글자를 알아보기 어려울 정도로 밀집되어 있을떄
    - 글자가 겹쳐 확인이 어려울떄(illegibility : True) -> tight하게 할 필요 없음
    - 글자와 유사한 모양의 물체는 표기하지 않음
4. 작업 대상 영역
    ![image](https://user-images.githubusercontent.com/77658029/140757906-6269f1a0-a8af-430d-989a-e334b56544dd.png)

### 일관성

- 가장 중요한건 일관성 있는 Guide

1. 띄어쓰기 : 의미보단 공백의 크기로된 기준으로 진행
    - 만약 의미로 한다고 하면, 고유명사(등촌 칼국수 vs 등촌칼국수)에 의한 차이가 발생할 수 있음
2. 손글씨 : 동일한 글자를 다르게 쓰는 경우를 손글씨로



## 검수

###  Labeling 검수

1. 감독자 전수 검사
    - 한 감독자가 할당된 작업자의 결과물을 모두 시각화하여 문제가 없는지 확인 후 다른 작업자에게 전달
2. Peer Check 
    - 끝난 작업 물을 다른 작업자에게 할당하여 틀린 부분을 찾아서 고침
3. 다수결
    - 여러 사람이 동일한 작업을 진행하고 그 결과를 프로그래밍 적으로 합침


### 가이드라인 검수

- 초기에 소량씩 완성본 받아서 품질을 확인
- 작업자 QnA 활용 : 가이드라인 수정할 부분이나 추가할 부분을 결정하여 재배포
- 추가 수정을 위한 비용과 시간이 크면 어느 정도 포기함

**📌reference**
- boostcourse AI tech


<br><br>

**📌reference**
- boostcourse AI tech

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

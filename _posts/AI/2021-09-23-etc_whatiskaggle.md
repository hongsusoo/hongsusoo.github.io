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

title: "Kaggle platform 소개"
excerpt: "about : data science competition"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - DL etc
tags:
  - [kaggle]
date: 2021-09-23
last_modified_at: 2021-09-23
---

<br>

# kaggle 

- 2010년 설립된 세계에서 가장 유명한 인공지능 대회 플랫폼
- 2017년 google에 인수됨

🎈 국내 유명 경진대회 플랫폼

![image](https://user-images.githubusercontent.com/77658029/134461513-12a431b6-245f-4d6e-8128-94e357ce8c36.png)

<br><br><br>

## 캐글을 왜 할까?

- 취업 목적 : 세계적으로 실력을 인정받기 위해서 

    + 유명 해외 업체에서 컨텍, 대학교 박사과적 제의

- 개인 성장 : AI 개발자로배우고 성장하기 위해서

    + 특유 공유문화로 배우기 좋은 수 많은 코드, 토론 자료들이 많음
    + 캐글 노트북은 버튼 몇 번 조작으로 빅데이터를 읽어서 학습, 훈련 가능함
    
<br><br><br>   

## 캐글에서 실력 인정 받기

- 랭킹 시스템 : 경진대회에서 높은 순위에 들어 포인트를 획득, 누적된 포인트로 순위가 정해짐

- 티어 시스템 : 경진대회에서 메달을 따게 되면 개수에 따라서 티어가 결정됨, 총 4개 종목이 있고, 가장 어려운 티어는 컴피티션 그랜드 마스터!

<br><br><br>

## 대회 목적

<br>

### Featured

- 상업적 목적의 예측 대회
- 실제 기업에서 우승한 모델을 현업에 적용하기도 함

<br><br>

### Research

- 연구 목적의 대회 연구 목적이라 상금이 낮은편

<br><br>

### Getting Started & Playground 

- 초심자를 위한 학습 목적의 대회
- 예시) 타이타닉 생존자 예측 대회
- 랭킹용 포인트나 메달을 얻을 수 없음

<br><br>

### Analytics

- 데이터 분석 목적의 대회
- 데이터 탐색과 이를 시각화한 노트북을 제출하는 대회

<br><br>

### Recruitment

- 리크루팅 목적의 대회

<br><br><br>

## 제출 방법

<br><br>

### General Competition

- 리소스 제약 없음
- Submission.csv 파일만 Submit predictions 메뉴에서 제출

<br><br>

### Code Competition

- 캐글 노트북에서 코드를 실행시켜 submission.csv 파일을 생성
- code 동작시 리소스(GPU, CPU, RAM, 실행시간) 제약이 있음
- 쓸모있는 모델을 만들 수 있도록 강제함

<br><br><br>

## 시작하기

1. 회원가입
2. 참여할 대회 선택
3. 데이터 다운로드
4. 대회를 위한 파이프라인 구축
5. 캐글로 파이프라인을 빠르게 경험해 보기

<br><br><br>

## 캐글 노하우

<br>

### 1. 파이프라인의 빠르고 효율적인 반복

- GPU장비 : 학습속도가 빠를 수록 파이프라인 반복속도가 빨라져, 캐글에서 상위권에 들기 위한 많은 시도를 할 수 있음

![image](https://user-images.githubusercontent.com/77658029/134466398-220dc483-4392-47f3-839f-35335ddfba5f.png)

- 시간투자


- 본인만의 기본 코드_[example code](https://github.com/lime-robot/categories-prediction)

    + 본인만의 기본 코드를 만들어 어떤 데이터를 다룰때 일부만 수정/사용하여 빠르게 파이프라인을 구축하고, 실수를 줄일 수 있음 

<br><br><br>

### 2. 점수 개선 아이디어

- 캐글 notebooks 탭 참고
    + 다양한 아이디어를 얻을 수 있음
    + 어떤 딥러닝 아키텍처를 사용하면 좋을지, 이미지 Augmentation은 어떻게 하면 좋을지 등
    
- discussion 
    + 비슷하거나 동일한 이전 대회, 참고할 논문, 현재 대회 Overview 등등을 확인 할 수 있음
    + 다른 경쟁자들의 글을 참고하여 마지막까지 아이디어 고민
    
<br><br><br>
    
### 3. 탄탄한 검증 전략

- Shake-up 현상 : Public LB -> Private LB넘어가며 순위가 뒤바뀌는 현상
- 리더보드의 제출 횟수 제한
- 위 두 가지로 인해 검증 방법에 대한 구축이 필요함
- 좋은 모델 : Training set과 test set이 비슷하게 나오는 모델
- Local CV(cross validation)와 Public LB를 모두 올리는 방법으로 구축

**💡 검증전략이란?**

![image](https://user-images.githubusercontent.com/77658029/134467057-7fbecb09-59c5-4a51-a934-86b61f6a1a00.png)

Test set에서 얻은 점수와 Training set에서 얻은 점수의 gap를 줄이는 평가 방법을 구축하는 것!

🔎 Kaggle Data 구성

![image](https://user-images.githubusercontent.com/77658029/134467297-3c58f10e-85d2-4695-aa0e-81475f851624.png)


**🎈 검증전략 구축하기(training set 나누기)**

![image](https://user-images.githubusercontent.com/77658029/134467950-a93fe461-9db5-47bd-82bb-7ad72d783c14.png)

![image](https://user-images.githubusercontent.com/77658029/134468038-a6e596ae-3805-4ce5-8463-48ac0a9bbbe5.png)


<br><br><br>

### 4. Ensemble

- single model로 최대한 성능을 높이고, 1~2주 정도 남았을때 ensemble 시작함
- 싱글 모델 보다 대부분 좋은 성능을 얻을 수 있음

![image](https://user-images.githubusercontent.com/77658029/134469082-69e7117a-f75c-4918-945a-88cdf7bcf619.png)

<br><br><br>

**📌reference**
- boostcourse AI tech


<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

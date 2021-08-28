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

title: "[CV Project] 마스크 착용 상태 분류 - EDA🌓"
excerpt: "about : Image Classification Competition"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - AI_project
tags:
  - [CV, Modeling, Pstage-01]
date: 2021-08-24
last_modified_at: 2021-08-24
---

<br>  

# EDA(Exploratory Data Analysis)

- 탐색적 데이터 분석으로 데이터를 이해하기 위한 노력을 의미함
- Task의 목적을 이루기 위해 필요하거나 궁금한 부분을 채워가는 부분

<br>

## Dataset description

- 20~70대의 아시아인 남녀로 구성
- 전체 사람 수 : 4,500
- 한 사람당 사진 수 : 7장(마스크 착용 5, 이상하게 착용 1, 미착용 1)
- image size : 384,512
- data 구분 : train set(60%, 2700), public test set(20%, 900), private test set(20%, 900)

<br>

## Target

- 총 18개 class로 구분
- Mask 착용(정상, 비정상, 미착용), 성별(남, 여), 나이(~30,30~60,60~)

![image](https://user-images.githubusercontent.com/77658029/131209538-f09809d2-d521-4848-b481-14d1938192c7.png)

<br>

## Data 위치 및 구성 확인

- train.csv : id, gender, race, age, path에 대한 정보 -> model 학습용 data
- info.csv : id, ans -> Public test용 data, 
- images folder : 학습용 Data, test용 Data image가 들어가 있음
- train data image의 file 명에 Mask 상태에 대한 정보가 들어있음

```
+-- train/
|   +-- images/
|       +-- 000001_female_Asian_45/
|           +-- mask1.jpg
|           +-- incorrect_mask.jpg
|           +-- normal.jpg
|       +-- 000002_female_Asian_52/
|       +-- …
|   +-- train.csv
+-- eval/
    +-- images/
        +-- 814bff668ae5b9c595ceabcbb6e1ea84634afbd6.jpg
        +-- 819f47db0617b3ea9725ef1f6f58e56561e7cb4b.jpg
        +-- …
    +-- info.csv
```

<br>

## DataFrame 만들기

- 주어진 Train data

![image](https://user-images.githubusercontent.com/77658029/131210186-4a4c58f4-55b8-4f97-b8be-540fe6b53959.png)

- 수정 후 Train data

![image](https://user-images.githubusercontent.com/77658029/131210203-94087b08-edeb-44e7-8aab-f86d0a17b2b3.png)

<br>

## Data Analysis

- 성별, 나이, Mask 착용 상태에 따른 분포

![image](https://user-images.githubusercontent.com/77658029/131209735-59d62789-25e6-4424-81f2-d634176b3aec.png)

- Class 별 분포

![image](https://user-images.githubusercontent.com/77658029/131209713-931dcd8e-a382-4b51-befc-6225c61c374c.png)


<br>

### 💡 내용 분석

1. 나이와 Mask 착용 상태에 대한 Data 분포의 불균형이 큼
2. 1번에 의해서 Target class에 대한 분포의 불균형이 큼

**📌 Data augmentation이나 dataset을 추가하여 불균형에 대한 문제 해결이 필요할 것 같음**


<br>

**📌reference**
- boostcourse AI tech


<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

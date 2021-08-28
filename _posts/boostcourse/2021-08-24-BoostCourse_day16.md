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

title: "[boostcourse] Day16 학습기록_minibatch28"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - daily
tags:
  - []
date: 2021-08-24
last_modified_at: 2021-08-24
---
<br>

## 학습 내용

<a href="https://hongsusoo.github.io/ai/proj_ImageClassify01"><img src="https://img.shields.io/badge/-EDA-red"/></a> 

<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 강재현

참가자 : 강재현, 권예환, 김준태, 박마루찬, 서광채, 장동건, 홍요한

<br>

### EDA 공유

- 동건님 발표
    - 3개를 각자 분류
    - One-hot Encoding

<br>

### 코드 작업 공유

- 광채님
    - EDA
        - 8번, 14번 클래스 데이터 부족(심각)
    - ViT 시도중
    - 처음에는 nfnet 시도
- 예환님
    - resnet18 사용
- 요한님
    - 데이터프레임 변환에 어려움을 겪었었음
    - 60대 이상 데이터가 적고, 클래스 불균형이 아주 심함
- 마루찬님
    - validation acc가 test acc 대비 20% 이상 낮은 원인 찾는 중

<br>

## 회고록

주어진 data에 대한 EDA분석을 진행했다. 그래프 하나 그리는데도 꽤 많은 시간이 소모됐다.

시각화 관련 강의들이 계속 밀리고 있는데 시간을 내서 쭉 보고 연습해봐야겠다. 

기본이 많이 부족한 것 같다. Model 구현과 함께 기본에 충실하게 연습해 나아가야 할 것 같다.


<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

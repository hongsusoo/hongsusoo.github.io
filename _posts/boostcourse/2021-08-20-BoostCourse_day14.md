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

title: "[boostcourse] Day14 학습기록_minibatch28"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - daily
tags:
  - []
date: 2021-08-20
last_modified_at: 2021-08-20
---
<br>

## 학습 내용


<a href="https://hongsusoo.github.io/ai_library/lib_hyperparameter_tuning"><img src="https://img.shields.io/badge/-hyperparameter tuning-red"/></a> <a href="https://hongsusoo.github.io/ai_dlbasic/dl_multi_GPUbasic"><img src="https://img.shields.io/badge/-Multi GPU-red"/></a> 

<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 장동건

참가자 : 강재현, 권예환, 김준태, 박마루찬, 서광채, 장동건, 홍요한


<br>

### GoogLeNet 모델 리뷰

- GoogLeNet (서광채님, 홍요환님, 장동건님)

<br>

### 3주차 팀 회고

- 잘했던 점/좋았던 점/계속할 점
    - TODO list 매일 작성한 점 → 자극이 됐음
    - 일상 공유
    - Model 정리(AlexNet, ResNet, GoogLeNet)
    - 개인 작업을 공유(재현님 AlexNet 코드 리뷰,마루찬님 고양이 testing)
    - 협업 방법 토의

<br>

- 잘못했던것, 아쉬운것, 부족한것 → 개선방향
    - 풀리지 않은 특정 문제에 집착
    - 시각화 강의를 잘 못 듣고 있음
    - 강의에 대한 질문거리가 부족했음
    - 다음 주차에 대한 일정 정보 부족 (수업 피드백)

<br>

- 도전할 것, 시도할 것
    - 다양한 방법론 탐색
    - 프로젝트 준비 위해 피어세션 일정 조정 - slack 통해 월요일에 나눠봅시다
    - 개인 작업들 공유
    - 코드 리뷰

<br>

- 키워드(공부한 것, 알게된 것, 느낀 점)
    - PyTorch
    - Computational Graph (Tensorflow vs PyTorch)
    - wandb (Weights and Biases)
    - hook
    - Customizing
    - Documents

<br>

### 멘토링

- Q

      이미지 분류 대회 협업을 어떻게 할 수 있을까?(각자 모델을 개발하는 방법, 하나의 모델을 여럿이 개발하는 방법 무엇이 좋을까요?)

  A 

      1. 모델 서치(base line 모델 2~3)
      2. 그 조합을 나눠서 진행
      3. 괜찮은 모델들은 다른 팀들도 같이 사용함
          a. augmentation
          b. parameter search
          c. 앙상블
      4. Ray, wandb 를 숙지해서 연습해놓기!

- Q

      MLOps 지금 공부하는게 좋을까요?

  A - [참고자료](https://m.facebook.com/groups/748639598856641?view=permalink&id=1374396392947622)

      현재 교육받는 내용에 집중하고 이후에 MLOps는 따로 공부하는 걸 추천

- Q

      ADP 등 자격증이 도움이 될까요?

  A 

      조금은 도움되겠지만, 크게 도움되진 않음, AWS Solution architecture를 공부 추천, 유명한 대회 수상경력이 더 나음

- Q

      interpreter, compiler 관련 읽고 계신 책은 어떤걸 공부하시는 건가요?

  A 

      지금 당장은 필요없지만 조금 더 Low level에서 원리를 공부하기 위해 읽고 있음


    
<br>

## 회고록

이미 많이 배운 멘토님도 끊임없이 공부하는 것을 보고, 스스로 반성도 하고 생각도 많아진 하루였다. 교육이 끝나고 앞으로 어떻게 내 미래를 그려나가야 할지 깊은 고민이 필요할 것 같다. 내 정확한 위치도 모르고, 어떻게 방향을 설정해야할까 고민하다. SGD가 생각났다. 결과가 어떻게 될지는 모르지만, 일단 현재 최선의 방향을 선택해서 시도하고 다시 고민하는 걸 반복해야할것 같다.

그래도 주말이 가까워 오니 멘탈은 조금 회복된것 같다. 우선 주말 동안에 밀린 공부를 좀 하고 진도를 따라잡아야겠다.


<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

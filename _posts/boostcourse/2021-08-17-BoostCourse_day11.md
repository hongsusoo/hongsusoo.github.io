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

title: "[boostcourse] Day11 학습기록_minibatch28"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - daily
tags:
  - []
date: 2021-08-17
last_modified_at: 2021-08-17
---
<br>

## 학습 내용

<a href="https://hongsusoo.github.io/ai/pytorch_intro"><img src="https://img.shields.io/badge/-pytorch 소개-red"/></a> 
<a href="https://hongsusoo.github.io/ai/pytorch_basicgram"><img src="https://img.shields.io/badge/-pytorch 기초 문법-red"/></a> 
<a href="https://hongsusoo.github.io/ai/projectstructure"><img src="https://img.shields.io/badge/-project structure-red"/></a> 

<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 김준태

참가자 : 강재현, 권예환, 김준태, 박마루찬, 서광채, 장동건, 홍요한

<br>

### 질문사항

- Q

      colab에서 쉘 명령어를 쓸 때 다른 건 !를 앞에 붙여 사용하는데 왜 cd만 %cd로 사용할까?

  A

      - ! 명령어는 임시 subshell에서 실행되는 방식
      - os.chdir()도 사용 가능

- Q

      view와 reshape의 차이

  A

      - reshape는 contiguous를 강제로 맞춰줌
      - view는 안지키면 error
      - 사용할때 Contiguous의 중요도에 맞춰서 사용이 필요함


<br>

### 건의사항

- 피어세션 시간 변경 : 16시~17시 30분
- ResNet, GoogLeNet 발표는 여러번 하지 않고, 조별로 내용 정리해서 발표하기

<br>

## 회고록

뭔가 하루종일 뽁작뽁작 공부를 하는 것 같은데, 시간도 부족한것 같고 공부가 되고 있는건지 잘 와닿지가 않는다. 이렇게 가면 쉽게 지칠것 같은데, 새로운 공부 방법을 찾아봐야겠다. 

시간을 효율적으로 사용할 수 있도록 시간표를 세워서 모르는 것에 너무 많은 시간을 쏟지 않고 어느 정도 조율 가능하게 공부를 해야겠다

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

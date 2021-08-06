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

title: "[boostcourse] Day4 학습기록_minibatch28"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - daily
tags:
  - []
date: 2021-08-05
last_modified_at: 2021-08-05
---
<br>

## 학습 내용

<a href="https://hongsusoo.github.io/AI/RNN_basic"><img src="https://img.shields.io/badge/-Day01-red"/></a>




## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 강재현
참가자 : 강재현, 권예환, 김준태, 박마루찬, 서광채, 장동건, 홍요한


### 과제 리뷰

- 과제 4. Baseball
    → 박마루찬님 발표 후 피드백
- 과제 5. Morse code
    → 서광채님 발표 후 피드백
- 과제 3. Text_Processing2
    → 김준태님 발표 후 피드백


### 질문내용

- 권예환님 질문
    역전파의 자세한 계산과정이 궁금합니다!
    → 블로그 구글링

- 강재현님 질문

    $$E_{y \sim P(y|x)}[y|x] = \int_y yP(y|x)dy$$

    조건부기댓값은 $E||y-f(x)||_2$ 을 최소화하는 함수 $f(x)$와 일치한다
    수식이 이해가 안됩니다😇

    → 홍요한님과 박마루찬님이 부가설명 제공

- 홍요한님 질문

    numpy는 연속된 메모리 주소를 가져간다고 했는데, 돌려보니까 list가 더 연속된 메모리를 가져가는 것 같은데 제가 잘못 이해하고 있는 걸까요?

    → 서로 화면공유, 구글링하며 리서치

- 서광채님 질문

    mock patch 동작 방식을 모르겠습니다
    → documentation 참고, 다른 디버깅 방법 제시


## 회고록

오늘은 활성함수와 딥러닝 부분에 대해서 공부를 하고, 필수과제를 연달아 3개를 끝냈다. 과제를 하다보니, 정작 강의에 집중을 못했는데, 다른 캠퍼분들도 느꼈는지 과제가 나온 다음날 푸는걸로 그라운드룰 수정했다. 

오늘은 간단하게 numpy의 메모리에 대해서 질문을 했는데, 다들 너무 적극적으로 대답해줘서, 좋은 답을 얻을 수 있었다. 

설명을 잘 못했는데 유능한 팀원들이 찰떡같이 알아들었는데, 설명하는 방식에 대해서도 조금 노력이 필요할 것 같다. 내 생각을 일목요연하게 표현하는 연습을 하기 위해 매일 글로 조금씩 남겨봐야겠다. 


<br>
```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```
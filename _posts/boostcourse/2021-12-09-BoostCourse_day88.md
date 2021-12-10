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

title: "[boostcourse] Day88 학습기록_팀명뭘로하조"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - daily
tags:
  - []
date: 2021-12-09
last_modified_at: 2021-12-09
---

## 학습 내용

- Product serving 기초(<a href="https://hongsusoo.github.io/ai%20etc/etc_mlserving"><img src="https://img.shields.io/badge/-Product Serving-red"/></a>)

<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

- metric 논의
  - 춤선 == 이동량에 대한 체크? → optical flow 를 이용하기? 도 한 방법이 될수도
  - [Human Pose Estimation 기초 이론 정리 및 설명 (tistory.com)](https://ctkim.tistory.com/101)
  - normalize는 어떻게 할지?
      - 카메라 위치에 따른 비율 달라지는건 affine transformation 이용해서 교정하면 되지 않을까

## 최종프로젝트 피드백

- 완벽을 요구하는 것이 아닌 이런 것도 감안했네? 이런 것도 생각할수 있구나?
- AI 개발자로써 생각하는 사고 마인드가 자료에 드러나면 좋을 것 같다.
- 진행하는 Task가 AI로 풀수 있는 문제인지, 시간은 어느 정도 걸리고, Resource는 어느 정도 들어갈지 그런 전반적인 감이 있으면 좋을 것 같다.
- generation 모델의 경우 도덕적으로든 저작권으로든 민감한 부분들이 나오지 않는지 고려해봐야함
- 제약사항 내에서 모델 요구사항등 제한을 미리 언급해 두는것도 좋음
- 전체적인 flow가 그려지면 좋음 → 입력 출력에 대한 flow, 비디오가 입력으로 되서 어떻게 처리되서 이미지로 출력
- 비디오의 시작점에 대한 정리가 필요할 것 

Q. 모델 서빙이라는 주제로 알고 있는데, 서비스는 어느정도 구현을 목표로 해야하는지, 간단하게 서비스를 구현하고 모델에 치중해도 되는지 궁금합니다.
    
이활석 CTO : 모델 서빙도 중요하지만, 이번엔 모델도 중요한것 같다. 모델에 대해서 얼마나 잘고민하고 했는지가 궁금할 것 같음, 개인의견임... 후후 중점은 모델에 둬야한다..
    
Q. AI 개발자로서 고민한 부분을 어필하는 것이 좋다고 말씀해 주셨는데, 잘 안된 부분은 어떤 식으로 어필하면 좋을까요?

이활석 CTO : 안되서 끝이라고 하면 의미 없고, 안되는걸 왜 안됐는지 고민해보는건 중요한 것 같음, 왜 안된느지 분석이 필요하다고 생각함, 나름 분석한걸 얘기하면 좋을 것 같음 개선책으로 이렇게 해봤는데 안됐음. 시도 → 분석 → 개선,시도 → 분석 → ~~
    
Q. 저희가 딥러닝을 공부하고 실사례에 적용해보려니 변수들이 많았습니다. (라이브 커머스에 댓글 수가 적다거나, 욕설이 없다거나..) 그러면 혹시 기술적인 부분을 어필하기 위해선, 실사례보단 저희가 기술을 어필할 수 있는 일정 조건을 정하고 진행해도 될까요?

이활석 CTO : 네! 실사례 변수들은 AI 더 많이 해보신 분들이 해결해줄것..ㅋㅋ 이런 변수들을 아는 것 만으로도 좋은 것 같음 그래서 기술을 어필하는게 중요함.

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

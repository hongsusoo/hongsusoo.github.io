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

title: "[boostcourse] Day36 학습기록_팀명뭘로하조"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - boostcourse
tags:
  - []
date: 2021-09-24
last_modified_at: 2021-09-24
---

## 학습 내용

- 특강 : <a href="https://hongsusoo.github.io/dl_etc/etc_AI_ethics"><img src="https://img.shields.io/badge/-AI ethics-red"/></a>

<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 박준혁

참가자 : 박범수, 박준혁, 서희수, 한건우, 홍요한, 황원상, 조혜원

<br>

### 토의 내용

**Q. AutoEncoder중 모래시계모양이 아닌 마름모 모양의 net을 쓰는경우는?**

A. CNN기반 모형으로 마름모 모양이지만 채널이 늘어난거고 중간에 풀링이 들어가 결과적으로는 축소 된 것.

[마름모 모양 AutoEncoder의 예](https://dacon.io/en/codeshare/2965)

**GRAM Matrix**

![image](https://user-images.githubusercontent.com/77658029/135783364-48a26428-75fa-4acb-bb5f-a9a8e6fd071b.png)

- 논문에서는 각각의 Feature Map의 Channel을 각각 Flatten 하여 새로 만들어질 이미지와 correlation을 같게 만들어준다. 이 Channel의 Correlation을 표현한 매트릭스를 Gram Matrix라고 한다. 이 Gram Matrix와 새로 만들어질 이미지의 Gram Matrix와의 차이를 Loss Function으로 정의하여 Loss를 Minimize 해주게 된다


```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

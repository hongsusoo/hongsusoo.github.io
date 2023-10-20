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

title: "[boostcourse] Day43 학습기록_팀명뭘로하조"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - boostcourse
tags:
  - []
date: 2021-10-06
last_modified_at: 2021-10-06
---

## 학습 내용

- Ready for Competition
- Cutmix 진행
  - Battery와 같이 Data 숫자가 부족한 Class가 있어, 이 부분을 보완하기 위해서 Cutmix를활용하여 Data 숫자를 보완(cutmix시 bbox간섭이 안되도로고 비어있는 공간에 cutmix를 진행하여 annotation 추가해줌)

  ![image](https://user-images.githubusercontent.com/77658029/137634994-39ec2f51-3ab1-4f8e-b822-1760eb91c4e9.png)

  -> LB 상에 큰 변화는 없음
  분석 : Battery를 포함하여 상대적으로 Data 수가 적은 Class의 경우 이미지의 특징이 명확하여 구분에 어려움이 없었음

  ![image](https://user-images.githubusercontent.com/77658029/137635361-e0e3cfa1-d478-4596-a1e9-62cdf600775b.png)
 
<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 한건우

참가자 : 박범수, 박준혁, 서희수, 한건우, 홍요한, 황원상, 조혜원

<br>

### 토의 내용

- Model 후보군 돌려보기
  - Universe101
  - Swim-S
  - Swim-T
  - vfnet
  - vfnetx
  - DetectoRS

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

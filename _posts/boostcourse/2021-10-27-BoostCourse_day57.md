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

title: "[boostcourse] Day57 학습기록_팀명뭘로하조"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - daily
tags:
  - []
date: 2021-10-27
last_modified_at: 2021-10-27
---

## 학습 내용

- WSSS(<a href="https://hongsusoo.github.io/ai_dlbasic/dl_wsss"><img src="https://img.shields.io/badge/-WSSS-red"/></a>)
- WSSS(<a href="https://hongsusoo.github.io/ai_models/md_hrnet"><img src="https://img.shields.io/badge/-HR Net-red"/></a>)
- Cutmix Test 진행

![image](https://user-images.githubusercontent.com/77658029/139884540-3981c9e8-4706-4896-b093-2bdac511be8c.png)

- Data imbalance에 비중을 두어 metal, glass, battery, clothing에 cutmix를 적용하였을 경우 battery에만 큰 효과가 있었음, battery의 경우 다른 class와 따로 떨어져 있는 경우가 많았고 metal, glass, clothing의 경우 다른 class와 겹쳐진 경우가 많아 이런 결과가 나온것으로 사료됨


<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 한건우

참가자 : 박범수, 박준혁, 서희수, 한건우, 홍요한, 황원상, 조혜원

<br>

### 대회 진행

- augmentation test 진행중
    - rotate 가 그나마 효과가 있었음
- kfold 앙상블 시도해보기
- PyTorch lightning으로 baseline 짜기

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

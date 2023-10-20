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

title: "[boostcourse] Day78 학습기록_팀명뭘로하조"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - boostcourse
tags:
  - []
date: 2021-11-25
last_modified_at: 2021-11-25
---

## 학습 내용

- Baseline 분석 및 optuna 적용 방법 고민

<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

최종프로젝트 논의

- 영상 segmentation/detection + LiDAR([https://aihub.or.kr/aidata/34162](https://aihub.or.kr/aidata/34162)) - 요한, 준혁, 혜원
    ⇒ 시연할 때 스토리 필요
    ⇒ 3D data 너무 클것같다 → 전처리만 오래 걸릴수있다, 학습자체도 오래 걸릴 것 같음.. 현실적으로 어려울 것 같다.
    ⇒ 밤 시간대 등 특정 환경을 정해서 해보는건 어떨까? → 목적을 좀 더 구체적으로 정해보자
    
- adaptive NMS 구현해서 재활용 쓰레기 detection에 적용해보고 싶어요. - 원상
내용이 작아서 혼자 따로 하고 싶습니다. (찐따, 아싸 기질)
[https://arxiv.org/abs/1904.03629](https://arxiv.org/abs/1904.03629)
    ⇒ 다른 NMS 방법들과 비교, 다른 데이터 셋에 대해서도 실험, 다양한 실험 하면 좋을 듯(SOTA에 넣어보기)
    
- 춤 영상 pose estimation - 범수, 준혁, 혜원, 요한 rank 2
    ⇒ 기준을 수치화하는 방식을 고민해봐야함, 같은 춤을 춘다고 해도 느낌이 다르고, 춤선이 다르기 때문에
    ⇒ 영상이다니까 데이터 전처리가 쉽지 않음.. → 장르/그룹 등 대상을 특정하는 것이 중요할 것

- image inpainting - 준혁, 혜원, 요한, 건우, 멘토님

- img2img translation - 건우님

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

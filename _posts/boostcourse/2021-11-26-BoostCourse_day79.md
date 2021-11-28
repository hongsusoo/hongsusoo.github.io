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

title: "[boostcourse] Day79 학습기록_팀명뭘로하조"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - daily
tags:
  - []
date: 2021-11-26
last_modified_at: 2021-11-26
---

## 학습 내용

- Baseline 분석 및 optuna 적용
- 데이터톤 수상식 다녀오기(National Pathology Health Datathon 2021)_[github link](https://github.com/hongsusoo/NPHD2021_gi_cell)

![image](https://user-images.githubusercontent.com/77658029/143607271-7deb6023-a48a-4e92-b722-3618f8e48034.png)

<br>

## Deview 요약 👨‍👨‍👦‍👦 👨‍👨‍👦

### **Clova AI LAB**

→ 잘은 모르겠는데 우리팀에 석사는 있고 학사는 인턴으로 본거같아요~! (상담은 착하게 잘해줌) → 학사는 안뽑는다는 의미가 아닐까..?

### **알레시오**

 → GAN 세미나 해주셨음. 부캠 1기때도 참여기업함! Semantic manipulation
 
- 제일 잘 알려진 생성 모델인 GAN에 대해서 설명함
    - 지표/metric 적 문제 해결
        - Wasserstein distance
            - 두 분포 사이의 변화를 최소한으로 할 수 있는 거리 ← Wasserstein distance 를 loss로 줘서 기존 JSD의 discrete한 특성을 극복함
        - Gradient Penalty
            - discriminator gradient^2을 loss에 추가해서 discriminator의 gradient가 너무 커지지않도록 억제함
- Instance Discriminator
    - Noise-Contrastive Estimation

### **Cake**

→  영어 학습 앱 (현재 9명 개발자가 전체 다함)
소수정예 알잘딱깔센 OK? (유능유능했으면 좋겠어요←넘모해 ㅠㅠ)

 **QnA**

  1. Q. 보내주신 채용공고 잘 봤습니다. 작성해주신 담당 업무나 우대 사항에 내용이 너무 광범위한거 같아서요. 혹시 주로 다루고 싶은 테스크에 대해서 설명을 부탁드려도 될까요? (NLP나 추천시스템 등등..) 
    
    A. 아직 전담 팀이 없어서 데이터만 쌓여있다. 그래서 팀을 꾸린다면 이 데이터로 무엇을 해야할지 방향성도 고려해봐야 할 것 같다.
    
    아까 설명 부족해서 추가 설명한다. ML쪽은 추가적으로 리딩해주는 카이스트 교수님이 계신다. 도움이 많이 될거라 생각한다.
    
  2. Q. 아까 xx님 말씀이 백엔드 하시면서 직접 AI쪽도 하셨다고 언급해 주셨던 것 같아서요... 어떤 분석이나 모델링들이 진행됐는지 문의드려도 괜찮을까요?
    
    A. 음성인식 모델이 이미 있고, 이것을 추가 학습하거나 수정하는 단계를 본인이 하고 있다.리서치 쪽으로 많이 힘을 주고 있고, 실험과 비용이 투입될 예정이다.
    
  3. Q.  전체적인 데이터 플로우에 대해 설명해 주실 수 있으신지 문의드립니다. 백엔드 중심으로 설명해 주시면 감사하겠습니다. 예를 들어 고객별 로그데이터가 어떤 환경의 시스템에 수집되고 어떻게 추출되어 활용되는지 이런 흐름들이 궁금합니다
    
    A. 알룰라 랄랄라 알랄릴라 ( 뭔말인지 모르겠음 ), 서비스 운영 관점으로 데이터를 많이 활용하고 있음.  AI는 이제 시작이라 거의 없따..
    
    초봉은 비밀이에요 친구들~🤭
    

채용 페이지([https://recruit.cakecorp.com/cake/recruitMain](https://recruit.cakecorp.com/cake/recruitMain))

### 마키나락스

  산업 AI 솔루션 회사 → 신입 뽑아욤~!
  코테 → 기술인터뷰(세션이 3개..?) → fit 인터뷰 
  시계열쪽 관심 있음..

  Q. 혹시 MLOps 관해서는 어느정도까지의 이해도를 생각하고 계신지 여쭤봐도 될까요?
  A. 신입도 된다. 모르면 와서 줘패서 가르칠 생각이다.

  Q. 비전쪽으로도 진행한 프로젝트들이 있으실까요?
  A. 아직 비전쪽은 없으나 할 의향은 충분히 있다.

  Q. 채용때에는 지원자가 해왔던 분야에 연연하지 않으신다는 말로 이해해도 될까요?
  A. ㅇㅅㅇ! 와서 맞으면서 배워라.

  Q. 혹시 학력이나 전공에 대한 제한은 없는지 궁금합니다.
  A. 관련 지식이 충분하다면 만사 OK.

  물어볼땐 [jobs@makinarocks.ai](mailto:jobs@makinarocks.ai)


<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

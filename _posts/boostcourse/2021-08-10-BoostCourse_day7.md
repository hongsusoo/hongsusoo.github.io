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

title: "[boostcourse] Day7 학습기록_minibatch28"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - daily
tags:
  - []
date: 2021-08-10
last_modified_at: 2021-08-10
---
<br>

## 학습 내용

<a href="https://hongsusoo.github.io/ai/vector"><img src="https://img.shields.io/badge/-vector-red"/></a>


## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 장동건
참가자 : 강재현, 권예환, 김준태, 박마루찬, 서광채, 장동건, 홍요한

<br>

### 과제 리뷰

- 필수과제 1 : MLP (발표자: 권예환)
    - 강의에서 코드 빈칸을 다 알려주므로 코드가 어떻게 실행되는지를 중점으로 설명
- 선택과제 1: ViT (발표자: 박마루찬, 서광채)
    - 논문: ([https://openreview.net/pdf?id=YicbFdNTTy](https://openreview.net/pdf?id=YicbFdNTTy))
    - 주요 개념: patch embedding, encoder, attention
    - cls 토큰?  → 시작점을 알려주는 신호값
    - 참고 자료 ([https://engineer-mole.tistory.com/133](https://engineer-mole.tistory.com/133))
- 선택과제 2 살펴보기: AAE (발표자: 김준태)
- 선택과제 3 살펴보기: MDN (발표자: 강재현, 권예환)

<br>

### 질문내용

<br>

### 건의사항

- 선택과제 2, 3번은 문제만 한 번 살펴보고 내일 다시 풀이

<br>

## 시각화 특강

안수빈 마스터님의 시각화 특강이 있었다.

시각화는 왜 필요할까?

1. 해석가능, 설명가능한 인공지능을 위해
2. 모델을 비교하고 선택하기 위해
3. 모델을 디버깅하고 성능을 향상시키기 위해
4. 다른 사람들에게 전달하고자 할때 

현재는 Python을 위주로 배우지만 Python이 답은 아니다, 여러 tool들이 있고, 표현하기 위한 방법은 상황에 맞춰 고민이 필요할 것 같다.

마지막으로, 새내기 개발자들에게 개발자의 마음가짐에 대해서 일러주셨다.

개발자는
결국 팀을 이뤄야하고, 코딩 실력이 아무리 좋아도 더 잘하는 사람들은 세상에 많고, 순위와 실력은 유지하기 어렵다.

그러기 때문에 실력은 기본으로 `함께 하고 싶은 개발자`가 되어야 한다.

<br>

## 도메인 특강

이번 Boostcamp과정은 중간에 CV와 NLP중에 하나를 선택하여 P-stage가 진행이 되는데, 신중한 선택을 위해서 이런 특강이 마련되었다. 

멘토님들이 각각 CV, NLP에 대해서 간단한 질문에 대답해 주셨는데, 몇까지만 남겨두려고 한다.

---

👶❓ :  NLP의 경우 언어별로 모델리에 차이가 있을까?

👨‍🎓❕ : 현재는 언아마다 차이가 있는 상황이다. 하지만 점점 언어 dependance가 줄어들고 있다.

👶❓ : CV와 NLP에 대한 선택 이후 각 분야에 대해서 중요하게 생각해야하는 부분은 무엇일까?

👨‍🎓❕ : NLP는 1)Task기반으로 어떤 Application을 만들 수 있을지 고민, 2)언어모델이 어떻게 학습하는지 생각하고, 3)모델에 따른 분야를 기억하자/CV는 1)network가 어떻게 학습되는지 이해하고, 2)다른 데이터에 대해서 공통된 부분을 찾아내는것에서 재미를 느껴보면 좋을것

👶❓ : CV와 NLP별로 참고 할만 한 논문이나, 기억에 남는 논문 추천

👨‍🎓❕ : 

CV - multi modelity,
[on the measurable intelligent](https://www.youtube.com/results?search_query=on+the+measure+of+intelligence)

NLP - [Transformer](https://arxiv.org/abs/1706.03762), [Vanilia-transformer]([https://github.com/KimDaeUng/PLM-Implementation/tree/main/01_Vanilla-Transformer](https://github.com/KimDaeUng/PLM-Implementation/tree/main/01_Vanilla-Transformer)), [Annotated Transformer](http://nlp.seas.harvard.edu/2018/04/03/attention.html)

---

<br>

## 회고

오늘 도메인 특강을 들었지만, 아직 CV와 NLP중에 어떤걸 선택해야할지 모르겠다. 두 가지 모두 가져가고 싶지만, 현재 주어진 내용도 제대로 소화를 못하고 있어서 두 가지 모두를 가져가는 건 욕심인 것같다. 

오늘부터 조금 진지하게 어떤걸 선택할지 고민해 봐야겠다. 

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

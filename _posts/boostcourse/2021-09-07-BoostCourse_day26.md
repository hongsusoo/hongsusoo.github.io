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

title: "[boostcourse] Day26 학습기록"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - boostcourse
tags:
  - []
date: 2021-09-07
last_modified_at: 2021-09-07
---

## 학습 내용

- AlexNet, VGG, GoogleNet, ResNet 강의


<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 한건우

참가자 : 박승찬, 한건우, 배지연, 강재현, 오하은, 홍요한

<br>

### 토의 내용

- nn.functional.softmax와 nn.softmax, nn.functional.log_softmax의 차이
    - log softmax를 사용하면 학습이 잘 안된다
    - nn.softamx는 state가 저장이 된다.
    - functional은 일시적으로 모든 forward와 backward가 끝난 다음에 후처리 용으로 사용한다.
    - 학습이 안되었던 이유는 값이 너무 작아서
    - log softmax는 중첩을 해도 값이 **그대로**이다.
        - log softmax는 출력값이 마이너스이다.

- Ai Stage 서버의 Ram은 90GB
- noisy student: labeling된 데이터의 영향력이 크다. pseudo data가 relabeling이 진행된다
    - labeled image로 teacher model을 학습
    - teacher model을 사용하여 unlabeled image에 대한 pseudo label을 생성
    - pseudo labeled image와 labeled image로 노이즈가 추가된 student model을 학습
    - 참고: [https://deep-learning-study.tistory.com/554](https://deep-learning-study.tistory.com/554)
- Avengers를 고유명사로 처리를 하는데, 항상 고유명사를 배제하도록 해야하는가? 배제해야하면 왜 배제해야하는가?
- 새로운 고유명사가 발생했을때, 이를 처리하는 방법은?
    - [이 사이트](https://heytech.tistory.com/15) 참고가 될거 같네요!


Q. VGG11 구현 시 마지막 Softmax를 넣으면 학습이 안되는데, 왜 그런걸까요?

A. Crossentropy loss는 Softmax + NLL Loss로 이뤄져 있기 때문에, 만약 VGG11 에서 softmax를 넣고 싶으면 NLL loss를 활용해야함

[참고](https://novister.tistory.com/46)

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

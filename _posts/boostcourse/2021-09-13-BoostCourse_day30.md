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

title: "[boostcourse] Day30 학습기록"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - boostcourse
tags:
  - []
date: 2021-09-13
last_modified_at: 2021-09-13
---

## 학습 내용

- CNN Visualization
- Auto Grad
- (선택과제) CNN visualization

<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 홍요한

참가자 : 박승찬, 한건우, 배지연, 강재현, 오하은, 홍요한

<br>

### 토의 내용

1. 모더레이터 순서 정하기

    기존 순서 유지

2. 멘토링 일정 정하기

    수요일 10시 예정 🥃

3. 질문
    - 강재현님: Grad-CAM

        Q: Grad-CAM에서 관심을 가지고 있는 activation map까지만 backpropagation을 진행하는데 activation map까지만 진행하면 이미지의 size가 다른데 어떻게 시각화를 진행하는 지 궁금

        - Grad-CAM에서 Backprop till conv가 무슨 의미인지 모르겠다.
        - 특정 conv의 특정 channel까지 한다고 하면, 해당 채널이 입력이미지의 어떤 부분을 나타내는지 모르겠다.

        A:  spacial dim이 다르니까 Upsampling을 진행하면 해결된다.

    - 홍요한님: 선택과제 1번, Activation Map
        - name과 module은 사용하지 않아서 지워줘도 될 거 같다.
        - input과 output은 우리가 채워주는 것이 아니라 모델이 돌아가면서 알아서 채워준다.
        - 함수를 우리가 직접 call하는 것이 아닌 해당함수를 넣어주면 알아서 불러온다.
        - functools.partial을 이용하면 미리 정해진 (input, output)를 제외한 매개변수 뿐 아니라 해당 함수와 관련된 다른 것 들을 미리 조작할 수 있다.
    - 홍요한님: YOLO, Grid에 동일 객체가 있을 경우

        - 위의 구조 (YOLO v1) 에서는 한 입력 영상에 여러 동일 객체가 있을 경우 검출이 어렵다.

            → 이를 YOLO v2에서 개선하였다.

4. 기타 토의
    - AI-Stage 1번 대회에 시각화 적용했다면?

        나이 관련 activation map에서는 주름에 많이 활성화되는 모습을 보였다.

    - HRNet
    - U-Net
        - mirror-padding: 논문에서 주변 픽셀과의 관계 확장? 이라고 주장
        - 요즘은 쓰이지 않음. feature의 W, H가 바뀌지 않게 padding을 더해주는 방식을 사용.

            : 구현의 편의성 및 확장성을 위함


<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

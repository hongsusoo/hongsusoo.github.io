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

title: "[선형대수] 행렬의 종류"
excerpt: "about : 선형대수"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  Linear Algebra
tags:
  - [선형대수]
date: 2021-12-01
last_modified_at: 2021-12-01
---

<br>

# 행렬의 종류

- 행렬

![image](https://user-images.githubusercontent.com/77658029/144184184-0b819c17-3e89-46b5-b01c-1ca1ded58a18.png)

## 정방 행렬(Square Matrix)

- 행과 열의 크기가 같은 행렬(m(행 크기)=n(열 크기))
- n차 정방행렬

## 대각 행렬(Diagonal Matrix)

- 주대각선 성분을 제외한 모든 성분이 0인 행렬

![image](https://user-images.githubusercontent.com/77658029/144185081-018f5c0c-1d11-43dc-83b1-9d2fd7c0528a.png)

## 전치행렬(Transposed Matrix)

- 원래의 행렬에서 행과 열을 서로 맞바꾼 행렬
- 표기 : $A^T$

<img src="https://user-images.githubusercontent.com/77658029/144182865-19cb050c-4e13-48d6-a628-17ae19233f02.png"  width="70%" height="70%"/>

## 단위 행렬(Identity Matrix)

- 주대각선 성분이 모두 1이고 그 외의 성분은 모두 0인 행렬
- $nxn$의 정방행렬 $A$와 단위행렬을 곱하면 $A$이 그대로 나옴
- 표기 : $I$

![image](https://user-images.githubusercontent.com/77658029/144185539-dfbf67e0-582f-4310-876a-5a9fb3087761.png)


## 역행렬(Inverse Matrix)

- n차 정방행렬 $A$에 대해서 $AB=BA=I$을 만족하는 행렬 B가 존재할때, B를 A의(A를 B의) **역행렬**이라고 함
- 표기 : A의 역행렬 = $A^{-1}$

![image](https://user-images.githubusercontent.com/77658029/144186245-b1cf5318-2bde-4300-ab9d-0a30521b8243.png)

## 직교 행렬(Orthogonal Matrix)

- 모든 Column들이 Otrhogonal Set을 이루는 행렬
- orthogonal은 직교를 의미하고, 직교행렬은 Normalized 되어 있는 형태(크기가 1)
- 특징 : 직교행렬을 전치하여 곱하면 단위행렬 $I$가 나옴, 이는 곳 직교행렬 $A^{-1}$ = $A^{T}$
![image](https://user-images.githubusercontent.com/77658029/144731417-f282826c-77ba-4df2-8fff-a048bfd922c3.png)

## 대칭행렬(Symmetic Matrix)

- 기존 행렬과 전치 행렬이 같은 행렬
- $A = A^{T}$
![image](https://user-images.githubusercontent.com/77658029/144731447-a1f4355a-be20-4556-a71f-355028eb642b.png)


**📌reference**
- [귀퉁이 서재 blog](https://bkshin.tistory.com/entry/%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D-19-%ED%96%89%EB%A0%AC)
- [존이 blog](https://blog.naver.com/mykepzzang/220990350484)
- [learn again](https://twlab.tistory.com/54)

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

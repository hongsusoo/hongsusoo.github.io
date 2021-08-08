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

title: "[AI basic] 베이즈 정리(bayes's theory)"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - AI
tags:
  - [python, AI Math]
date: 2021-08-04
last_modified_at: 2021-08-04
---
<br>

# 베이즈 정리

- 두 확률변수의 사전확률과 사후확률 사이의 관계를 나타내는 정리
- 불확실성 하에서의 의사결정문제를 수학적으로 다루는데 사용함
- 조건부 확률을 통해서 유도할 수 있음

<br>

## 조건부 확률

- A 확률이 일어났을때 B확률이 일어날 확률

![image](https://user-images.githubusercontent.com/77658029/128620393-3ed9c7dc-87b5-4033-aeae-27894dfd6df9.png)

🚨 주의해야할 사항으로 조건부확률의 경우 **인과관계**를 나타내는것이 아닌, **상관관계**를 나타냄

💡 인과관계(causality)를 확인하기 위해서는 중첩요인(confounding factor)의 효과를 제거해야함
   Z(중첩요인)에 대한 효과를 포함시켜주거나, 제거해야 정확한 T,R의 인과관계를 알 수 있음
   ![image](https://user-images.githubusercontent.com/77658029/128620846-9ed9bc34-1623-46e0-b032-484fc529f4b5.png)

<br>

## 베이즈 정리 해석

- 조건부 확률을 이용하여 정보를 갱신하는 방법을 제시해줌
- 사전 확률($P(B)$)이 주어졌을때 새로운 사건($P(A)$)이 일어나, 그 사건이 일어났을 때의 확률($P(B|A)$)로 반환

![image](https://user-images.githubusercontent.com/77658029/128620410-25c3b4f4-4a74-44aa-b75d-f8ca3e88ed29.png)

- 변수를 바꿔서 확인해보면 아래와 같이 생각할 수 있음

![image](https://user-images.githubusercontent.com/77658029/128620493-466be911-bdda-4400-907c-492f1229f91a.png)

- 정보를 chain처럼 연결하여 갱신할 수 있음

![image](https://user-images.githubusercontent.com/77658029/128620538-04785901-c597-4f15-b3e6-e59a734414a1.png)

<br>

### 베이즈 정리 시각화

![image](https://user-images.githubusercontent.com/77658029/128620634-59802f98-9938-4307-9cea-caf78e1e30a8.png)


**📌reference**
- boostcourse AI tech pre-course
- [베이즈 정리](https://ko.wikipedia.org/wiki/%EB%B2%A0%EC%9D%B4%EC%A6%88_%EC%A0%95%EB%A6%AC)

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

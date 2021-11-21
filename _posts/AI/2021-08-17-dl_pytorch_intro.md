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

title: "PyTorch 소개"
excerpt: "about : "
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - DL Basic
tags:
  - [PyTorch]
date: 2021-08-17
last_modified_at: 2021-08-17
---

<br>

# PyTorch intro

- Deep Learning를 코딩을 도와주는 frame work
- 직접 하나하나 coding을 해서 Deep Learning을 사용할 수 있음
- 하지만 요즘은 남이 만든걸 사용하여 효율을 높임
- 요즘은 Tensorflow(google), Pytorch(facebook) 두 가지로 많이 사용함


추천책 - 밑바닥부터 시작하는 Deep Learning

<br>

## TensorFlow(Keras) vs PyTorch

- 요즘은 점점 PyTorch를 많이 쓰는 추세임
- 학회나 다른 연구들에서 PyTorch가 많이 쓰이지만,
- Tensor는 Google의 도구로 Prodcution화에 유리하고, Cloud연결성, Multi GPU 사용에 유리함

![image](https://user-images.githubusercontent.com/77658029/129648538-e474971c-8d2c-406d-b9f1-2f88e69d9e7c.png)

![image](https://user-images.githubusercontent.com/77658029/129647676-ece5ffc7-35c4-47eb-a8c6-0174a1d3fcc2.png)



<br>

## Computational Graph

- 연산을 그래프화 하는걸 Computational Graph라고함

![image](https://user-images.githubusercontent.com/77658029/129647897-001da84a-8cd5-4db6-b4c3-6f660eff86e0.png)

- 그래프와 연산의 순서에 따라 크게 2가지 종류가 있음

1. Define and Run - TensorFlow
- 그래프를 먼저 그린 후 Data를 Feed 하는 형식으로 사용

2. Define by Run(Dynamic Computational Graph, DCG) - PyTorch
- 실행을 하면서 그래프를 생성하는 방식

![image](https://user-images.githubusercontent.com/77658029/129648216-48d82a89-533a-49ce-bc0a-4335f8cc1e7c.png)


<br>

## PyTorch의 장점

- Define By Run 방식의 Computational Graph → 바로바로 확인 가능
- Pythonic Code
- GPU 지원, API와 community가 활발함
- Numpy(구조, Tensor) + Autograd(자동미분) + Function(다양한 DL 함수)


<br>

**📌reference**
- boostcourse AI tech
- [standford DL lecture](http://cs231n.stanford.edu/slides/2017/cs231n_2017_lecture8.pdf)

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

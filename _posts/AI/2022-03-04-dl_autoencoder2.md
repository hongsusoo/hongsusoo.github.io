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

title: "Autoencoder 기초(2/5)"
excerpt: "about : Autoencoder"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - DL
tags:
  - [autoencoder]
date: 2022-03-04
last_modified_at: 2022-03-04
---

<br>
> 해당 글은 이활석님의 오토인코더의 모든 것 유튜브 영상을 바탕으로 제작되었습니다.

<iframe width="885" height="498" src="https://www.youtube.com/embed/o_peo6U7IRM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

--- 

**AutoEncoder**

딥러닝을 하다보면 가공된 데이터를 만들기 위해 많은 에너지를 쏟고 있다.

하여 최근 딥러닝 연구는 이런 데이터가 필요없는 비지도 학습으로 무게중심을 옮겨가고 있는데, Autoencoder는 비지도학습(**Unsupervised Learning**)의 대표적인 방법이다.

Autoencoder는 아래와 같은 구조를 가지고 있는데,

 <img src="https://user-images.githubusercontent.com/77658029/156111234-aad23ae9-d571-4ac7-b7ca-47aeacb5d2cd.png"  width="70%" height="70%"/>

Encoder를 통해 차원을 축소시키는 역할을 해주고(**Manifold Learning**), Decoder를 통해 차원을 복원하며 데이터를 생성하는 역할을 해준다.(**Generative Model Learning**)

학습의 경우는 **Negative Maximum Likelihood Estimation을 통한 Loss최소화**를 목적으로 학습하게 된다.

**main keywords**

1. Unsupervised Learning
2. ML(Maximum Likelihood) Density Estimation
3. Manifold Learning
4. Generative Model Learning

Autoencoder에 대한 정확한 이해를 위해 DNN과 Manifold learning에 대한 기초 지식을 쌓고(Chapter 1,2), Autoencoder에 대한 설명(Chapter 3,4), 그리고 어떻게 활용되는지(Chapter 5) 순서로 정리할 예정이다.

[chapter 1 정리](https://hongsusoo.github.io/math/math_matrix2)

---

# 2. Manifold



**📌reference**
- [오토인코더의 모든 것](https://www.youtube.com/watch?v=o_peo6U7IRM&t=3176s)

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

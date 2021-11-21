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

title: "경사하강법을 이용한 선형회귀식 유도"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - DL Basic
tags:
  - [gradient descent]
date: 2021-08-01
last_modified_at: 2021-08-01
---
<br>

# gradient Descent를 활용한 선형회귀

![image](https://user-images.githubusercontent.com/77658029/127756601-72738faa-a149-4481-a639-bcfecf300f4a.png)

- $n >= m$인 경우 하나의 선형적 해가 존재하지 않는다(모든 data가 일직선에 있는 경우가 있긴하지만, 그 부분은 현실적이지 않기 때문에 제외한다)
- 오차를 최소로 하는 $\beta$를 구하기 위해 $\hat Y = X\beta$로 정의하면
- 오차항인 $||Y-X\beta||_2$를 최소로 만드는 $\beta$를 구하는 식으로 바꿀 수 있다.
- $||Y-\hat Y||_2$을 목적식으로 하여 경사하강법을 사용하여 최소값을 구해보자

## 수식 유도

- $||Y-\hat Y||_2 = ||Y-X\beta||_2$를 최소로 하는 $\beta$ 구하기!

  ![image](https://user-images.githubusercontent.com/77658029/127757425-5dce7405-ad85-4091-8d43-f6ad5ee22eee.png)

>여기서 식 ②번을 유도하는 과정은 위해 식 ①번의 k번째 항을 정리해보자

![image](https://user-images.githubusercontent.com/77658029/127757431-64e3634d-980c-46ad-8c19-c44bce69d7aa.png)

<br>
```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

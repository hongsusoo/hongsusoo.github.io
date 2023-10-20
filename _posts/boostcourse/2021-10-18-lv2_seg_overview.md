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

title: "[Segmentation Task] Overview"
excerpt: "about : segmentation"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - boostcourse
tags:
  - [Segmentation]
date: 2021-10-18
last_modified_at: 2021-10-18
---

<br>

# COCO Format_Segmentation Task

- Json file 형태로 제공됨
- 학습 및 추론에 필요한 Json file로 이뤄짐

## Json File 구성

- info
![image](https://user-images.githubusercontent.com/77658029/137656294-770f8e53-5d6b-4699-b343-eb7fefc66d0b.png)

- licenses
![image](https://user-images.githubusercontent.com/77658029/137656312-bad8aab7-ca01-407d-80db-a3445e85e5c6.png)

- images : image 목록 및 각각의 width,heigh,file_name,id(image_id)
![image](https://user-images.githubusercontent.com/77658029/137656327-2b5b6b23-6de9-42e6-a1f3-c5db36e078f2.png)

- categories : class에 해당하는 id, name 및 supercategory
![image](https://user-images.githubusercontent.com/77658029/137656491-a56a0dcb-5151-4279-bdef-5312afcde35f.png)

- annotations :  class에 해당되는 pixel의 x, y 좌표로 구성, polygon형태로 되어 있어 순서가 중요함(좌표들을 순서대로 이으면 Object의 둘레를 그리게됨)

![image](https://user-images.githubusercontent.com/77658029/137656399-c4d29fe0-336f-4661-9487-15b0f9db6d63.png)


## DataLoader

- Shape of Image : Batch,3,H,W 
- Shape of Target : Batch, H,W -> pixel의 annotation 정보가 담겨 있기 때문에 Channel은 따로 필요없음


## 평가 Metric

- mean IoU

![image](https://user-images.githubusercontent.com/77658029/137659589-c51cfa11-edc1-4e05-b75d-2a1beb22e87b.png)

## Data Overview

- 10가지 Class에 대한 Segmentation 진행

![image](https://user-images.githubusercontent.com/77658029/139697022-f982371e-4162-40ac-bd15-847e1ab262a5.png)

### EDA

- 몇까지 구분하기 어려운 대상들이 존재함

![image](https://user-images.githubusercontent.com/77658029/139698599-81154ce2-15ae-4f0e-9477-8c8261d19ad4.png)


<br><br>

**📌reference**
- boostcourse AI tech

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

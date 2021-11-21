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

title: "02. Python 기초 문법(주석, indent)"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - Python Basic
tags:
  - 
date: 2021-06-28
last_modified_at: 2021-06-28
---

# Python 기본 문법(주석, indent)
---
<br>

## 1. 주석

주석은 프로그래밍시 메모의 목적으로 사용되며, 코드 실행 시 컴파일러나, 인터프리터에 의해 무시되어 프로그램에 영향을 주지 않음

### 1-1 Python 주석 종류

1. `# 블럭 주석`(단축키 : *ctrl + /*)
2. `print(10) # Comment 주석`
3. `'''여러줄 주석'''`

![image](https://user-images.githubusercontent.com/77658029/123656324-c5b46900-d86a-11eb-9c48-f052c0acf86a.png)

<br>

## 2. 들여쓰기

다른 언어의 경우 코드를 읽기 쉽도록 간격을 띄워쓰는 용도로 사용되지만, `Python의 경우 들여쓰기 자체가 문법`이기 때문에 조건문, 반복문, 함수, class 생성 등 여러 상황에서 들여쓰기가 잘못되면 error 발생함
(들여쓰기는 Space 4칸이 기준(tab과 동일))

### 2-1 error 확인

![image](https://user-images.githubusercontent.com/77658029/123657043-69057e00-d86b-11eb-9cbd-05ff4670e709.png)

![image](https://user-images.githubusercontent.com/77658029/123657318-a5d17500-d86b-11eb-8824-e8bc40231a56.png)


<br>

## 3. 띄어쓰기

Python 언어는 한줄씩 해석하는 언어이다. 모든 함수나 변수 정의할 때는 한 줄에 하나씩 정의해야하며, 만약 한줄에 쓰려고 하면 `;`를 사용해 구분해줘야함

![image](https://user-images.githubusercontent.com/77658029/123657600-e630f300-d86b-11eb-90b6-73c9086ad315.png)


**📌reference**
- [파이썬 코딩 도장](https://dojang.io/course/view.php?id=7)

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```
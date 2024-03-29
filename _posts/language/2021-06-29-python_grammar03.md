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

title: "03. Python 기초 문법(bool자료형, 비교, 논리 연산자)"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - python
tags:
  - 
date: 2021-06-29
last_modified_at: 2021-06-29
---

# bool자료형과 비교, 논리 연산자

boolean은 참, 거짓의 값을 가지고 있는 자료형으로 if, while 문에서 필수적으로 사용되는 자료형
비교, 논리 연산자의 결과값은 boolean 자료형으로 결과가 나온다.

## 비교 연산자
<br>

|기호|설명|
|---|---|
|a > b|a가 b보다 클 경우 True|
|a < b|a가 b보다 작을 경우 True|
|a >= b|a가 b보다 크거나 같은 경우 True|
|a <= b|a가 b보다 작거나 같은 경우 True|
|a == b|a,b 같을 경우 True|
|a != b|a,b 같지 않을 경우 True|
|a is b|a와 b의 객체(메모리 주소) 비교|

<br>

![image](https://user-images.githubusercontent.com/77658029/123719983-e2c65780-d8bd-11eb-8c6b-438431752661.png)

* python 에서는 자주 사용하는 값을 같은 메모리에 저장하기 때문에, -5~256의 숫자는 동일 메모리에서 관리하게 됨

![image](https://user-images.githubusercontent.com/77658029/123720326-c70f8100-d8be-11eb-801d-71390d2973bf.png)


![image](https://user-images.githubusercontent.com/77658029/123746155-364f9a00-d8ec-11eb-814d-5bdbb4fa6d06.png)

[참고자료](https://docs.python.org/2/c-api/int.html)

## 논리 연산자 

<br>

|기호|설명|
|---|---|
|a and b|a,b 모두 True일 경우 True|
|a or b|a,b 둘중 하나라도 True면 True|
|not a|a가 False면 True, True면 False|
|a & b|비트 연산시 둘 다 1이면 1, 집합에선 교집합|
|a \| b|비트 연산시 둘중 하나라도 1이면 1, 집합에선 합집합|
|a ~ b| 비트연산시 not|

<br>
---

**📌reference**
- [파이썬 코딩 도장](https://dojang.io/course/view.php?id=7)


```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```
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

title: "07. Python 기초 문법(if, elif, else)"
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

# if 조건문


> "돈이 많으면, 택시를 탈 것이다"

처럼 우리는 어떤 조건에 따라 결과값이 바뀌는 경우가 있는데, 이 경우 if 조건문을 통하여 통제가 가능함

## if 조건문 사용

`if 조건문 :` 의 형태로 조건문을 시작함, 콜론(:)을 써줘야 if 문 시작됨을 기억해야함
이때 조건문에 들어갈 수 있는 항목은 결과값이 boolean값으로 나오는 대상은 모두 넣을 수 있음
(ex. 비교연산자(with 논리연산자), boolean, 숫자, 문자 등)


## if 조건문 들여쓰기

python의 경우 if문의 시작과 끝을 들여쓰기로 구분하고 있어, 들여쓰기가 잘못되어 있으면 error를 발생시킴

```python
if True: 
    print(1)
     print(2)
```
result : 
![image](https://user-images.githubusercontent.com/77658029/123762828-22ad2f00-d8fe-11eb-8862-7d379919ca9a.png)
 ↳ 공백에 문제가 발생했다는 error 발생(indent는 공백을 의미)
 
 ## elif과 else
 
 elif는 else if를 의미하는데, 만약 if문에서 False로 빠져 나왔을때 다음 조건을 거는 함수
 else는 모든 if문과 elif문의 조건문이 모두 False일 경우 마지막으로 실행되는 구문
 elif와 else모두 단독으로 사용할 수 없고, if 조건문과 함께 사용될 수 있음

 ```python
if False:
    print("pass")
elif True:
    print('이부분 출력')
else : 
    print("pass")
```

**📌reference**
- [파이썬 코딩 도장](https://dojang.io/course/view.php?id=7)

---
<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```
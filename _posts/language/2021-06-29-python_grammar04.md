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

title: "04. Python 기초 문법(문자열, escape code)"
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

# 문자열

## 문자열 만들기
작은 따옴표(')와 큰 따옴표(")를 이용하여 문자열로 만들 수 있음

→ `'hello'`,`'''hello'''`,`"hello"`,`"""hello"""`

문자열 내에 따옴표를 출력하고 싶을 경우 
작은 따옴표(')출력은 큰 따옴표로 감싸주면 출력 가능하고, 그 반대로 큰 따옴표(")출력은 작은 따옴표로 감싸주면 출력 가능함

만약 두 가지 모두 출력하고 싶을 경우 '\'를 이용하하면 그 바로 뒤의 따옴표는 무시됨

```python
hello = "python 'hello'"
hello2 = 'python \'hello2\''
print(hello)
print(hello2)
```
result
![image](https://user-images.githubusercontent.com/77658029/123723211-e3162100-d8c4-11eb-88d1-75609a015e41.png)

만약 여러줄의 문자열을 만들 경우 따옴표 3개로 감싸주어 출력 가능함
ex)
```python
'''
hello
world
'''
```

## 이스케이프 코드(Escape Code)

- 문자열 안에 `"따옴표"`는 문자열의 따옴표인지, 내부 data에 따옴표인지 확인이 어려움
- 따옴표를 문자열 내에 표현하고 싶을때 `\`를 사용하혀 표현할 수 있음
- 그 이외에도 여러 문자를 문자열로 출력하고 싶을때 사용함

<br>

|기호|설명|
|---|---|
|\\'|작은 따옴표 출력|
|\\"|큰 따옴표 출력|
|\\|\ 출력|
|\n|enter key 아래로 줄바꿈|
|\t|tab key 수평 이동(space 4회)|
|\r|현재 줄의 맨 앞 글자로 이동|
|\b|back slash 한칸 앞을 지움|

<br>

**📌reference**
- [파이썬 코딩 도장](https://dojang.io/course/view.php?id=7)

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```
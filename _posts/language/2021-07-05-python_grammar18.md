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

title: "18. Python 기초 문법(Magic Method)"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - python
tags:
  - 
date: 2021-07-05
last_modified_at: 2021-07-05
---


# Magic Method

- 사칙연산이나, 조건문은 간단한 기호(+,-,*,/,>,<)로 연산할 수 있도록 도와주고, 특별한 상황이 됐을때 자동으로 동작하는 기능을 수행하는 method
- Python 내부에는 이미 여러가지 Magic Method를 가지고 있음
- `__매직메소드이름__` 형식으로 사용함

## Magic Method 동작 방법(`__add__`)

- `__add__` Method가 있는 경우 `+`에 대한 연산을 가능하게 한다 
- `x + y`라는 입력이 주어졌을 때, 이것은 `x.__add__(y)`로 연산을 하게 됨

**📰code**
```python
class AddExample():
    def __init__(self,i):
        self.i=i
    def __add__(self, other):
        return self.i + other.i
    
a=AddExample(3)
b=AddExample(5)
print(a+b)
```
**🔍result**
```
8
```

## 자주 사용하는 Magic Method

- `__init__` : 생성자라고 불리며, 인스턴스가 생성될때 파이썬 인터프리터에 의해 자동으로 호출되는 메소드
- `__main__` : 현재 실행되고 있는 파일에 붙는 이름

**📰code**
```python
class MyFunc:
    pass
print(__name__)
```
**🔍result**
```
__main__
```

- `__call__` : 함수를 불러올때 사용하는 `()`를 사용하면 function이라는 클래스 객체의 `__call__` 메소드를 호출하는 것

**📰code**
```python
class MyFunc:
    def __call__(self, *args, **kwargs):
        print("호출됨")

f = MyFunc()
f()
```
**🔍result**
```
호출됨
```

- `__getattribute__` : 메소드 호출시 (.)을 찍는데, 이때 호출되는 함수

**📰code**
```python
class Stock:
    def __getattribute__(self, item):
        print(item, "객체에 접근하셨습니다.")

s = Stock()
s.data
```
**🔍result**
```
data 객체에 접근하셨습니다.
```

## 비공개 속성

- 비공개 속성은 이름이 __ (밑줄 두 개)로 시작함
- 단, `__속성__`처럼 밑줄 두 개가 양 옆에 왔을 때는 Magic Method

**📌reference**
- [파이썬 코딩 도장](https://dojang.io/course/view.php?id=7)
- [school of web](http://schoolofweb.net/blog/posts/%ED%8C%8C%EC%9D%B4%EC%8D%AC-oop-part-6-%EB%A7%A4%EC%A7%81-%EB%A9%94%EC%86%8C%EB%93%9C-magic-method/)


```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```
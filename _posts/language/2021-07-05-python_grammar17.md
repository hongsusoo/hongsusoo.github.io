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

title: "17. Python 기초 문법(Class와 Method)"
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


# Python Class와 Method

## 객체지향언어(Object-Oriented Programming)

- `oop`, `oo`로 통용됨
- Python은 객체를 생성하여 여러가지 개념이나 형태를 표현
- 비슷한 속성(기능)들을 묶어 하나의 객체로 만들어 동일한 일을 효율적으로 처리할 수 있음
- 일정한 틀(class)를 활용하여 쿠키(object 혹은 instance)를 만들수가 있다. 
- 설계도는 `클래스`, 구현체는 `인스턴스`

## 인스턴스와 객체의 차이점

- 보통 객체만 지칭할때는 객체
- 클래스와 연관지어서 말할 때는 인스턴스라고 부름
- `a=list(range(10))`에서 a,b는 객체이고
- `a=list(range(10))` a,b는 list의 인스턴스

## Naming Rule

- class name : 띄어쓰기에 대문자 사용(naming rule → NamingRule)
- 변수(속성) name : 띄어쓰기에 under bar 사용(naming rule → naming_rule)


## class와 Method

- `class 클래스명`형식으로 class생성 
- method는 class내에 있는 함수를 뜻함
- `def method명`형식으로 method 생성

### Special Method(Magic Method)

- 앞뒤로 __ (밑줄두개)가 붙는 method는 파이썬이 자동으로 호출해주는 method
- **special method**, **magic method**라고 불림

> 자주 사용하는 Magic Method

- `__init__` : 생성자라고 불리며, 인스턴스가 생성될때 파이썬 인터프리터에 의해 자동으로 호출되는 메소드
- `__main__` : 현재 실행되고 있는 파일에 붙는 이름

```python
class MyFunc:
    pass
print(__name__)
```
result : `__main__`

- `__call__` : 함수를 불러올때 사용하는 `()`를 사용하면 function이라는 클래스 객체의 `__call__` 메소드를 호출하는 것

```python
class MyFunc:
    def __call__(self, *args, **kwargs):
        print("호출됨")

f = MyFunc()
f()
```
result : 호출됨

- `__getattribute__` : 메소드 호출시 (.)을 찍는데, 이때 호출되는 함수

```python
class Stock:
    def __getattribute__(self, item):
        print(item, "객체에 접근하셨습니다.")

s = Stock()
s.data
```
result : data 객체에 접근하셨습니다.




## 3. Attribute(속성)

- class 내부에 있는 변수나 메소드를 속성이라고 함

### 3-1 클래스 속성

- 클래스 속성의 위치는 Methon 밖에 나와있음(`__init__`밖에 있음)
- 하나의 인스턴스에 종속되어 있는 값이 아님
- 모든 인스턴스에 공유하는 속성값으로 하나의 인스턴스에 추가하면 다른 인스턴트도 추가됨

*사용예제*
```python
class Person:
    bag = []
    def put_bag(self,stuff):
        Person.bag.append(stuff) #self는 인스턴스에서 사용, self써도 상관없음

james=Person()
james.put_bag('책')

maria = Person()
maria.put_bag('열쇠')

print("james bag :",james.bag)
print("maria bag :",maria.bag)
print(Person.bag)
```
result : <br>
james bag : ['책', '열쇠'] <br>
maria bag : ['책', '열쇠'] <br>
['책', '열쇠']

### 3-2 인스턴스 속성

- `__init__` method 안에서 `self.속성`에 값을 할당함
- 사용 형식

```python
class 클래스이름:
    def __init__(self):
        self.속성=값
```
- 클래스에 ()를 붙여 인스턴스를 만들때 호출되는 method
- `__init__`(initialize)이라는 이름 그대로 인스턴스(객체)를 초기화함
- 앞뒤로 __ (밑줄두개)가 붙는 method는 파이썬이 자동으로 호출해주는 method
- special method, magic method라고 불림

*사용예제*
```python
class person():
    def __init__(self):
        self.hello='hello'
    def greeting(self):
        print(self.hello)

hong=person()
hong.greeting()
```
result : hello

**📌reference**
- [파이썬 코딩 도장](https://dojang.io/course/view.php?id=7)

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```
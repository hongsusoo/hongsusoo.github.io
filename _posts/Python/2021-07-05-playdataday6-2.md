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

title: "[playdata_day6] Python Class와 Method"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - py_grammar
tags:
  - [playdata]
date: 2021-07-05  
last_modified_at: 2021-07-05
---

# Python Class와 Method

## 0. 객체지향언어

- Python은 객체를 생성하여 여러가지 개념이나 형태를 표현
- 비슷한 속성(기능)들을 묶어 하나의 객체로 만들어 동일한 일을 효율적으로 처리할 수 있음
- 일정한 틀(class)를 활용하여 쿠키(객체)를 만들수가 있다. 

## 1. class와 메소드

- `class 클래스명`형식으로 class생성 
- method는 class내에 있는 함수를 뜻함
- `def method명`형식으로 method 생성

### 1-1 Special Method(Magic Method)

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


## 2. 인스턴스와 객체의 차이점

- 보통 객체만 지칭할때는 객체
- 클래스와 연관지어서 말할 때는 인스턴스라고 부름
- `a=list(range(10))`에서 a,b는 객체이고
- `a=list(range(10))` a,b는 list의 인스턴스

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

### 3-3 비공개 속성

- 비공개 속성은 이름이 __ (밑줄 두 개)로 시작함
- 단, `__속성__`처럼 밑줄 두 개가 양 옆에 왔을 때는 속성이 아님

## 4. 정적 메소드

- 인스턴스 없이 class의 메소드를 바로 호출/실행 할 수 있음
- 메서드의 실행이 외부 상태에 영향을 끼치지 않는 순수한 함수를 만들때 사용

### 4-1 @staticmethod(정적 메소드)

- 데코레이터 `@staticmethod`를 사용
- 초기화 해주고 나면 에러 발생함
- 인스턴스와 클래스 메소드와 다르게 매개 변수가 따로 없음
- 부모 클래스에서 속성을 먼저 찾음

```python
class a:
    t = '부모'
    @staticmethod
    def static_method():
        return a.t
class a_2(a):
    t = '자식'
print(a_2.static_method())
```
result : 부모

### 4-2 @classmethod(클래스 메소드)

- 인스턴스 없이 Method를 호출할 수 있음
- 인스턴스에서는 `self`를 사용했지만, 클래스 메소드는 `cls`를 첫 매개변수로 사용
- `cls`는 상속 받은 클래스에서 먼저 찾음
- class 변수를 가져와서 사용 가능함(`cls`로) 

```python
class a:
    t = '부모'
    @classmethod
    def class_method(cls):
        return cls.t
class a_2(a):
    t = '자식'
print(a_2.class_method())
```
result : 자식

## 5. 클래스 상속

- 기능은 그대로 유지한 채로 다른 기능을 추가할때 사용
- 기능을 물려주는 클래스를 기반 클래스(base class)_부모 클래스, 슈퍼 클래스
- 상속받은 클래스를 파생클래스(derived class)_자식 클래스, 서브 클래스
- 클래스 생성시 `()`를 붙이고 안에 기반 클래스 이름을 넣어서 활용
- `class 클래스명(기반클래스명):` 형식으로 사용

*list 상속받아 replace함수 만들기*

```python
class AdvancedList(list):
    def replace(self,b,a):
        while b in self:
            idx=self.index(b)
            self[idx]=a
        
x=AdvancedList([1,2,3,1,2,3,1,2,3])
x.replace(1,100)
print(x)
```
resutl : [100,2,3,100,2,3,100,2,3]


### 5-1 부모 클래스 속성 상속

- `super().__init__()` 통하여 부모의 생성자 내에 속성을 상속 받을 수 있음
- 만약 인수가 있을 경우에는 아래와 같이 error가 발생

```python
class a:
    def __init__(self,t):
        self.t= t
class a_2(a):
    def __init__(self):
        super().__init__()
    def print_t(self):
        print(self.t)
i=a_2()
i.print_t()
```
result :

![image](https://user-images.githubusercontent.com/77658029/124524701-00a03900-de37-11eb-8e99-eb195f0dc625.png)
↳ argument 't'가 없다고 error 발생

이 경우 우리는 t값을 어떻게 해서든 전달이 필요한데

3가지 해결 방향이있다

1. 부모 함수에서 직접 작성

```python
class a:
    def __init__(self):
        self.t= '상속'
class a_2(a):
    def __init__(self):
        super().__init__()
    def print_t(self):
        print(self.t)
i=a_2()
i.print_t()
```
result : 상속

2. 상속 받을 때 인수 전달

```python
class a:
    def __init__(self,t):
        self.t= t
class a_2(a):
    def __init__(self):
        super().__init__('상속') #상속 시 인수 전달
    def print_t(self):
        print(self.t)
i=a_2()
i.print_t()
```
result : 상속

3. 자식 클래스에서 인수 선언 후 객체 선언시 인수 전달

```python
class a:
    def __init__(self,t):
        self.t= t
class a_2(a):
    def __init__(self,t):
        super().__init__(t) #상속 시 변수 자체를 추가
    def print_t(self):
        print(self.t)
i=a_2('상속') #객체화 할때 인수 전달
i.print_t()
```
result : 상속

### 5-2 Method overriding

- overriding은 무시하다, 우성하다라는 뜻으로, 기반 클래스의 메소드를 무시하고 새로운 메소드를 만든다는 뜻
- Method overriding은 보통 프로그램에서 어떤 기능이 같은 메서드 이름으로 계속 사용되어야 할 때 사용
- `super().상속받을메소드()`로 상속받을 부모 메소드를 상속 받아서 기능을 사용할 수 있음

```python
class Person:
    def house(self):
        print("주소 : 서울시",end=' ')

class home(Person):
    def house(self):
        super().house()
        print('강서구')
h=home()
h.house()
```
result : <br>
주소 : 서울시 강서구


## 6. 다중 상속

- 여러개의 부모 클래스를 상속 받아서 사용함

```python 
class A:
    def aa(self):
        print('aa입니다')
        
class B:
    def bb(self):
        print('bb입니다')
        
class C(A,B):
    def cc(self):
        print('cc입니다')
i=C()
i.cc()
i.bb()
i.aa()
```
result : <br>
cc입니다 <br>
bb입니다 <br>
aa입니다 

## 7. 추상 클래스 사용

- 메서드의 목록만 가진 클래스 이며, 상속받은 자식 클래스에서 메서드 구현을 강제함
- 추상 클래스 목록 내에 메소드를 자식 클래스에서 구현하지 않으면 Error 발생

```python
from abc import * 

class StudentBase(metaclass=ABCMeta):
    @abstractmethod
    def study(self):
        pass
    
    @abstractmethod
    def go_to_school(self):
        pass    

class Student(StudentBase): #go_to_school 없기 때문에 Error 발생
    def study(self):
        print('공부하기')
        
james = Student()
james.study() 
```
![image](https://user-images.githubusercontent.com/77658029/124434715-297ceb80-ddaf-11eb-86e4-e904b93ed1b5.png)


<br><br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

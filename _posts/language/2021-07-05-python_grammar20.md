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

title: "20. Python 기초 문법(데코레이터(@))"
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

# python decorator

- 메서드를 장식하다고 하여 데코레이터라는 이름이 붙음
- `@`를 사용하여 메서드와 함수에 가벼운 기능을 추가할 수 있음
- 잘 사용하면 debugging할때 유용하게 사용 가능함

## @staticmethod(정적 메소드)

- 인스턴스 없이 class의 메소드를 바로 호출/실행 할 수 있음
- 메서드의 실행이 외부 상태에 영향을 끼치지 않는 순수한 함수를 만들때 사용
- 데코레이터 `@staticmethod`를 사용
- 초기화 해주고 나면 에러 발생함
- 인스턴스와 클래스 메소드와 다르게 매개 변수가 따로 없음
- 부모 클래스에서 속성을 먼저 찾음

**📰code**
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
**🔍result**
```
부모
```

## @classmethod(클래스 메소드)

- 인스턴스 없이 Method를 호출할 수 있음
- 인스턴스에서는 `self`를 사용했지만, 클래스 메소드는 `cls`를 첫 매개변수로 사용
- `cls`는 상속 받은 클래스에서 먼저 찾음
- class 변수를 가져와서 사용 가능함(`cls`로) 

**📰code**
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

**🔍result**
```
자식
```


## @abstractmethod(추상 메소드)

- 메서드의 목록만 가진 클래스 이며, 상속받은 자식 클래스에서 메서드 구현을 강제함
- 추상 클래스 목록 내에 메소드를 자식 클래스에서 구현하지 않으면 Error 발생

**📰code**
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
**🔍result**
![image](https://user-images.githubusercontent.com/77658029/124434715-297ceb80-ddaf-11eb-86e4-e904b93ed1b5.png)


## @trace

- 함수나 메소드앞에 `@`를 통하여 사용
- `@트레이스명`바로 다음에 오는 함수를 대상으로 진행됨
- 해당 함수가 실행 될때 `trace` 함수 or class가 동작함

*Source Code, class 타입*
**📰code**
```python
class Trace:
    def __init__(self,func):
        self.func = func

    def __call__(self, *args,**kwargs):
        r=self.func(*args,**kwargs)
        print(f'{self.func.__name__}(args={args},kwargs={kwargs}) -> {r}')
@trace
def get_max(*args):
    return max(args)
@trace
def get_min(**kwargs):
    return min(kwargs.values())

print(get_max(10,20))
print(get_min(x=10,y=20,z=30))
```
**🔍result**
```
get_max(args=(10, 20), kwargs={}) -> 20  
20  
get_min(args=(), kwargs={'x': 10, 'y': 20, 'z': 30}) -> 10  
10  
```

*Source Code, 함수 타입*
**📰code**
```python
def trace(func):
    def wrapper(*args,**kwargs):
        r=func(*args,**kwargs)
        print('{0}(args={1}, kwargs={2}) -> {3}'.format(func.__name__,args,kwargs,r))
        return r
    return wrapper

@trace
def get_max(*args):
    return max(args)

@trace
def get_min(**kwargs):
    return min(kwargs.values())

print(get_max(10,20))
print(get_min(x=10,y=20,z=30))
```
**🔍result**
``` 
get_max(args=(10, 20), kwargs={}) -> 20  
20  
get_min(args=(), kwargs={'x': 10, 'y': 20, 'z': 30}) -> 10  
10  
```


- 메서드의 목록만 가진 클래스 이며, 상속받은 자식 클래스에서 메서드 구현을 강제함
- 추상 클래스 목록 내에 메소드를 자식 클래스에서 구현하지 않으면 Error 발생

**📰code**
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
**🔍result**
![image](https://user-images.githubusercontent.com/77658029/124434715-297ceb80-ddaf-11eb-86e4-e904b93ed1b5.png)


**📌reference**
- [파이썬 코딩 도장](https://dojang.io/course/view.php?id=7)


```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```
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

title: "19. Python 기초 문법(Class 상속)"
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


# 클래스 상속

- 기능은 그대로 유지한 채로 다른 기능을 추가할때 사용
- 기능을 물려주는 클래스를 기반 클래스(base class)_부모 클래스, 슈퍼 클래스
- 상속받은 클래스를 파생클래스(derived class)_자식 클래스, 서브 클래스
- 클래스 생성시 `()`를 붙이고 안에 기반 클래스 이름을 넣어서 활용
- `class 클래스명(기반클래스명):` 형식으로 사용

*list 상속받아 replace함수 만들기*

**📰code**
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
**🔍result**
```
[100,2,3,100,2,3,100,2,3]
```

## 부모 클래스 속성 상속

- `super().__init__()` 통하여 부모의 생성자 내에 속성을 상속 받을 수 있음
- 만약 인수가 있을 경우에는 아래와 같이 error가 발생

**📰code**
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
**🔍result**
![image](https://user-images.githubusercontent.com/77658029/124524701-00a03900-de37-11eb-8e99-eb195f0dc625.png)
↳ argument 't'가 없다고 error 발생

이 경우 우리는 t값을 어떻게 해서든 전달이 필요한데

> 3가지 해결 방향

1. 부모 함수에서 직접 작성

**📰code**
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
**🔍result**
```
상속
```

2. 상속 받을 때 인수 전달

**📰code**
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
**🔍result**
```
상속
```

3. 자식 클래스에서 인수 선언 후 객체 선언시 인수 전달

**📰code**
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
**🔍result**
```
result : 상속
```

## Method overriding

- overriding은 무시하다, 우선하다라는 뜻으로, 기반 클래스의 메소드를 무시하고 새로운 메소드를 만든다는 뜻
- Method overriding은 보통 프로그램에서 어떤 기능이 같은 메서드 이름으로 계속 사용되어야 할 때 사용
- `super().상속받을메소드()`로 상속받을 부모 메소드를 상속 받아서 기능을 사용할 수 있음
**📰code**
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
**🔍result**
```
주소 : 서울시 강서구
```

## 다중 상속

- 여러개의 부모 클래스를 상속 받아서 사용함

**📰code**
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

**🔍result**
```
cc입니다
bb입니다
aa입니다 
```

**📌reference**
- [파이썬 코딩 도장](https://dojang.io/course/view.php?id=7)


```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```
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

title: "[playdata_day8] Python 모듈, 패키지"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - py_grammar
tags:
  - [playdata]
date: 2021-07-08
last_modified_at: 2021-07-08
---

# Python 모듈, 패키지

## 1. 모듈이란?

- 특정 기능을 `.py` 파일 단위로 작성한 것
- 여러가지 기능을 쉽게 사용할 수 있도록 도와줌

## 2. import로 모듈 수입하기

- import는 수입이라는 뜻으로 모듈
- `import` 하나에 여러 모듈을 import할 수 있음
- 모듈의 사용은 클래스와 비슷하게 사용할 수 있음
- `모듈.변수`, `모듈.함수` 형식으로 사용 가능함
- 현재 파일에서 구동되는 모듈의 `__name__`은 `__main__`으로 정해져있음
- 모듈 제작중 디버깅을 위한 실행 시 `if __name__ == '__main__':` 조건문을 활용하여 그 페이지에서만 동작할 수 있도록 함

### 2-1 import - as 모듈 이름 사용자 정의

- 모듈 import시 모듈의 이름이 길거나,사용자 편의의 문제로 변경할 수 있음
- `as` 키워드를 사용하여 지정할 수 있음

```python
import pandas as pd
import math as m
```

### 2-2 from - import 부분 모듈 가져오기

- 모듈에서 필요한 기능, 모듈만 import함
- `from 모듈명 import 필요한기능/변수`

```python
from math import pi, sqrt #,exp
print(pi)
print(sqrt(2))
print(exp(1))
```
result :  
![image](https://user-images.githubusercontent.com/77658029/124564301-e3da2480-de7b-11eb-9782-c0acca006c0d.png)

### 2-3 모듈 만들기 (함수)

- 간단한 list 더하기 모듈 만들기  

**sum_list.py**
```python 
def sum_list(a=[],b=[]):
    z=[]
    for i,j in zip(a,b):
        z.append(i+j)
    return z
```
**모듈 사용**
```python
from sum_list import sum_list
a=[1,2,3]
b=[5,4,3]
print(sum_list(a,b))
```
result : [6, 6, 6]

### 2-4 모듈 만들기 (클래스)

**Person.py**
```python
class Person:
    def __init__(self, name, age, address):
        self.name = name
        self.age = age
        self.address = address
        
    def greeting(self):
        print("안녕하세요. 저는 {0}입니다.".format(self.name))
```
**활용**
```python
import Person

tree = Person.Person('tree',28,'서울시')
tree.greeting()
```
result : 안녕하세요. 저는 tree입니다.


## 3. 패키지란?

- 여러가지 모듈을 모아놓은 파일

![image](https://user-images.githubusercontent.com/77658029/124778436-f2a80080-df7b-11eb-8e32-b018a497304d.png)

### 3-1 import로 패키지 가져오기

- `import 패키지명.모듈명 형식으로` 불러옴
- package 폴더안에 `__init__.py` 파일이 있어야 패키지로 인식함


**main.py**
```python
from pkg_calculator.calc_mul import mul
from pkg_calculator.calc_add import add

print(add(1,2))
print(mul(2,10))
```
result :  
3  
20

**pkg_calculator\calc_mul**
```python
def mul(x,y):
    return x*y
```

**pkg_calculator\calc_add**
```python
def add(x,y):
    return x+y
```

### 3-2 __init__.py 파일 활용하기

- package 내에 모듈들을 편하게 import하기 위해 __init__.py 안에서 미리 import 해놓을 수 있음
- 특이하게도 __init__.py안에서 함수까지 호출하더라도 함수를 바로 가져올 수 없었음
- 모듈명을 정확하게 지정해줘야 사용 가능함

> __init__.py에서 모듈+함수 호출

**__init__.py**
```python
from .calc_add import add
from .calc_mul import mul
```

**main.py**
```python
from pkg_calculator import *

print(calc_add.add(1,2))
print(calc_mul.mul(2,10))
print(dir())
```
result :  
3  
20  
['__builtins__', '__file__', '__name__', '__nonzero__', 'calc_add', 'calc_mul']

> __init__.py에서 모듈 호출

**__init__.py**
```python
from pkg_calculator import calc_add
from pkg_calculator import calc_mul
```

**main.py**
```python
from pkg_calculator import *

print(calc_add.add(1,2))
print(calc_mul.mul(2,10))
print(dir())
```
result :  
3  
20  
['__builtins__', '__file__', '__name__', '__nonzero__', 'calc_add', 'calc_mul']

<br><br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

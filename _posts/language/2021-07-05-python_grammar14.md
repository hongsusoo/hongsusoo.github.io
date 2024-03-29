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

title: "14. Python 기초 문법(함수, 변수, args*, kwargs**)"
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

# 함수

## 함수 만들기

- `def 함수명():`형식으로 선언 후 들여쓰기로 함수 내용을 정의함

```python 
def hello():
    print('hello world')
```
result : 
→ 호출이 되어야 출력됨

## 함수 호출

- 정의된 함수를 불러오는 작업이 필요
- `함수명()` 형식으로 호출할 수 있음

```python
def hello():
    print('hello world')
hello()
```
result : hello world

## 함수 작성과 호출 순서

- 함수를 선 작성 후 호출 가능
- python은 위에서부터 한 line씩 읽어들여 해석하는 언어여서 함수 정의 후 호출 가능

*선 호출 후 정의*
```python
h1()
def h1():
    print('hello world')
```
result : error 발생 <br>
![image](https://user-images.githubusercontent.com/77658029/124212222-8d8e7e00-db29-11eb-8dd3-c39f7604ecbf.png)
<br>

*선 정의 후 호출*
```python
def h2():
    print('hello world')
h2()
```
result : hello world


## parameter(매개변수) 지정

- 함수에서 사용할 변수를 전달해주는 변수
- 함수 정의 : `def 함수명(매개변수):`
- 함수 호출 : `함수명(매개변수)`

```python
def add(a,b):
    print(a+b)
add(10,11)
```
result : 21

## return(반환)

- 함수에서 진행한 결과를 반환하는 역할을 해줌
- 결과값을 변수로 저장하여 다시 사용할 수 있어 유용하게 사용 가능함

```python
def oper(a,b,o):
    if o=='+':  return a+b
    elif o=='-':return a-b
temp1=oper(10,11,'+')
temp2=oper(10,11,'-')
print(f'더하기 : {temp1}')
print(f'빼기 : {temp2}')
```
result : <br>
더하기 : 21 <br>
빼기 : -1

## unpacking(리스트, 튜플, 딕셔너리)
 
- list와 Tuple 앞에 `*`를 붙여 unpacking함
- dictionary 앞에 `**`를 붙여 unpacking함

```python
a=[1,2,3]
print(f'그대로 출력 : {a}')
print('언패킹 진행 :',sep = '\n',*a)
```
result : <br>
그대로 출력 : [1, 2, 3]  <br>
언패킹 진행 : <br>
1 <br>
2 <br>
3

## 가변 가능한 매개변수

- `*` unpacking을 이용하면 가변하는 매개변수 대응이 가능함
- 매개변수 개수를 유동적으로 활용 가능

```python
def p(*args):
    for arg in args:
        print(arg, end = ' ')
p(1,2,3)
print()
p(1,2,3,4,5,6)
```
result :  <br>
1 2 3  <br>
1 2 3 4 5 6 

## keyword argument

- 키워드 인수는 직접 인수에 들어갈 키워드를 입력하여 사용함
- print 함수에 end, sep 같은 인수들도 키워드 인수
- 키워드 인수는 위치를 바꿔도 상관없음

## 가변 가능한 키워드 인수

- `**`형식으로 사용할 수 있음
- 매개변수 이름은 관례적으로 keyword arguments를 줄여서 kwargs로 사용함
- 키워드 인수와 값의 갯수를 유동적으로 사용 가능

```python
def personal_info(**kwargs):
    for k,v in kwargs.items():
        print(k,':',v)

personal_info(name='ㅎㅇㅎ')
print()
personal_info(name='ㅎㅇㅎ',age='33',address='ㅅㅇㅅ')
```
result : <br>
name : ㅎㅇㅎ <br>
 <br>
name : ㅎㅇㅎ <br>
age : 33 <br>
address : ㅅㅇㅅ

## 인수별로 위치가 정해져 있음

- `함수명(일반 변수, 키워드인수, *가변변수, **가변 키워드인수)` 형식으로 사용됨

## default parameter(매개변수 초기값)

- `함수명(kwargs = default value)`형식으로 사용됨
- 매개변수를 통한 초기값이 지정되어 있는 경우 함수를 호출할때 그 변수는 따로 지정해주지 않아도 됨
- `print`함수의 `end="\n"`도 초기화된 값으로 따로 지정할 필요가 없이 사용 가능함

## lambda 표현식

- 간단한 함수를 구현하기 위한 함수
- 익명함수(anonymous function)라고도 불림
- `lambda 매개변수들 : 식`형식으로 사용됨
- 이름 없는 함수이기 때문에 위 상태로는 함수를 호출할 수 없어, 변수에 넣어서 사용 가능
- `(lambda 매개변수들 : 식)(입력)` 형식으로 인수를 바로 받을 수도 있음
- 반환값 부분은 변수 없이 한 줄로 표현 가능해야함


```python
y=10
plus_ten = lambda x:x+y
l=[1,2,3]
print(list(map(lambda x:x+y,l)))
print(list(map(plus_ten,l)))
```
result : <br>
[11, 12, 13] <br>
[11, 12, 13]

*if-else추가*
```python
a=[1,2,3,4,5,6,7,8,9,10]
print(list(map(lambda x:str(x) if x%3==0 else x,a))) # 3의 배수만 str으로 변경
```
result : [1, 2, '3', 4, 5, '6', 7, 8, '9', 10]


## filter 함수

- `filter(함수, 순서형자료)`형식으로 사용
- 함수는 boolean값으로 True인 값만 저장

```python
print(list(filter(lambda x:x%3==0,range(10))))
```
result : [0, 3, 6, 9]

## reduce 함수

- `reduce(함수, 순서형자료)`형식으로 사용
- `from functools import reduce` 모듈 불러와야함
- 0-1, (0-1)-2, ((0-1)-2)-3, ... 형식으로 연산 진행

![image](https://user-images.githubusercontent.com/77658029/124392086-c0ee2a00-dd2e-11eb-8135-ec6627872694.png)

*가장 큰 값 구하기*
```python
from functools import reduce
a=[1,4,7,5,3,2,3,6]
print(reduce(lambda x,y: max(x,y),a))
```
result : 7


## 클로저

- 함수를 둘러싼 환경(지역변수, 코드 등)을 계속유지하다가 함수를 호출할 때 다시 꺼내서 사용하는 함수를 클로저(closure)라고 함
- return에 내부함수를 넣어 클로저를 만듦
- return에 함수 넣을 때, `()`를 빼고 넣어서 작성함

![image](https://user-images.githubusercontent.com/77658029/124492652-b8115d00-ddef-11eb-861e-682aaeb51c39.png)

```python
def calc():
    a=10
    b=5
    def mul_add(x):
        return a*x+b
    return mul_add

c=calc()
print(c(1),c(3),c(5))
```
result : 15 35 55
<br><br>

**📌reference**
- [파이썬 코딩 도장](https://dojang.io/course/view.php?id=7)

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```
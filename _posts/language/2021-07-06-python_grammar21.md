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

title: "21. Python 기초 문법(예외처리)"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - python
tags:
  - 
date: 2021-07-06
last_modified_at: 2021-07-06
---

# Python 예외처리

- 예외(exception)란 코드를 실행하는 중에 발생한 에러
- 에러 발생하여도 프로그램이 멈추지 않고 계획한 방향으로 동작하게 함

## try-except 

- error 발생 시 실행 코드를 중단하고, 바로 except로 넘어가 코드를 실행함
- error 발생이 예상되는 곳에 사용하여 프로그램이 멈추지 않고 진행되도록 함
- 사용 방법

**📰code**
```python
try :
    실행할 코드
except : 
    예외가 발생했을 때 처리 코드
```

*사용 예제*
**📰code**
```python
y=[10,20,30]
x=0,1,2,4
for i,j in zip(range(4),x):
    try:
        print(y[i]/j)
    except ZeroDivisionError:
        print('숫자 0으로 못나눔')
    except IndexError:
        print('잘못된 인덱스')
```
**🔍result**
```
숫자 0으로 못나눔 <br>
20.0 <br>
15.0 <br>
잘못된 인덱스
```
## 예외의 에러 메시지 받기

- 예외 상황에서 에러에 대한 정보를 받아옴

**📰code**
```python
try:
    print(1/0)
except Exception as e:
    print(e)
```
**🔍result**
```
division by zero
```

## 예외 계층도

- index error 가 zerodivision보다 우선순위가 높음
- except선언 순서와 상관없이 python 내부에 프로그래밍 되어있는 순서가 있음

**📰code**
```python
y=[10,20,30]
x=0
i=5
try: print(y[i]/x)
except IndexError: print('잘못된 인덱스')
except ZeroDivisionError: print('숫자 0으로 못나눔')
```
**🔍result**
```
잘못된 인덱스
```

**📰code**
```python
y=[10,20,30]
x=0
i=5
try: print(y[i]/x)
except ZeroDivisionError: print('숫자 0으로 못나눔')
except IndexError: print('잘못된 인덱스')
```

**🔍result**
```
잘못된 인덱스
```

## else와 finally

- try가 정상적으로 진행되었을때, else로 진행됨
- try에 예외의 발생 여부와 상관없이 실행할 코드

**📰code**
```python
try: print(1/0)
except Exception as e: print('except :', e)
else : print('else : 문제 없음')
finally : print('finally : 끝')
```
**🔍result**
```
except : division by zero
finally : 끝
```

**📰code**
```python
try: print(1/1)
except Exception as e: print('except :', e)
else : print('else : 문제 없음')
finally : print('finally : 끝')
```
**🔍result**
```
try : 1.0 
else : 문제 없음 
finally : 끝
```

# 예외 발생시키기

- 기존에 없던 에러이지만 사용자의 필요에 의해 에러를 만들 수 있음

## raise
- raise를 통한 Exception에 저장된 에러는 지역 변수처럼 함수 안에서 사용되어도 밖에서도 사용 가능함

**📰code**
```python
try:
    x=3
    if x%2!=0:
        raise Exception('홀수')
    print(x)
except Exception as e:
    print('error code :',e)
```

**🔍result**
```
error code : 홀수
```

*함수를 통한 에러 코드 받기*
**📰code**
```python
def Chk_even():
    x=3
    if x%2!=0:
        raise Exception('홀수')
try:
    Chk_even()
except Exception as e:
    print('error code :',e)
```
**🔍result**
```
error code : 홀수
```

## assert

- 조건식이 맞지않으면 error 발생

**📰code**
```python
x=1
assert x%2==0, '짝수 아닙니다'
print(x)
```
**🔍result**
![image](https://user-images.githubusercontent.com/77658029/124528207-9b524500-de42-11eb-9471-939377730829.png)

# 예외 만들기

- 프로그래머가 직접 만든 예외를 사용할 수 있음
- raise와 동일한 결과가 나오지만, raise에 함수 자체를 사용하는 방법도 있음 
- 사용 방법

**📰code**
```python
class 예외이름(exception):
    def __init__(self):
        super().__init__('에러메세지')
```

- `Exception`에 에러메세지를 추가하였기 때문에 에러 발생시켰을때 확인 가능함

**📰code**
```python
class NotEvenError(Exception):
    def __init__(self):
        super().__init__('짝수가 아닙니다')

try:
    x=3
    if x%2!=0:
        raise NotEvenError
except Exception as e:
    print('error code :',e)
```

**🔍result**
```
error code : 짝수가 아닙니다
```

<br><br>

**📌reference**
- [파이썬 코딩 도장](https://dojang.io/course/view.php?id=7)


```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```
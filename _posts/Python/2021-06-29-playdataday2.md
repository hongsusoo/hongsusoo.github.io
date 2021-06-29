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

title: "[playdata_day2] Python 기초2"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - py_grammar
tags:
  - [playdata]
date: 2021-06-29
last_modified_at: 2021-06-29
---

# python 기초 2

## bool자료형과 비교, 논리 연산자

boolean은 참, 거짓의 값을 가지고 있는 자료형으로 if, while 문에서 필수적으로 사용되는 자료형
비교, 논리 연산자의 결과값은 boolean 자료형으로 결과가 나온다.

### 비교 연산자
|기호|설명|
|---|---|
|a > b|a가 b보다 클 경우 True|
|a < b|a가 b보다 작을 경우 True|
|a >= b|a가 b보다 크거나 같은 경우 True|
|a <= b|a가 b보다 작거나 같은 경우 True|
|a == b|a,b 같을 경우 True|
|a != b|a,b 같지 않을 경우 True|
|a is b|a와 b의 객체(메모리 주소) 비교|

![image](https://user-images.githubusercontent.com/77658029/123719983-e2c65780-d8bd-11eb-8c6b-438431752661.png)

* python 에서는 자주 사용하는 값을 같은 메모리에 저장하기 때문에, -5~256의 숫자는 동일 메모리에서 관리하게 됨

![image](https://user-images.githubusercontent.com/77658029/123720326-c70f8100-d8be-11eb-801d-71390d2973bf.png)


![image](https://user-images.githubusercontent.com/77658029/123746155-364f9a00-d8ec-11eb-814d-5bdbb4fa6d06.png)

[참고자료](https://docs.python.org/2/c-api/int.html)

### 논리 연산자 
|기호|설명|
|---|---|
|a and b|a,b 모두 True일 경우 True|
|a or b|a,b 둘중 하나라도 True면 True|
|not a|a가 False면 True, True면 False|
|a & b|비트 연산시 둘 다 1이면 1, 집합에선 교집합|
|a \| b|비트 연산시 둘중 하나라도 1이면 1, 집합에선 합집합|
|a ~ b| 비트연산시 not|
---

<br>

## 문자열

### 문자열 만들기
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

### 이스케이프 코드(Escape Code)

`\`를 사용하면 문자열(string)에서 따옴표로 감싸주면서 생기는 여러가지 문제점이 생기는데, 그 문제를 보완해 주는 기능
한 가지 예로 따옴표를 문자열 내에 표현하고 싶을때 `\`를 사용하혀 표현할 수 있음

|기호|설명|
|---|---|
|\'|작은 따옴표 출력|
|\"|큰 따옴표 출력|
|\\|\ 출력|
|\n|enter key 아래로 줄바꿈|
|\t|tab key 수평 이동(space 4회)|
|\r|현재 줄의 맨 앞 글자로 이동|
|\b|back slash 한칸 앞을 지움|

---
<br>

## 리스트와 튜플

### 리스트 생성

list는 목록이라는 뜻으로 순서에 맞춰 항목을 저장해주는 자료형
python에서의 list는 여러 자료형을 list의 요소로 넣을 수 있다. 

*생성 방법*
1. `listname = [값, 값, 값]`
2. `listname = [] #빈 list`
3. `listname = list() #빈 list`


### 튜플 생성

튜플은 변경할 수 없는 list라고 생각할 수 있음 list와 다르게 소괄호(`(소괄호)`)를 사용하여 나타내고 콤마로 요소를 구분함

*사용방법*
1. `tuplename = (값,값,값)`
2. `tuplename = tuple() #빈 tuple`
3. `tuplename = 값, 값, 값`

한 가지 주의해야할 것은 Tuple값은 위에서 언급된 내용처럼 내용 변경이 불가하고, 값 하나로 tuple을 생성할때 (값,)뒤에 콤마를 찍어줘야 tuple로 인식됨

```python
a=(1)
b=(2,)
print('a=',type(a),'b=',type(b))
```

result
![image](https://user-images.githubusercontent.com/77658029/123728233-ef52ac00-d8cd-11eb-8b7e-78eedc12c734.png)



### range 활용한 list, tuple 생성

range는 간단한 규칙의 연속된 숫자를 만들어 내는 함수로, type은 range로 제공을 해주고 있음
그 값을 확인하기 위해서는 list, tuple같은 자료형으로 형변환 하여 확인할 수 있다.

*사용방법*
range(시작, 끝, 간격)

예를 들어 
시작 = 10
끝 = 1
간격 = -2

list(range(10,1,-2)) → [10, 8, 6, 4, 2]
tuple(range(10,1,-2)) → (10, 8, 6, 4, 2)

---
<br>

## sepuence 자료형

list, tuple, range, string, bytes?, bytesarry?등 자료형은  연속적인 자료로 저장되는데, 이런걸 시퀀스 자료형이라고 함
시퀀스 자료형에서 사용할 수 있는 몇까지 유용한 기능이 있음

### in 연산자(not in)

`a in sepquence자료`으로 사용하여 a가 sequence 내에 있는지 확인하고, 있으면 True 없으면 False로 boolean자료형으로 결과값이 출력됨
`in`과 반대로  `not in` 연산자는 있으면 False, 없으면 True로 출력하게 됨

### 연결하기

객체를 서로 연결하고, 여러개의 시퀀스 자료를 하나의 시퀀스 자료로 구성할 수 있음
주의해야할 사항은 순서가 있기 때문에 더하기에 대해서 교환법칙이 성립하지 않는다. 

*ex)*
a=[1,2,3]
b=[4,5,6]
a+b → [1,2,3,4,5,6]
b+a → [4,5,6,1,2,3]

### 반복하기

\*연산자를 사용하여 시퀀스 객체를 반복한 값을 저장할 수 있음

*ex)*
a=[1,2,3]*3
a=[1,2,3,1,2,3,1,2,3]

### 요소 개수

`len`함수를 이용하여 요소의 개수를 구할 수 있음

*ex)*
1. `len('hello world')` → result : 11
2. `len('hello\' world')` → result : 12

여기서 주의해야할 점은 문자열에서 이스케이프 코드는 1개의 문자로 인식함

### index 사용

index는 위치값을 뜻하는데 국어사전의 ㄱ,ㄴ,ㄷ과 동일한 의미를 갖음
시퀀스 객체는 index를 통하여 요소에 접근할 수 있어서 쉽게 해당 값을 가져올 수 있음

len과 동일하게 이스케이프 코드는 1개의 문자로 인식하여 출력됨

![image](https://user-images.githubusercontent.com/77658029/123733263-2462fc80-d8d6-11eb-88f7-5d725d56c61c.png)

```python
s='hello\' world'
print(s[4],s[5],s[6],s[7],sep='')
```
result : o' w

또한 음수로 index를 불러 올 수 있는데 

![image](https://user-images.githubusercontent.com/77658029/123733880-4c9f2b00-d8d7-11eb-9a7b-bc93f6cf2f3e.png)



### slicing

index는 요소 하나씩 접근할 수 있었다면, slicing은 여러 index의 값을 한번에 가져오는 기능
range에서 숫자열을 가져오는 방법과 동일하지만 range는 `,`로 구분되고, slicing은 `:`로 구분됨

*사용방법*
sequence object[시작:끝:간격]

![image](https://user-images.githubusercontent.com/77658029/123734802-faf7a000-d8d8-11eb-9f07-c363b8af3d2a.png)



### 요소 할당(list 자료형)

index으로 우리가 선정한 값을 변수에 값을 넣듯이 값을 대체할 수 있음, list 자료형에서만 사용 가능함
slicing 한 값도 변경 할 수 있음
ex)
```python
a=[1,2,3]
a[0]=3
print(a)
```
result : [3,2,3]

### 요소 삭제(list 자료형, del 함수) 

요소값을 삭제할 수 있음

*사용방법*
del 요소값

ex)
```python
a=[1,2,3]
del a[0]
print(a)
```
result : [2,3]

---

<br>

## dictionary

Python에서 제공하는 자료형으로 연관된 값을 묶어서 저장하는 용도로 사용됨

시퀀스 자료형에서의 Index값 대신에 딕셔너리에서는 key값으로 Value를 저장할 수 있음

딕셔너리에 key값으로 정수, 튜플 등 여러 자료형이 들어갈 수 있지만, list와 dictionary는 들어갈 수 없음(hashable 한 자료형만 가능,<u>hash()함수를 사용하여 key값 가능여부 확인 가능 </u>)

index와 동일하게 유일한 값으로 이뤄져야함(key값 중복이 될 경우 마지막 값으로 대체됨)

*사용방법*
key값:value값을 쌍으로하고 항목별로 콤마로 구분짓고, 중괄호로 감싸서 사용함
1. 딕셔녀리 = {key1:value1, key2:value2, ...}
2. 딕셔너리 = dict(key1=value1, key2=value2) # key값은 변수로 지정할 수 있는 값만 넣을 수 있음
3. 딕셔너리 = dict(zip([key1,key2],[value1,value2]))

### key값으로 value 출력

```python
c = {"a" : "코딩", "b" : ["공","부"], "c" : ("하","자"), "d" : 111 }
print(c["a"]) 
```
result : "코딩"

---
<br>

## if 조건문


> "돈이 많으면, 택시를 탈 것이다"

처럼 우리는 어떤 조건에 따라 결과값이 바뀌는 경우가 있는데, 이 경우 if 조건문을 통하여 통제가 가능함

### if 조건문 사용

`if 조건문 :` 의 형태로 조건문을 시작함, 콜론(:)을 써줘야 if 문 시작됨을 기억해야함
이때 조건문에 들어갈 수 있는 항목은 결과값이 boolean값으로 나오는 대상은 모두 넣을 수 있음
(ex. 비교연산자(with 논리연산자), boolean, 숫자, 문자 등)


### if 조건문 들여쓰기

python의 경우 if문의 시작과 끝을 들여쓰기로 구분하고 있어, 들여쓰기가 잘못되어 있으면 error를 발생시킴

```python
if True: 
    print(1)
     print(2)
```
result : 
![image](https://user-images.githubusercontent.com/77658029/123762828-22ad2f00-d8fe-11eb-8862-7d379919ca9a.png)
 ↳ 공백에 문제가 발생했다는 error 발생(indent는 공백을 의미)
 
 ### elif과 else
 
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



```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```
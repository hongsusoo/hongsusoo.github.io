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

title: "11. Python 기초 문법(dictionary 다루기)"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - python
tags:
  - 
date: 2021-07-01
last_modified_at: 2021-07-01
---
# Dictionary 다루기

## setdefault

- dictionary에 key,value값을 추가해줌

```python
x = {'a' : 10, 'b' : 20, 'c' : 30, 'd' : 40}
x.setdefault('e')
x.setdefault('f', 100)
print(x)
```
result : {'a': 10, 'b': 20, 'c': 30, 'd': 40, 'e': None, 'f': 100}

## update

- dictionary의 key에 해당하는 value값을 수정 및 추가 가능
- `dic.update({key:'value'})`형식으로 사용(key는 숫자, 튜플 등 가능함)
- key가 문자열 형태이면 `dic.update(key='value')`형식으로 사용 가능

```python
y={1:'one',2:'two'}
y.update({1:'ONE',3:'THREE'})
y.update(a="에")
print(y)
```
result : {1: 'ONE', 2: 'two', 3: 'THREE', 'a': '에'}

### list 형식으로 update

- `[[key1,value1],[key2,value2]]`형식으로 update가능

```python
y={1:'one',2:'two'}
y.update([[3,'Three'],[4,'Four']])
print(y)
```
result : {1: 'one', 2: 'two', 3: 'Three', 4: 'Four'}

## pop(삭제)

- dictionary 내에서 key-value 값을 삭제한 후 value 반환
- 만약 key값이 없을 경우에 대한 처리기능 있음
- `dic.pop(key,'key없을경우 출력')` 형식으로 사용

```python
y={1:'one',2:'two'}
print(y.pop(1,"key 없음"))
print(y.pop(1,"key 없음"))
```
result : <br>
one <br>
key 없음

### popitem(맨뒤 삭제)

- dictionary는 key-value 묶음으로 되어있는데, 이 묶음을 item이라고함
- 맨 뒤에 item을 반환하고, dictionary 내에서 제거
- `dic.popitem()`형식으로 사용

```python
y={1:'one',2:'two'}
print(y.popitem())
```
result : (2, 'two')

## get

- dictionary 내에서 찾고자 하는 key를 입력하면 Value 반환
- pop과 다르게 항목이 삭제되지 않고 가져오기만함

```python
y={1:'one',2:'two'}
print(y.get(1))
```
result : 'one'


## keys, values, items

- keys는 dictionary의 key들을 가져옴
- values는 dictionary의 value들을 가져옴
- dict_keys() type이기 때문에 sequecne 자료형 처럼 subscriptable할 수 없음

```python
x={'a':10,'b':20,'c':30,'d':40}
print(f'keys = {x.keys()}')
print(f'values = {x.values()}')
print(f'items = {x.items()}')
```
result : <br>
keys = dict_keys(['a', 'b', 'c', 'd']) <br>
values = dict_values([10, 20, 30, 40]) <br>
items = dict_items([('a', 10), ('b', 20), ('c', 30), ('d', 40)])  


## fromkeys(w. list, tuple)

- 리스트나 튜플을 key값으로 하여 dictionary 생성
- `dict.fromkeys(keys,value)`형식으로 사용
- value 지정 안해주면 None으로 자동 저장

```python
keys = ['a','b','c','d']
x=dict.fromkeys(keys)
y=dict.fromkeys(keys,100)
print(f'x = {x}')
print(f'y = {y}')
```
result : <br>
x = {'a': None, 'b': None, 'c': None, 'd': None} <br>
y = {'a': 100, 'b': 100, 'c': 100, 'd': 100}

## dictionary 표현식

```python
print({key : value for key,value in dict.fromkeys( ['a','b','c','d']).items()})
print({key : 0 for key in dict.fromkeys( ['a','b','c','d']).keys()})
```
result : <br>
{'a': None, 'b': None, 'c': None, 'd': None} <br>
{'a': 0, 'b': 0, 'c': 0, 'd': 0}


## Dictionary 안에 Dictionary

- `딕셔너리 = {key1:{keyA:valueA},key2:{keyB:valueB}}` 형식으로 된 형태
- key값을 연속으로 사용하여 value값 가져올 수 있음

```python
x={'a':{'A' :10},'b':{'B':20}}
print(x['a']['A'])
```
result : 10

## dictionary 할당과 복사

- list와 동일하게 dictionary도 복사할 경우 메모리를 공유하여하 나를 변경하면, 다른 하나도 변경됨
- dictionary 복사 시 모든 item을 하나씩 복사해줘야함
- dic.copy()를 사용하면 새롭게 메모리를 할당하여 할 수 있음

```python
x={'a':10,'b':20,'c':30,'d':40}
y=x
z=x.copy()
k={k:v for k,v in x.items()}
print("x, y 메모리 비교 : ",x is y)
print("x, z 메모리 비교 : ",x is z)
print("x, k 메모리 비교 : ",x is k)
```
result : <br>
x, y 메모리 비교 :  True <br>
x, z 메모리 비교 :  False <br>
x, k 메모리 비교 :  False


## deepcopy 

- 중첩된 dictionary의 경우는 copy로 해도 원본과 복사본 모두 변경됨
- 이럴땐 import copy 모듈에 있는 deepcopy 함수를 이용해야함



## clear

- dictionary 전체 item을 제거
- `dic.clear()` 형식으로 사용

**📌reference**
- [파이썬 코딩 도장](https://dojang.io/course/view.php?id=7)


```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```
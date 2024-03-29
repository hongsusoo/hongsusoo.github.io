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

title: "09. Python 기초 문법(list 함수, tuple)"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - python
tags:
  - 
date: 2021-06-30
last_modified_at: 2021-06-30
---

# 1. list 응용

## 1-1 append

- 리스트 안에 요소를 추가 할 수 있도록 도와줌
- 무조건 맨 뒤로 길이늘 늘려 추가하게됨
- list, tuple, 수 등 여러 자료형을 append 할 수 있음
- 총 list 길이는 1만큼 증가함

## 1-2 extend

- 리스트를 연장시키는 방법
- sequence 자료형에서 나왔던 sequence 객체간 `+` 연산과 동일함
- append는 여러 자료형을 추가 할 수 있지만, extend는 같은 자료형에서 연산 가능함

## 1-3 insert

- 특정 번지(index)에 요소를 추가할 수 있음
- 만약 번지를 list의 크기보다 큰 값으로 넣으면, 제일 마지막 항목으로 요소가 추가됨(append와 동일 기능)
- `list명[a:a] = "추가요소값"`으로 진행하면, insert(a)와 동일하게 동작함

```python
a=[1,1,1]
b=[1,1,1]
a.insert(1,'a')
b[1:1]=['a']
print("a=",a,", b=",b,sep='')
```
result : a=[1, 'a', 1, 1], b=[1, 'a', 1, 1]

## 1-4 pop

- 리스트에서 값을 삭제함
- pop()을 하면 제일 마지막 항목이 제거
- del과 차이점은 del은 단순 삭제이고, pop은 빼내서 출력으로 나온다음 삭제함

```python
a=[1,2,3,1,2]
print(a.pop())
print(a)
```
result :<br>
2 → pop()하며 지워진 값을 내뱉고(del로 지우면 지운값을 내뱉지 않고 지워지기만함)<br>
[1, 2, 3, 1]  → list에서는 항목이 지워짐

## 1-5 remove

- remove(값) 해당 값을 삭제함
- del이나, pop은 index를 입력으로 받아 해당 항목을 삭제하고, remove는 value를 입력받아 제거함
- default로 맨 처음 나오는 값 1개만 지움, 추가적으로 몇개 지울지 선정 가능

```python
a=[1,2,3,1,2]
a.remove(1)
print(a)
```
result : [2, 3, 1, 2]  → 맨 처음 나온 value값만 삭제됨

## 1-6 stack 만들기(자료구조)

- append()로 추가하고, pop()으로 제거하여 stack 자료구조로 사용 가능
- LIFO(Last In First Out)


## 1-7 Que 만들기(자료구조)

- append()로 추가하고, pop(0)으로 제거하여 Que 구조형태로 사용 가능
- FIFO(First In First Out)

## 1-8 index

- value를 input으로 받아 index를 출력해주는 함수
- `list명.index(value,st,end)`으로 사용 가능하고 index `st`번부터 `end`번 사이에 처음으로 나오는 value값의 위치를 출력

```python
a=['a','b','c','d','a','b','a','b']
print(a.index('a'), end=' ')
print(a.index('a',2,7))
```
result : 0 4

## 1-9 count

- list내에 특정 요소값이 몇개 있는지 확인하는 함수
- value값을 입력받아 개수로 출력

```python 
a=[1,1,2,3]
print(a.count(1))
```
result : 2

## 1-10 reverse

- 거꾸로 바꿈
- reversed()와는 다름(`reversed(sequence명)`형식으로 사용)
- `list명.reverse()`형식으로 사용됨

## 1-11 sort

- list를 오름차순으로 정리함
- 문자면 abc, 가나다 순으로 정리됨
- `list명.sort()`형식으로 사용함
- `list명.sort(reverse=True)`로 하면 내림차순으로 정리됨
- reverse=False가 default값

```python
a=[1,3,5,4,2]
a.sort(reverse=True)
print(a)
```
result : 5 4 3 2 1

## 1-12 Shallow Copy(얕은 복사)

- List의 복사는 메모리를 공유하는 방식으로 복사가됨(기본적으로는 얕은 복사)
- 원본과 복사본이 있을때, 둘중에 하나가 수정되면 다른 하나도 함께 수정됨

*얕은 복사*
```python
a=[1,2,3]
b=a
print( a is b)
```
result : True

## 1-13 list의 deep copy

- 얕은 복사와 다르게 메모리를 공유하지 않아 한 쪽에서 변경해도 다른 쪽에 영향을 주지 않음
- list를 깊은 복사를 하기 위해서는 요소별로 복사가 필요함

*깊은 복사*
```python
a=[1,2,3]
b=[i for i in a]
print(a is b)
```
result : False

## 1-14 enumerate

- sequence 객체에서 index와 value값을 모두 출력할 때 사용함
- 기본적으로 start=0으로 셋팅되어 있고, 필요시 start = 숫자로 시작값 바꿀 수 있음

```python
a='hello world'
for i,v in enumerate(a):
    print('num :',i,"value :",v)
```
result :<br>
![image](https://user-images.githubusercontent.com/77658029/123909902-ac1f3880-d9b4-11eb-95c1-22c9024c3974.png)

## 1-15 min, max, sum

- list의 min, max값을 구할 수 있고, sum은 list의 전체 합을 구할 수 있음
- `min(list명)`, `max(list명)`, `sum(list명)` 형식으로 사용됨

## 1-16 clear

- list의 모든 요소를 삭제함

## 1-17 list 표현식

- for문을 활용해 list를 구성할때, 한 line에서 구현할 수 있는 방법
- deepcopy에서 자주 사용됨

### 1-17-1 list 표현식 기본

```python
a=[1,2,3]
b=[i+3 for i in a]
print(b)
```
result = [4, 5, 6]

### 1-17-2 list 표현식 if-else문

- list 표현식과 if문을 함께 사용할 수 있다
- `if`만 사용될 땐 for문 뒤에서 쓰이고 `else`와 함께 사용될 경우 for문 앞에서 쓰임
- 앞서 얘기했던 내용처럼 for문도 else와 같이 사용되기 때문에 어디에 걸려있는 else인지 오해를 없애기 위해 위치에 차이를 둠


```python
a=[i for i in range(10) if i%2==0]
print(f'a={a}')
b=[i if i%2==0 else '홀' for i in range(10)]
print(f'b={b}')
```
result : <br>
a=[0, 2, 4, 6, 8]<br>
b=[0, '홀', 2, '홀', 4, '홀', 6, '홀', 8, '홀']


### 1-18 map 

- list의 각 요소별로 접근하여 일괄적인 함수를 적용시킴
- `map(함수, list)` 형식으로 사용됨
- map으로 바로 출력할 경우 map 형식으로 출력하여 확인이 어려워, list, tuple로 자료형을 선언해줘야함

```python
a=[1,2,3,4]
print(map(str,a))
print(list(map(str,a)))
```
result : <br>
<map object at 0x0000020D1056D760><br>
['1', '2', '3', '4']

<br>

# 2. Tuple 응용

- Tuple은 우선 변경이 불가능함으로 List에서 사용한 append, insert, del, remove 함수 등 변경이 생기는 함수는 사용 불가
- min, max, sum 함수는 그대로 사용가능

## 2-1 Tuple 표현식

- list와 동일하게 한 line에 tuple 만들 수 있음
- `tuple(식 for 변수 in 리스트 if 조건문)` 형식으로 활용됨
- list에서는 괄호만 써서 가능했지만, tuple에서는 소괄호만 쓰면 generator 형식이 됨

**📌reference**
- [파이썬 코딩 도장](https://dojang.io/course/view.php?id=7)

---
<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```
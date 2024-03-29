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

title: "08. Python 기초 문법(for, while)"
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

# 반복문(for, while)

프로그래밍 할때 여러가지 구문을 반복해서 출력하거나 연산해야하는 작업들을 할때가 많이 주어진다. 컴퓨터를 제대로 사용하기 위한 가장 기본이되는 구문이 아닐까 생각한다. 반복문으로 자주 사용되는 것은 for와 while이 있는데 둘의 사용 방법은 참조하면 좋을것 같다.

## 1. for문

for문은 우리가 일일이 반복해야할 일을 도와주는 도구로 **시퀀스 객체**의 요소별로 접근하거나, 일련의 숫자의 증감에 대해 코딩할 때 유용하게 사용할 수 있음, for문도 들여쓰기로 loop가 정해지기 때문에 들여쓰기에 신경쓰며 프로그래밍 필요함

### 1-1 for문 사용(with range)

가장 기초적인 방식으로 `for i in range(횟수):` range를 활용하여 for문을 사용할 수 있음

```python
for i in range(1,20,5):
    print(i, end=' ')
```
result : 1 6 11 16

for문을 돌리때 반대로 돌려야할 경우가 생기는데, 그때는 reversed 함수를 이용하면 쉽게 구현할 수 있음

```python
for i in reversed(range(1,20,5)):
    print(i, end=' ')
```
result : 16 11 6 1


### 1-2 for문 사용(with Tuple)

Tuple도 range와 동일하게 사용할 수 있는데, 

`in` 뒤에 Tuple 객체를 넣어 사용할 수 있음

```python
t=('a','b','c')
for i in t:
    print(i, end=' ')
```
result : a b c

```python
t=('a','b','c')
for i in reversed(t):
    print(i, end=' ')
```
result : c b a

### 1-3 for문 사용(with string)

```python
s="hello"
for i in s:
    print(i, end=' ')
```
result : h e l l o

```python
s="hello"
for i in reversed(s):
    print(i, end=' ')
```
result : o l l e h

### 1-4 for문 사용(list)

```python
l=[1,2,3,4]
for i in l:
    pritn(i, end=' ')
```
result : 1 2 3 4

list도 동일하게 reversed 구문을 사용할 수 있음

## 2. while문

for문에서는 sequence 객체를 통하여 반복 작업을 진행하였지만, while문의 경우는 조건문에 의해 while문 동작을 제어할 수 있음
while문도 들여쓰기로 loop가 결정되기 때문에 프로그래밍 할때 신경써줘야 함
if문과 동일하게 조건문이 True인 동안 반복수행하게 되기 때문에 적절한 제어할 수 있는 기능을 추가해야 함

### 2-1 while문 사용(비교연산자 제어)

```python
i=0
while i<5:
    print(i,end=' ')
    i+=1
```
result : 0 1 2 3 4

### 2-2 while문 사용(비교+논리연산자 제어)

```python
i=0
j=5
while i<5 and j>0:
    print(i+j,end=' ')
    i+=1
    j-=1
```
result : 5 5 5 5 5

### 2-3 while문 사용(boolean)

```python
i=0
while True:
    if i ==5:
        break
    i+=1
    print(i, end=' ')
```
result : 1 2 3 4 5 


## 3. 반복문제어

반복문을 제어할 수 있어야 좀 더 세밀한 프로그래밍 작업이 가능하다 
break와 continue를 통하여 반복문 제어할 수 있음

### 3-1 break

`break문`은 반복되는 loop를 깨는 구문으로 break 한 번에 하나의 반복문을 빠져나올 수 있음
만약 이중 반복문이면 2개의 break를 사용해야함

```python
i=0
while True:
    i+=1
    print(i,end=' ')
    if i>=5:
        break
```
result : 1 2 3 4 5


### 3-2 continue

`continue문`은 반복되는 loop에서 loop는 유지하고 싶지만 특정 경우에서 출력이나 연산을 제어하고 싶을 때 사용하는 구문

```python
i=0
while i<10:
    i+=1
    if i>5:
        continue
    print(i,end=' ')
```
result : 1 2 3 4 5

## 4. 반복문에서의 else

반복문에서도 `else`문을 사용할 수 있는데, if-else문에서의 `else`는 if문의 조건이 만족하지 않을때 실행되었지만, 
반복문에서의 `else`는 반복문이 정상적으로 완료되었을때 실행됨
만약 break를 통하여 반복문을 벗어나는 경우는 `else`문에 들어가지 않고 지나치게 됨

### 4-1 break 사용 시

```python
for i in range(5):
    print(i,end=' ')
    if i==4: break
else:print('끝')
```
result: 0 1 2 3 4  → '끝' 출력이 안됨을 확인할 수 있음(else문 건너뜀)

### 4-1 break 미사용 시

```python
for i in range(5):
    print(i,end=' ')
else:print('끝')
```
result : 0 1 2 3 4 끝  → '끝' 출력됨(else문 동작)

**📌reference**
- [파이썬 코딩 도장](https://dojang.io/course/view.php?id=7)

---
<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```
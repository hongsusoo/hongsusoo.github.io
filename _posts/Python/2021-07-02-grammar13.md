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

title: "13. Python 기초 문법(Python file read/write)"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - Python Basic
tags:
  - 
date: 2021-07-02
last_modified_at: 2021-07-02
---

# Python file read/write

## file write

- open 시 file이 없으면 자동 생성됨
- `file = open('파일명','파일모드')` 형식으로 생성가능
- `'w'`,`'r'`등 여러모드를 사용할 수 있는데, w는 write의 약자, r은 read의 약자
- open후에는 close()로 파일을 닫아줘야함
- 안닫아도 프로그램 종료하며 저절로 종료되지만, write로 열려이는 상황에서 open 하면 error 발생

```python
file = open("hello.txt",'w') #file 생성 및 open, 'w'모드
file.write('hello world') #hello world 입력
file.close()
```
result : <br>
![image](https://user-images.githubusercontent.com/77658029/124107952-b454a200-daa0-11eb-810c-6d73c679b2bf.png)

## file read

- `'r'`모드로 open시 file명 다르면 error 침
- 파일 객체를 read()메소드를 통하여 출력 시킴
- write와 동일하게 file open, close 동작이 필요함

```python
file = open("hello1.txt",'r') #file 생성 및 open, 'r'모드로
s = file.read() #hello world 입력
print(s)
file.close()
```
result : hello world

## with open as 구문(write)

- close를 자동으로 해주는 구문
- `with open('파일명','w') as file객체:`형식으로 사용

```python
with open ('hello2.txt','w') as file:
    for i in range(3):
        file.write('Hello world {0}\n'.format(i))
```
result : <br>
![image](https://user-images.githubusercontent.com/77658029/124109963-ae5fc080-daa2-11eb-836b-1116618b010c.png)

## with open as 구문(read)

- close를 자동으로 해주는 구문
- `with open('파일명','r') as file객체:`형식으로 사용

```python
with open ('hello2.txt','r') as file:
    s=file.read()
    print(s)
```
result : <br>
Hello world 0 <br>
Hello world 1 <br>
Hello world 2

## writelines

- string으로 되어 있는 리스트를 가져와 입력 시켜줌
- 개행문자는 포함되어 있어야함(없을 경우 한줄로 입력됨)
- 한글 입력시에는 `encoding ="utf-8"`입력이 되어 있어야 제대로 입력됨

```python
lines= ['파이썬\n','공부\n','"\n"을 기준으로\n list구분/']
with open ('python.txt','w',encoding ="utf-8") as file:
    file.writelines(lines)
```
result : <br>
![image](https://user-images.githubusercontent.com/77658029/124204756-acd1df00-db1a-11eb-9b4e-98f3e3319482.png)

## readline(s)

- `readlines`는 file에 있는 문자열을 list로 받아옴
- 개행문자 기준으로 요소가 나눠짐
- file의 encoding형태에 따라서 `encoding ="utf-8"`입력이 필요할 수도 있음
- 이전 파일 저장시 `"utf-8"`로 저장하였기 때문에 추가해줘야함
- `\n`기준으로 split되어 list 반환됨

```python
with open ('python.txt','r',encoding ="utf-8") as file:
    l = file.readlines()
    print(l)
```
result : ['파이썬\n', '공부\n', '"\n', '"을 기준으로\n', ' list구분/']

## pickle (객체 저장)

- `pickle`은 파이썬에서 객체를 파일에 저장하는 모듈
- 피클링(pickling) : 파일로 객체를 저장하는 행위
- 언피클링(unpickling) : 객체를 읽어오는 행위
- `dump` 메소드를 이용하여 객체 저장
- `load` 메소드를 이용하여 객체 읽음
- binary 형식으로 파일을 저장함

*객체 저장*
```python
import pickle

name = 'james'
age = 17
address = '서울시 강서구 염창동'
scores = {'kor':90,'eng':95,'math':85,'sci':82}

with open ('james.p','wb') as file:
    pickle.dump(name,file)
    pickle.dump(age,file)
    pickle.dump(address,file)
    pickle.dump(scores,file)
```
result : <br>
![image](https://user-images.githubusercontent.com/77658029/124208019-abf07b80-db21-11eb-8efc-a93d693a6746.png)
↳ binary형태로 저장되어 있어 실제로 알아볼 수 없음

*객체 읽기*
```python
import pickle

with open ('james.p','rb') as file:
    name = pickle.load(file)
    age = pickle.load(file)
    address = pickle.load(file)
    scores = pickle.load(file)
    print(name,age,address,scores,sep='\n')
```
result : <br>
james <br>
17 <br>
서울시 강서구 염창동 <br>
{'kor': 90, 'eng': 95, 'math': 85, 'sci': 82}


<br><br>

**📌reference**
- [파이썬 코딩 도장](https://dojang.io/course/view.php?id=7)

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```
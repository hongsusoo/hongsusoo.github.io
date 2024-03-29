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

title: "05. Python 기초 문법(list, tuple, dictionary )"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - python
tags:
  - 
date: 2021-06-29
last_modified_at: 2021-06-29
---

# 리스트, 튜플, 딕셔너리 

## 리스트 생성

list는 목록이라는 뜻으로 순서에 맞춰 항목을 저장해주는 자료형
python에서의 list는 여러 자료형을 list의 요소로 넣을 수 있다. 

*생성 방법*
1. `listname = [값, 값, 값]`
2. `listname = [] #빈 list`
3. `listname = list() #빈 list`


## 튜플 생성

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


## dictionary 생성

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


**📌reference**
- [파이썬 코딩 도장](https://dojang.io/course/view.php?id=7)

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```
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

title: "06. Python 기초 문법(sequence 자료형(in, index, slicing ...))"
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

# sepuence 자료형

list, tuple, range, string, bytes?, bytesarry?등 자료형은  연속적인 자료로 저장되는데, 이런걸 시퀀스 자료형이라고 함
시퀀스 자료형에서 사용할 수 있는 몇까지 유용한 기능이 있음

## in 연산자(not in)

`a in sepquence자료`으로 사용하여 a가 sequence 내에 있는지 확인하고, 있으면 True 없으면 False로 boolean자료형으로 결과값이 출력됨
`in`과 반대로  `not in` 연산자는 있으면 False, 없으면 True로 출력하게 됨

## 연결하기

객체를 서로 연결하고, 여러개의 시퀀스 자료를 하나의 시퀀스 자료로 구성할 수 있음
주의해야할 사항은 순서가 있기 때문에 더하기에 대해서 교환법칙이 성립하지 않는다. 

*ex)*
a=[1,2,3]
b=[4,5,6]
a+b → [1,2,3,4,5,6]
b+a → [4,5,6,1,2,3]

## 반복하기

\*연산자를 사용하여 시퀀스 객체를 반복한 값을 저장할 수 있음

*ex)*
a=[1,2,3]*3
a=[1,2,3,1,2,3,1,2,3]

## 요소 개수

`len`함수를 이용하여 요소의 개수를 구할 수 있음

*ex)*
1. `len('hello world')` → result : 11
2. `len('hello\' world')` → result : 12

여기서 주의해야할 점은 문자열에서 이스케이프 코드는 1개의 문자로 인식함

## index 사용

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



## slicing

index는 요소 하나씩 접근할 수 있었다면, slicing은 여러 index의 값을 한번에 가져오는 기능
range에서 숫자열을 가져오는 방법과 동일하지만 range는 `,`로 구분되고, slicing은 `:`로 구분됨

*사용방법*
sequence object[시작:끝:간격]

![image](https://user-images.githubusercontent.com/77658029/123734802-faf7a000-d8d8-11eb-9f07-c363b8af3d2a.png)



## 요소 할당(list 자료형)

index으로 우리가 선정한 값을 변수에 값을 넣듯이 값을 대체할 수 있음, list 자료형에서만 사용 가능함
slicing 한 값도 변경 할 수 있음
ex)
```python
a=[1,2,3]
a[0]=3
print(a)
```
result : [3,2,3]

## 요소 삭제(list 자료형, del 함수) 

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



**📌reference**
- [파이썬 코딩 도장](https://dojang.io/course/view.php?id=7)

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```
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

title: "15. Python 기초 문법(변수)"
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

# 변수

- 변수는 크게 전역변수와 지역변수로 나눠짐
- 전역 변수는 함수를 포함한 스크립트 전체에서 접근 가능한 변수
- 전역 변수에 접근할 수 있는 범위를 전역 범위(global scope)라고 함
- 지역 변수는 변수를 만든 함수 안에서 접근 가능함
- 지역 변수에 접근할 수 있는 범위를 지역 범위(local scope)라고 함 

![image](https://user-images.githubusercontent.com/77658029/124450328-45888900-ddbf-11eb-939a-f68de7efdcb5.png)

## global

- 지역 변수를 전역 변수로 바꿔줌
- 전역 변수로 바뀐 변수는 해당 스크립트 전체에서 사용 가능
- 함수가 몇 단계든 상관없이 global 키워드 사용하면 전역 변수를 사용함

![image](https://user-images.githubusercontent.com/77658029/124450933-df503600-ddbf-11eb-91dd-e388bd24992e.png)

```python
x=1
def A(): 
    x=10
    def B(): 
        x=100
        def C(): 
            global x
            print(x)
        C()
    B()
A()
```
result : 1

## nonlocal

- 지역 변수의 scope를 바깥 함수까지 넓혀줌
- nonlocal의 경우 바깥 함수내에 동일한 변수가 있어야함(없으면 error)
- 동일한 변수가 나올때까지 scope를 넓힘

![image](https://user-images.githubusercontent.com/77658029/124486014-1d615000-dde8-11eb-99d5-7e1e2ab5bc3e.png)

```python
def A(): 
    x=1
    def B(): 
        print(x)
        def C(): 
            nonlocal x
            x=3
        C()
        print(x)
    B()
A()
```
result :  <br>
1  <br>
3

**📌reference**
- [파이썬 코딩 도장](https://dojang.io/course/view.php?id=7)

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```
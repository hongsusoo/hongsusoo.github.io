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

title: "22. Python 기초 문법(Iterator와 Generator)"
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

# Python Iterator

- 값을 차례대로 꺼낼 수 있는 객체
- Python에서는 이터레이터만 생성하고 값이 필요한 시점이 되었을 때 값을 만들어 출력
- __지연 평가__ : 데이터 생성을 뒤로 미룸
- **반복자**라고 불림

![image](https://user-images.githubusercontent.com/77658029/124529217-01d86280-de45-11eb-8e9e-707d0d38f790.png)

## __iter__메서드

> dir함수를 통해 반복가능한 객체인지 확인 가능

![image](https://user-images.githubusercontent.com/77658029/124529365-672c5380-de45-11eb-8240-fc356c33b791.png)
<br>
![image](https://user-images.githubusercontent.com/77658029/124529399-7e6b4100-de45-11eb-94c2-aea083cda91c.png)

## __next__메서드

- 다음 항목을 가져오는 메서드
- `__iter__`메소드를 가지고 있는 자료형은 기본적으로 `__next__`메소드를 지원함
- for문에서 in뒤에 오는 자료형이 iterator 자료형임
- 마지막 항목에서 `__next__`호출할 경우 `StopIteration error` 발생

**📰code**
```python
it=[1,2,3].__iter__()
print(it.__next__())
print(it.__next__())
print(it.__next__())
```

**🔍result**
```
1  
2  
3  
```

![image](https://user-images.githubusercontent.com/77658029/124530463-85934e80-de47-11eb-9aa2-08747adf379f.png)

## 이터레이터 언패킹

**📰code**
```python
a,b,c = map(int,['1','2','3'])
print(a,b,c)
```
**🔍result**
```
1 2 3
```
## 이터레이터 만들어 보기(실습)

- `__iter__` : 이터레이터로 사용
- `__next__` : 다음 수 출력
- `__getitem__` : 값 출력

**📰code**
```python
class Counter:
    def __init__(self, stop):
        self.current = 0
        self.stop = stop
    def __iter__(self):
        return self
    def __getitem__(self,index):
        if index < self.stop:
            return index
        else : 
            raise IndexError
    def __next__(self):
        if self.current < self.stop:
            r=self.current
            self.current +=1
            return r
        else:
            raise StopIteration
            
for i in Counter(3):
    print(i,end=' ')
```
**🔍result**
```
0 1 2 
```


## iter와 next함수

- `__iter__()`메소드와 `__next__` 메소드는 함수로도 사용이 가능하다 
- `iter()`, `next()` 형식으로 사용 가능함

### iter()

- 기존 `__iter__` 메서드를 이용한 iterator화와 동일한 방식
- `iter(반복자객체)`형식으로 iterator화 가능함

**📰code**
```python
it = iter(range(10))
it2= range(10).__iter__()
print(type(it))
print(type(it2))
```

**🔍result**
``` 
<class 'range_iterator'>  
<class 'range_iterator'>
```

### next()

- 기존 `__next__` 메서드를 활용하여 다음 숫자를 반환한 방식과 동일한 방식
- `next(반복자객체)`형식으로 다음 숫자 반환함

**📰code**
```python
it = iter(range(10))
print(it.__next__(),end=' ')
print(next(it),end=' ')
print(it.__next__(),end=' ')
print(next(it),end=' ')
```
**🔍result**
```
0 1 2 3
```
<br><br>

# Python generator

- iteratort를 생성해주는 함수
- 함수 내에서 `yield` 키워드를 사용하면 자동으로 Generator로 바뀜
- 제너레이터는 함수 안에서 yield라는 키워드로 iterator의 `__iter__`, `__next__`을 대신함
- 발생자라고 불림

**📰code**
```python
def generator():
    yield 0
g=generator()
print(dir(g))
```
**🔍result**
![image](https://user-images.githubusercontent.com/77658029/124537130-44ee0200-de54-11eb-8745-51fc8b079ef6.png)

## yield

- Iterator의 경우 `__next__` 메서드 안에서 직접 Return으로 반환했지만, 
- Generator의 경우 yield에지정한 값이 `__next__`메서드 반환값으로 나옴
- 마지막에 도달할 경우 iterator는 raise로 예외를 발생시켰지만, generator는 자동으로 발생함
- generator 객체에서 `__next__` 메서드 호출 시 함수 안의 yield에서 값을 발생시킴

![image](https://user-images.githubusercontent.com/77658029/124761611-ef594880-df6c-11eb-84f0-81843b8a76fd.png)

- yield뒤에는 함수도 올수 있다 

**📰code**
```python
def upper_g(x):
    for i in x:
        yield i.upper()
        
alpha = ["a",'b','c','d']
for i in upper_g(alpha):
    print(i, end=' ')
```
**🔍result**
```
A B C D 
```
## yield - from 

- yield from의 경우 뒤에 이터레이터, 제너레이터 객체가 오면 그 요소 개수만큼 전달함

**📰code**
```python
def upper_g():
    yield from ["a",'b','c','d']
        
for i in upper_g():
    print(i, end=' ')
```
**🔍result**
```
a b c d 
```

**📌reference**
- [파이썬 코딩 도장](https://dojang.io/course/view.php?id=7)


```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```
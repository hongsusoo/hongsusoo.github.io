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

title: "10. Python 기초 문법(문자열 함수(replace, translate ...))"
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

# 문자열 응용

## replace(문자열 변경)

- 문자열 내에 부분 문자열을 다른 문자열로 바꿈
- 문자열 자체는 변경하지 않고, 반뀐 결과를 Return 함
- `"문자열".replace('부분문자열','교체문자열)` 형식으로 사용함

```python
s='hello world!'.replace('world','Python')
print(s)
```
result : hello Python!

## translate(문자열 변경)

- translate는 문자열 안의 문자를 다른 문자로 바꿈
- 1차적으로 `table=str.maketrans('바꿀문자','새문자')`형식으로 규칙을 만들어줌
- 그 다음 `'문자열'.translate(table)` 형식으로 사용

```python
table=str.maketrans('abcd','1234')
s='a1b2c3d4'.translate(table)
print(s)
```
result : 11223344

## split

- 문자열을 특정 문자를 기준으로 구분해줌
- default값은 `' '`
```python
'1,2,3'.split(',')
```
result : ['1','2','3']

## join

- 문자열 list를 구분자 문자열과 결합하여 문자열을 만듬

```python
','.join(['1','2','3'])
```
result : '1,2,3'

## 대소문자 변경

- `upper`문자열 내에 소문자를 대문자로 바꿔줌
- `lower`문자열 내에 대문자를 소문자로 바꿔줌

```python
print(f'upper : {"abc가나다".upper()}')
print(f'lower : {"ABC가나다".lower()}')
```
result : <br>
upper : ABC가나다  <br>
lower : abc가나다

## lstrip,rstrip,strip(공백, 특정 문자 삭제)

- `'문자열'.lstrip('삭제할 문자')` 문자열의 왼쪽에 특정 문자 삭제
- `'문자열'.rstrip('삭제할 문자')` 문자열의 오른쪽에 특정 문자 삭제
- `'문자열'.strip('삭제할 문자')` 문자열의 양쪽에 특정 문자 삭제

```python
print(f'lstrip : {",. string ,.".lstrip(",. ")}')
print(f'rstrip : {",. string ,.".rstrip(",. ")}')
print(f'strip : {",. string ,.".strip(",. ")}')
```
result : <br>
lstrip : string ,. <br>
rstrip : ,. string <br>
strip : string

## ljust,rjust,center(정렬)

- 지정한 길이 만큼으로 string을 늘린다음 문자열을 정렬
- `'문자열'.ljust(길이)` 문자열의 왼쪽으로 정렬
- `'문자열'.rjust(길이)` 문자열의 오른쪽으로 정렬
- `'문자열'.center(길이)` 문자열의 센터으로 정렬(자리가 홀수개로 남으면 왼쪽으로 한칸 더 들어감)

```python
print(f'ljust : {"python".ljust(10)}')
print(f'rjust : {"python".rjust(10)}')
print(f'center : {"python".center(10)}')
```
result : <br>
ljust : python     <br>
rjust :     python <br>
center :   python   

## Mathod Chaining(메소드 체이닝)

- `input().split()` 처럼 두개 이상의 mathod를 연결시켜 사용할 있음

## zfill 

- 왼쪽에 0을 채워줌
- 문자열 길이를 맞출때 사용됨

## find, rfind

- 문자열에서 특정 문자열을 찾아 인덱스로 반환
- 문자열이 없으면 -1로 반환
- 문자열에서 찾는 문자열이 여러 개일 경우 처음 찾는 문자열의 인덱스를 반환
- index도 동일한 기능이 있지만, 찾는 문자열이 없을 경우 error 발생
- rfind의 경우 오른쪽부터 문자열을 찾아나감

```python
s='abacd'.find('a')
print(s)
s='abacd'.rfind('a')
print(s)
```
result : <br>
0 <br>
2

## index, rindex

- 문자열에서 특정 문자열을 찾아 인덱스로 반환
- 문자열이 없으면 error 발생
- rindex의 경우 오른쪽부터 문자열을 찾아나감


## count
1
- 문자열에서 특정 문자열이 몇 번 나오는지 확인
- `'문자열'.count('찾을 문자열')`형식으로 사용

```python
'apple pineapple'.count('pl')
```
result : 2

## 서식 지정자

- 문자열 안에서 특정부분을 원하는 변수나 값으로 바꿀때 유용함
- 문자, 정수, 실수를 구분하여 받아야함(다르게 넣을 경우 error 발생)

### 서식 지정자 문자열, 숫자 넣기 

```python
age = 13
print('I am %d' %age)
name = 'haha'
print('I am %s' %name)
print('%s %d' %(name,age))
```
result : <br>
I am 13 <br>
I am haha <br>
haha 13

### 소수점 표현

- `"%.자리수f" % 숫자` 형식으로 사용

```python
print('%.2f' %2.3)
```
result : 2.30

### 오른쪽, 왼쪽 정렬

- `'%길이s' % 'python'` 형식으로 사용

```python
print('%.10s' %'python)
```
result : '    python'

## format

- 서식 지정자와는 다르게 문자,숫자,실수 구분없이 받을 수 있음

### format 사용

![image](https://user-images.githubusercontent.com/77658029/124053293-efcc7d80-da5a-11eb-818b-1404fbdea634.png)
↳ `{인덱스 : [채울문자][정렬방식(<,>)][문자열길이][.자리수][자료형]}.format()`

```python
'Hello, {0} {2} {1}'.format('0','2','1')
```
result : Hello, 0 1 2

- 문자로 대체 가능

```python
'Hello, {language} {version}'.format(language='Python',version=3.6)
```
result : Hello, Python 3.6

- 숫자 개수 맞추기도 가능함

```python
'{0:0.2f} != {1:0.4f}'.format(3.6,3.6)
```

- 정렬도 가능

```python
print('왼쪽정렬 : {0:0<10}'.format(15))
print('오른쪽 정렬 : {0:0>10}'.format(15))
```
result : <br>
왼쪽정렬 : 1500000000 <br>
오른쪽 정렬 : 0000000015

### formatting 줄임표현

- `f'data1 = {data1:[채울문자][정렬방식(<,>)][문자열길이][.자리수][자료형]}'`형식으로 사용 가능함

```python
print(f'왼쪽정렬 : {15:0<10}')
print(f'오른쪽 정렬 : {15:0>10}')
```
result : <br>
왼쪽정렬 : 1500000000 <br>
오른쪽 정렬 : 0000000015

**📌reference**
- [파이썬 코딩 도장](https://dojang.io/course/view.php?id=7)

---
<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```
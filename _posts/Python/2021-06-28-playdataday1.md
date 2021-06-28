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

title: "[playdata_day1] Python 기초"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - py_grammar
tags:
  - [playdata]
date: 2021-06-28
last_modified_at: 2021-06-28
---

# python 기초

## Python 인터프리터 및 컴파일러

<br>

### 1. cmd를 통한 Python file 열기 

<br>

win+R → cmd 실행 → dir 변경(cd 파일 경로) → `python` file명`.py`

![cmd](https://user-images.githubusercontent.com/77658029/123651836-c519d380-d866-11eb-8700-4859877c372e.png)


💨 한 줄씩만 입력이 가능하여 긴 코드 작성이 어려움


<br>

### 2. ipython

ipython은 대화형 프로토콜로 line별로 입력, 출력을 확인할 수 있어 대화하듯 프로그래밍할 수 있도록 도와준다. (jupyter notebook과 동일한 방식)

cmd와 동일하게 directory를 설정
(win+R → cmd 실행 → dir 변경(cd 파일 경로))
→ `ipython` 입력
(ipyhon 종료 방법 : `exit()`+enter)

![ipython](https://user-images.githubusercontent.com/77658029/123652790-93553c80-d867-11eb-87d7-1181ab676ccc.png)

💨 대화형으로 여러 줄의 코드를 연속하여 프로그래밍 할 수 있지만, 기존 data 새롭게 정의에 번거로운 점이 있음

<br>

### 3. jupyter notebook

#### 3.1 실행
cmd와 동일하게 directory를 설정
(win+R → cmd 실행 → dir 변경(cd 파일 경로))
→ `jupyter notebook` 입력

브라우저에서 자동으로 jupyter notebook 실행됨
![image](https://user-images.githubusercontent.com/77658029/123653619-46259a80-d868-11eb-9b8d-9e542a3c4301.png)

만약 닫히거나, 다른 브라우저에서 다시 열고 싶을 경우 하기 이미지의 맨아래 주소를 활용해 브라우저에서 열수 있다.

![jupyter notebook](https://user-images.githubusercontent.com/77658029/123653407-1080b180-d868-11eb-8bba-e51670e5efe9.png)


#### 3.2 활용

##### 3.2.1 block 활용

    - 블럭 선택 : 파란색 표시(단축키 사용가능)

  ![image](https://user-images.githubusercontent.com/77658029/123658305-8e46bc00-d86c-11eb-9b11-f2072aa6832e.png)

    - 블럭 사용 : 초록색 표시(코드 가능)

  ![image](https://user-images.githubusercontent.com/77658029/123658403-a74f6d00-d86c-11eb-8e2e-2322ec9d19f9.png)

  - markdown 형식
    : 블럭 선택 후 `m` 눌러 변경 가능
  - code 형식
    : 블럭 선택 후 `y` 눌러 변경 가능

##### 3.2.1 유용한 기능(tab, 도움말, 매직명령어)

  - tab key : 변수 및 사용할 수 있는 함수나 모듈을 알려줌
  ex) b라는 list와 함께 사용할 수 있는 함수들이 나열되어 선택하서 사용할 수 있도록 도와줌

![image](https://user-images.githubusercontent.com/77658029/123659263-73287c00-d86d-11eb-87cb-f80f1b25a89b.png)


  - 도움말(자기관찰) : 함수명`?`
  함수에 `?`를 붙여 함수나 모듈에 대한 정보를 얻을 수 있음, 물음표 두 개를(`??`) 붙이면 Source 코드까지 확인할 수 있음
  
  ![image](https://user-images.githubusercontent.com/77658029/123659519-be428f00-d86d-11eb-9d6b-9f8ffd8d647d.png)
  
  - 매직명령어
    1. `%quickref` or `%magic` : 여러가지 매직명령어 확인 가능
    2. `%pwd` : 해당 jupyter file의 경로 출력
    3. `%run` : .py 파일 실행 후 결과값 출력
    4. `%load` : .py 파일 불러온 후 %load 부분은 주석 처리

    ![image](https://user-images.githubusercontent.com/77658029/123660543-b8997900-d86e-11eb-89bd-b89e783befb6.png)

💨 cmd와 ipython의 단점을 어느정도 보완한 대화형 프로토콜로 블럭단위로 실행이 가능하여 코드 디버깅에 용이하고, 코드뿐만 아니라 Markdown형태로도 출력이 가능하여 공부나 정리할때 유용한 툴

---
<br>

## Python 기본 문법
---
<br>

### 1. 주석

주석은 프로그래밍시 메모의 목적으로 사용되며, 코드 실행 시 컴파일러나, 인터프리터에 의해 무시되어 프로그램에 영향을 주지 않음

#### Python 주석 종류

1. `# 블럭 주석`(단축키 : *ctrl + /*)
2. `print(10) # Comment 주석`
3. `'''여러줄 주석'''`

![image](https://user-images.githubusercontent.com/77658029/123656324-c5b46900-d86a-11eb-9c48-f052c0acf86a.png)

<br>

### 2. 들여쓰기

다른 언어의 경우 코드를 읽기 쉽도록 간격을 띄워쓰는 용도로 사용되지만, `Python의 경우 들여쓰기 자체가 문법`이기 때문에 조건문, 반복문, 함수, class 생성 등 여러 상황에서 들여쓰기가 잘못되면 error 발생함
(들여쓰기는 Space 4칸이 기준(tab과 동일))

#### error 확인

![image](https://user-images.githubusercontent.com/77658029/123657043-69057e00-d86b-11eb-9cbd-05ff4670e709.png)

![image](https://user-images.githubusercontent.com/77658029/123657318-a5d17500-d86b-11eb-8824-e8bc40231a56.png)


<br>

### 3. 띄어쓰기

Python 언어는 한줄씩 해석하는 언어이다. 모든 함수나 변수 정의할 때는 한 줄에 하나씩 정의해야하며, 만약 한줄에 쓰려고 하면 ;를 사용해 구분해줘야함

![image](https://user-images.githubusercontent.com/77658029/123657600-e630f300-d86b-11eb-90b6-73c9086ad315.png)


```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```
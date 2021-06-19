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

title: "[Angle 가격계산_(1)] Pyqt5 활용 excel 수정 및 저장하기"
excerpt: "about : pyqt5"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - py_proj1
tags:
  - [py_proj1,pyqt5,pandas]
date: 2021-06-19
last_modified_at: 2021-06-19
---


# pyqt5와 Pandas를 활용한 excel 수정

<br>

## 1. 사용한 module 및 Class  
<br>

```python
import sys
import pandas as pd
from PyQt5.QtWidgets import QLabel, QPushButton, QTableWidget,QHeaderView,QHBoxLayout, QVBoxLayout,QWidget, QApplication,QTableWidgetItem
```

|module|class|기능|
|---|---|---|
|Pyqt.QtWidgets|QWidget||
||QApplication|창띄워줄때 사용|
||QHBoxLayout|가로로 Layout 분할하여 배치|
||QVBoxLayout|세로로 Layout 분할하여 배치|
||QLabel|간단하게 글자 남길 수 있음|
||QPushButton|button 생성|
||QTableWidget|Table 생성|
||QHeaderView|Table Header 확인|
||QTableWidgetItem|Table 내용을 채울때 사용|
|pandas|pandas|Data 변경/저장(excel, csv 등)|

---

## 2. class 구성

```python
class MyApp(QWidget):
    def __init__(self): 
    def initUI(self):    # Main Layout 구성
    def read_exl(self):  # Data 불러오기
    def set_exl(self):   # Data 출력
    def add_row(self):   # 맨 아래 행 추가
    def del_row(self):   # 선택 행 삭제
    def save_data(self): # 엑셀로 저장
    def set_label(self, row, column): #마우스로 선택한 cell의 data출력
```
<br>
  
  ### 2-1.  `__init__(self)`

  ```python
  def __init__(self):
    super().__init__()
    self.read_exl()
    self.initUI()
    self.set_exl()
    self.r=0
  ```
  - super() : 처음 `class Myapp`에서 `QWidget`을 상속받아서 사용하는데, `QWidget`의 `__init__()`을 받아서 사용하기 위해 사용
  - self.read_exl() : initUI()라는 처음 Table 구성전에 엑셀을 먼저 읽어와줌
  - self.initUI() : 전체적인 UI 구성을 해줌
  - self.set_exl() : initUI()에서 구성한 Table에 excel data를 입력 시킴
  - self.r=0 : row 추가/제거 시 row 수를 확인하기 위한 변수(class 전체에서 사용됨)
<br>

  ### 2-2.  `initUI(self)`
  ```python
  def initUI(self):
    
    self.tableWidget = QTableWidget()
    self.tableWidget.setRowCount(self.row)
    self.tableWidget.setColumnCount(self.col)

    self.label = QLabel('')
    self.addRow = QPushButton('행추가')
    self.addRow.clicked.connect(self.add_row)
    self.delRow = QPushButton('행삭제')
    self.tableWidget.cellClicked.connect(self.set_label)
    self.delRow.clicked.connect(self.del_row)
    self.save = QPushButton('저장')
    self.save.clicked.connect(self.save_data)

    self.tableWidget.horizontalHeader().setSectionResizeMode(QHeaderView.Stretch)

    hbox = QHBoxLayout()
    hbox.addWidget(self.addRow)
    hbox.addWidget(self.delRow)
    hbox.addWidget(self.save)

    vbox = QVBoxLayout()
    vbox.addWidget(self.tableWidget)
    vbox.addWidget(self.label)

    vbox.addLayout(hbox)
    self.setLayout(vbox)

    self.setWindowTitle('QTableWidget')
    self.setGeometry(300, 100, 1000, 700)
    self.show()
  ```
  - table 사이즈를 `self.row`, `self.col`를 활용하여 맞춰줌
  - label, button의 내용을 구성해줌
  - button의 경우 `clicked` 기능을 이용하여 button 누를 경우 connect 된 함수가 동작하게 만듬
    - 여기서 다른 Mathod에 연결될때 `self.Mathod명`으로 들어가는데 뒤에 ( )가 없다. 그 이유는 정확하게 이해는 못했지만,, 바로 동작하는 경우에는 ( )를 붙여주고 아닌 경우는 빼주고 한다고 한다.
  - QHBoxLayout, QVBoxLayout : horizontal, vertical 방향으로 박스 형태로 Layout을 그려줌
    - 위 code 기준으로 보면, 처음 가로 방향으로 button 3개를 추가 하였고,  이후 Table과 label그리고, 그 가로로 들어간 button 3개(hbox)를 세로로 배치하도록 만들었다.
    ![boxlayout](https://user-images.githubusercontent.com/77658029/122639160-30f79000-d133-11eb-904e-5cc48fc3eb5b.png)

  - setWindowTitle("") : 띄워질 창 위에 써질 문구 입력
  - setGeometry(x,y,size_x,size_y) : window 화면에 띄워질 위치 및 크기 설정
  - show() : 창 띄워줌
<br>

  ### 2-3.  `read_exl(self)`
  ```python
  def read_exl(self): #Data 불러오기
    self.df = pd.read_excel("C:/.../.../~.xlsx",sheet_name = "aa") #불러올 파일 경로 및 이름
    self.df = self.df.dropna()
    self.col = self.df.shape[1]
    self.row = self.df.shape[0]
  ```
  - dropna() : pandas에 있는 함수로 결측값이 있는 행을 삭제함
  - shape[1]은 행의 크기, shape[0]은 열 크기로 각각 col, row변수에 입력시킴
<br>

  ### 2-4.  `set_exl(self)`  
  ```python
  self.tableWidget.setHorizontalHeaderLabels(self.df.columns)
  for i in range(self.row):
      for j in range(self.col):
          if type(self.df.loc[i][j])!=str: 
              temp=str(int(self.df.loc[i][j]))
          else : temp = self.df.loc[i][j]
          self.tableWidget.setItem(i,j,QTableWidgetItem(temp))
  ```
  - table에 header를 excel에서 불러온 열 데이터로 대체함
  - `read_exl` 메소드에서 저장했던 row, col변수 기준으로 table에 data를 채움
  - setItem 함수로 table 각 cell에 접근하여 data입력
<br>

  ### 2-5.  `add_row(self)`    
  ```python
  def add_row(self): #맨 아래 행 추가
    self.row += 1
    self.tableWidget.setRowCount(self.row)
    df2 = pd.DataFrame([['' for _ in range(self.df.shape[1])]],columns=self.df.columns)
    self.df = self.df.append(df2,ignore_index=True)   
  ```
  - 행을 추가하기 위해 row 변수의 값을 1 증가시키고
  - tablewidget의 크기를 재 정의해줌
  - `df2`라는 마지막 행에 대한 정보를 입력해줌(Table widget의 경우 str data만 입력이 가능함)
  - 기존 `df`에 마지막 행을 append하여 추가해줌
<br>

  ### 2-6.  `del_row(self)` 
  ```python
  def del_row(self): #선택 행 삭제
    self.tableWidget.removeRow(self.r)
    self.df.iloc[self.r] = None
    self.df = self.df.dropna()
    self.df.reset_index(inplace=True)
    self.df.drop(["index"],axis=1,inplace=True)
    self.col = self.df.shape[1]
    self.row = self.df.shape[0]
  ``` 
  - tableWidget에 Item 메소드를 이용(아래 `2-6 set_label`에서 선언)하여 클릭한 cell의 row data를 `self.r`변수에 넣어주고, 그 row를 removeRow 메소드를 통하여 Table에서 제거
  - 이후 self.df를 통하여 데이터도 지우는 작업을 실행
    - 해당 행을 nan값으로 바꿔준 후 dropna를 진행, index초기화
<br>

  ### 2-7.  `save_data(self)`  
  ```python
  def save_data(self): #엑셀로 저장       
      for i in range(self.row):
          for j in range(self.col):
              self.df.loc[i][j] = self.tableWidget.item(i,j).text()
      self.df.to_excel("C:/.../.../~.xlsx",sheet_name = "aa",index=False)

  ```
  - 이중 for문을 통해 전체 cell에 접근하여 값을 확인
  - 확인한 값을 df에 update 진행
  - `to_excel` 메소드를 이용하여 원하는 경로 및 파일에 저장
  - `index = False` 로 진행해야 index값
<br>

  ### 2-6.  `set_label(self, row, column)`  
  ```python
  def set_label(self, row, column): 
    item = self.tableWidget.item(row, column)
    try:
        value = item.text()
    except: 
        value = ''
    label_str = 'Row: ' + str(row+1) + ', Column: ' + str(column+1) + ', Value: ' + str(value)
    self.label.setText(label_str)
    self.r=row
  ```
  - 선택한 행,열에 대한 정보와 현재 cell에 입력된 값을 출력해줌
  - 선택한 행에 대한 정보를 self.r에 저장해줌
<br>
## 3. 결과 출력
 ![pyqt5 table excel 변환 저장](https://user-images.githubusercontent.com/77658029/122639123-060d3c00-d133-11eb-8953-4a7121ec1597.gif)

<br>
<br>


```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```
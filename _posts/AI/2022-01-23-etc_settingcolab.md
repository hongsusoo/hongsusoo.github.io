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

title: "Colab Setting 하기"
excerpt: "about : colab"
toc: true
toc_sticky: true
toc_label: "Label"
categories: 
  - AI ETC
tags:
  - [colab]
date: 2022-01-23
last_modified_at: 2022-01-23
---

<br>

# colab

- 구글 Colaboratory 서비스의 줄임말로 주피터 노트북으로 구글 서버를 사용할 수 있음
- 별도의 파이썬 설치 없이 웹 브라우저 만을 이용해 주피터 노트북과 같은 작업 가능함
- 공유가 편리함
- 하지만 지속적으로 연결이 끊겨 처음부터 다시 실행해야하는 불편함이 있음(패키지도 재설치 필요)

## Google Drive 연동하기

- 드라이브 마운트를 통해 본인의 Google Drive와 연동할 수 있음
- 첫 cell에서 아래와 같은 코드를 치고, 왼쪽의 파일모양의 버튼을 찾아 누름
- `content/drive/MyDrive/` 경로로 들어가면 본인의 드라이브를 확인할 수 있음

```python
from google.colab import drive 
drive.mount('/content/drive/')
```
- 현재 위치는 content 폴더에 들어와 있기 때문에, cd 명령어를 통해 본인이 앞으로 사용할 폴더로 이동이 필요함
- `cd drive/MyDrive/Colab\ Notebooks`

## GPU 설정하기

- 런타임 → 런타임 유형 변경 → 하드웨어 가속기 (GPU로 변경) → 저장



## 기타 설정

아기고양이 모드 : 도구 -> 설정 -> 기타 -> 코기 모드 + 아기고양이 모드 설정
파워레벨 모드 : 도구 -> 설정 -> 기타 -> 파워 레벨 설정
<img src="https://user-images.githubusercontent.com/77658029/150667927-6c6eeed2-6a8c-4258-b547-26d0117cb363.gif"  width="70%" height="70%"/>


**📌reference**
- [hongni](https://leti-lee.tistory.com/3)
<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

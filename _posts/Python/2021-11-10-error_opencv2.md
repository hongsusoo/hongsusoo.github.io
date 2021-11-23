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

title: "[import error] import cv2 error"
excerpt: "about : error"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - Python Error
tags:
  - 
date: 2021-11-10
last_modified_at: 2021-11-10
---
<br>

open cv 설치 후 import 시 

`ImportError: libGL.so.1: cannot open shared object file: No such file or directory` 에러 발생시 

리눅스 cli에
`apt-get install libgl1-mesa-glx` 명령어로 해결 가능


[stackoverflow 참고](https://stackoverflow.com/questions/55313610/importerror-libgl-so-1-cannot-open-shared-object-file-no-such-file-or-directo)


<br>
```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

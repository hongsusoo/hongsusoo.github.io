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

title: "16. Python 기초 문법(클로저)"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - Python Basic
tags:
  - 
date: 2021-07-05
last_modified_at: 2021-07-05
---

# 클로저(Closure)

- 함수를 둘러싼 환경(지역변수, 코드 등)을 계속유지하다가 함수를 호출할 때 다시 꺼내서 사용하는 함수를 클로저(closure)라고 함
- return에 내부함수를 넣어 클로저를 만듦
- return에 함수 넣을 때, `()`를 빼고 넣어서 작성함

![image](https://user-images.githubusercontent.com/77658029/124492652-b8115d00-ddef-11eb-861e-682aaeb51c39.png)

```python
def calc():
    a=10
    b=5
    def mul_add(x):
        return a*x+b
    return mul_add

c=calc()
print(c(1),c(3),c(5))
```
result : 15 35 55


<br><br>

**📌reference**
- [파이썬 코딩 도장](https://dojang.io/course/view.php?id=7)


```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```
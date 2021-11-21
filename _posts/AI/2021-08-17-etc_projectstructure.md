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

title: "[PJT-Template] Project Structure Template"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - AI ETC
tags:
  - [project template]
date: 2021-08-17
last_modified_at: 2021-08-17
---

<br>

# Project Structure

- Project를 진행하면 어떻게 구성을 해야할까?

<br>

## project 시작

- Jupyter Notebook을 통한 대화식 개발
- 학습과정과 디버깅 지속적인 확인

**jupyter notebook의 한계**
- 배포 및 공유단계에서는 Notebook 공유가 어려움 → 재현이 어렵고, 실행순서가 꼬임
- DL 코드도 하나의 프로그램이지만 유지보수 및 개발용이성이 떨어짐

<br>

## Project 구조

- 코드도 레고블럭 처럼 → OOP+모듈 = 프로젝트
- 다양한 프로젝트 템플릿 존재
- 사용자 필요에 따라 수정하여 사용
- 실행, 데이터, 모델, 설정, 로깅, 지표, 유틸리티 등 세분화된 모듈로 분리하여 템플릿화가 필요함

![image](https://user-images.githubusercontent.com/77658029/130300539-7309cd89-b0fd-4dc9-878a-f602f2d27dcc.png)

[**🎈추천 Template**](https://github.com/victoresque/pytorch-template)

<br>

**📌reference**
- boostcourse AI tech

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

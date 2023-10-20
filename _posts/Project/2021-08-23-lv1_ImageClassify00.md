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

title: "[CV Project] 마스크 착용 상태 분류 - 시작🌓"
excerpt: "about : Image Classification Competition"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - boostcourse
tags:
  - [CV, Modeling, Pstage-01]
date: 2021-08-23
last_modified_at: 2021-08-23
---

<br>  

# 마스크 착용 상태 분류 대회

1. **목적** : COVID-19 상황에서 사용할 수 있는 Mask 착용 상태 구분 Model 구축

2. **기간** : 21.08.23 ~ 21.09.03

3. **task target** : 주어진 Iamge에 대한 18개 class로 구분

    ※ Mask 착용(정상, 비정상, 미착용), 성별(남, 여), 나이(~30,30~60,60~)

4. **평가 지표** : f1-score

5. **stack** : Python, PyTorch


## Task Description

### Overview

  COVID-19의 확산으로 세계적으로 경제적, 생산적인 활동에 많은 제약이 생겼다. 오랜 기간 동안 우리를 괴롭히고 있는 근본적인 이유는 바로 COVID-19의 강력한 전염력 때문입니다.감염자의 입, 호흡기로부터 나오는 비말, 침 등으로 인해 다른 사람에게 쉽게 전파가 될 수 있기 때문에 감염 확산 방지를 위해 공공 장소에 있는 사람들은 반드시 마스크를 착용해야 할 필요가 있으며, 무엇 보다도 코와 입을 완전히 가릴 수 있도록 올바르게 착용하는 것이 중요합니다. 하지만 넓은 공공장소에서 모든 사람들의 올바른 마스크 착용 상태를 검사하기 위해서는 추가적인 인적자원이 필요할 것입니다.

  따라서, 우리는 카메라로 비춰진 사람 얼굴 이미지 만으로 이 사람이 마스크를 쓰고 있는지, 쓰지 않았는지, 정확히 쓴 것이 맞는지 자동으로 가려낼 수 있는 시스템이 필요합니다. 이 시스템이 공공장소 입구에 갖춰져 있다면 적은 인적자원으로도 충분히 검사가 가능할 것입니다.

## Evaluation Description

- 제출 방식 : 

    - submission.csv 파일은 다음과 같은 포맷으로 구성 되어야 합니다.
    - 각 이미지들에 대해서 mask_class(ans) 를 예측한 값이 콤마(,)로 구분된 형태입니다.
    - 제출 파일은 ImageID,ans 형식으로 헤더를 포함하여야 합니다.

- 평가 방식 : Submission 파일에 대한 평가는 F1 Score 를 통해 진행

![image](https://user-images.githubusercontent.com/77658029/131208502-6fd6b89d-4dd4-498f-9c25-401dfe4ad4dd.png)


<br>

**📌reference**
- boostcourse AI tech


<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

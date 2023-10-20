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

title: "[boostcourse] Day28 학습기록"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - boostcourse
tags:
  - []
date: 2021-09-09
last_modified_at: 2021-09-09
---

## 학습 내용

- semantic segmentation

<br>


## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

모더레이터 : 강재현

참가자 : 박승찬, 한건우, 배지연, 강재현, 오하은, 홍요한

<br>

### 토의 내용

#### CV 과제

- Discussion
    - **want_to_check_heat_map_result** flag를 True로 설정하여 추가로 heatmap을 확인해보세요. 해당 과정을 통해 모델의 출력값을 그대로 시각화할 수 있습니다!
    - Segmentation이라고 했지만, 막상 heatmap에 가깝고 정확하게 Segmentation이 안되는 결과가 나온 것 같습니다. 좀 더 Segmentation 답게 만들기 위해서는 어떤 것들을 추가적으로 해야할지 고민해보시기 바랍니다.
        - 다시 학습시키면 성능이 좋아질 거 같다.
- 피어세션 토론
    - softmax를 사용하는 것의 의미가 무색한거 같다.
        - softmax를 하면 결과적으로 얻어야 하는 것이 class의 확률
        - semantic segmantation도 확률적인 결과를 얻어야 하는지 궁금
        - 신뢰도가 95이상이면 해당 픽셀로 인식하겠다.
            - 80으로 낮추면 인식 영역이 넓어진다.
    - channel을 7개를 사용하는데 7의 의미가 궁금했다.
        - get_class_idx_from_img_name 함수에 나눠져 있다.
        - 픽셀 단위로 classification이 된건가..?
            - 현재 dataset은 사람은 다 똑같은데 마스크 부분만 큰 변화가 있다. 따라서 마스크 부분만 heat map으로 보여주는 거 같다. 즉, 차이만 학습하는 거 같다.
        - 이상한 과제인거 같다.. segmantation으로 학습을 안한거 같다.. classification으로 학습한 듯!
        - FC layer의 weight가 마스크 쓴 사람과 안 쓴 사람을 토대로 학습을 함 → 이 weight만 가져와서 class별로 곱해준 것이기 때문에 실제적으로 classification에서 구분하기 위해서 학습했던 부부분을 visualization으로 보여준 거 같다.
        - 이미지를 직접 처리한 게 아니라 결과값이 7channel이 나오면 그 중 한 channel을 가져와서 heat map으로 만든 뒤 (만들어져 있는 1channel짜리 heat map)을 사용해서 visualization을 한듯

---

Q. 아래 code에서 ToTensor 부분의 순서에 따라 Error 나고 안나고 하는데, 이유가 뭘까요?

```python
transform = transforms.Compose([
    transforms.ToTensor(),
    transforms.GaussianBlur(kernel_size=(9, 9), sigma=(0.1, 3)),
    transforms.Resize((224,224)),
    transforms.Normalize(mean=[0.485, 0.456, 0.406],std=[0.229, 0.224, 0.225])
])
```

A. 기본적으로 PIL이나 opencv같은 이미지는 unsigned int8을 사용합니다. 그래서 Normalize시 연산을 하려면 float으로 형변환이 필요한데 이때 ToTensor가 그 역할을 해주게 됩니다. 그래서 ToTensor가 Normalize 보다 앞에 오는지 뒤에 오는지 따라 에러가 발생합니다

```python
tran = transforms.ToTensor()
tran2 = transforms.GaussianBlur(kernel_size=(9, 9), sigma=(0.1, 3))
tran3 = transforms.Resize((224,224))
tran4 = transforms.Normalize(mean=[0.485, 0.456, 0.406],std=[0.229, 0.224, 0.225])
print(type(tran(train_data[0])))
print(type(tran2(train_data[0])))
print(type(tran3(train_data[0])))
print(type(tran4(train_data[0]))) #여기서 문제가 발생하네요
print(type(tran4(tran(train_data[0])))) 

#위 설명처럼 normalize 하기전에 tensor로 변환해야 할 것같네요
```


### 팀정하기

각자의 약점을 공개해야 한다! → 공개 안하면 복불복...

- 서로 약점 공개함!! (제가 승찬님이 말씀하실 때부터 기록을 시작해서 많이 작성하지 못했네요..ㅠ 추가하고 싶으신 부분 추가해주시면 감사하겠습니당!)

    오하은: 실력 부족 but 기록 잘함. 역할분담을 제대로 해서 깃헙을 통한 협업을 진행하고 싶습니다. 진로는 취직입니다!

    배지연: 컴퓨팅적 지식은 부족하지만 데이터 관련해서 인턴을 해보신 경험이 있다. 

    홍요한: 비전공자서 실력은 부족할 수 있으나 창의적이시다. (아이디어 뱅크!)

    강재현: 깃헙 협업을 잘 하고 싶다.

    한건우: 전기전자 학부 졸업이라 OS관련 지식은 부족할 수 있다. GAN을 현업에서 사용하심. 여러 부트캠프 경험이 있으시며 강사로도 활동해보신 경험이 있다.

    박승찬: GAN annotation사용해봄. 엔지니어로 마음을 잡았다가 1기 선배님들 말씀을 듣고 (기본적인 것을 갖고 어떤 역할을 하는지 고민해보는 것을 좋아함) 리서쳐도 생각 중. 남이 추천하면 잘 하지만 새로운 것을 스스로 시도하는 것은 약간의 시간이 걸린다. CUTMIX를 게시판에 올라온 거 그대로 사용하지 않고 스스로 코드를 구현함. 부스트캠프가 끝난 후 진로: 취직 쪽이지만 대학원도 긍정적

- 부트캠프

    Aiffel은 개발자보다는 리서쳐

    학사로는 취업 적합 X

    현업에서는 리서쳐보다는 배포자를 원함

    네이버는 keyword를 많이 뿌려줘서 전체적인 그림을 파악하고 알아서 공부해보라고 함 → 취업은 이쪽이 더 적합한 거 같다.

Python lightening → 다른 사람이 자신만의 길로 나아가는 것을 방지할 수 있다.


<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

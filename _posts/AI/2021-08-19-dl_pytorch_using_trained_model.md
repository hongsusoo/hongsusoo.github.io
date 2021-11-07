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

title: "Pre-trained model 사용하기"
excerpt: "about : "
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - ai_dlbasic
tags:
  - [pretrained]
date: 2021-08-19
last_modified_at: 2021-08-19
---

<br>  

# pretrained model 사용하기 

<br>

## Transfer learning 

- 다른 데이터셋으로 만든 모델을 현재 데이터에 적용해보는 것
- 일반적으로 대용량 데이터셋으로 만들어진 모델의 성능이 좋음
- 현재의 DL에서는 가장 일반적인 학습기법
- backbone architecture가 잘 학습된 모델에서 일부분만(Freezing) 변경하여 학습을 수행하여 현재 데이터에서도 성능을 끌어올림

![image](https://user-images.githubusercontent.com/77658029/130343239-0122252f-ee37-4b59-832b-00c9bf939f3a.png)

- 새로운 데이터셋으로 새로운 결과를 얻기 위해서 기존 학습데이터는 그대로 두고, 새로운 Layer를 추가/학습하여 원하는 결과를 얻을 수 있음

**📷CV pretrained model**

- [PyTorch image model](https://github.com/rwightman/pytorch-image-models#introduction)

![image](https://user-images.githubusercontent.com/77658029/130318021-e4cb68ae-9c93-4e0a-ac8f-16398fde8eb7.png)


**📞NLP pretrained model**

- [hugging Face](https://huggingface.co/models)
- GPT-3

<br>

## Freezing

- Pretrained model를 활용시 모델의 일부분을 Frozen 시켜서 학습이 필요한 부분만 학습시킴
- 요즘은 freezing하는 layer를 이동/변경하며 training 시키는 stepping froezing도 사용하는 경우가 있음

![image](https://user-images.githubusercontent.com/77658029/130318156-8291eaf5-8d4e-42af-a5f4-39f4ac183877.png)

<br>

## Model 사용

- `import torchvision.models as models`로 models package를 불러옴
- `models`에 있는 pretrained model를 찾아 model를 저장해주면됨
- 새로운 output이 필요하면 목적에 맞게 새로운 layer를 추가해주면됨
- 마지막으로 freezing으로 원하는 layer을 사용할 데이터셋으로 학습시킴
- freezing은 모든 layer를 freezing 한 후 학습이 필요한 layer만 열어서(`param.requires_grad = True`) 학습시킴

**📰code**
```python
class MyNewNet(nn.Module):
    def __init__(self):
        super(MyNewNet, self).__init__()
        self.vgg19 = models.vgg19(pretrained=True)  # models에서 pretrained된 모델들을 가져올 수 있음
        self.linear_layers = nn.Linear(1000, 1) # 우리가 사용할 dataset에 맞게 마지막 Layer를 추가해줌
        
    def forward(self, x):
        x = self.vgg19(x)
        return self.linear_layers(x)
    
for param in my_model.parameters(): #모두 Freezing 시킨 후
    param.requires_grad = False
    
for param in my_model.linear_layers.parameters(): #필요한 부분만 열어줌
    param.requires_grad = True
```

<br>

**📌reference**
- boostcourse AI tech
- [purnasai gudikandula](https://purnasaigudikandula.medium.com/deep-view-on-transfer-learning-with-iamge-classification-pytorch-5cf963939575)

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

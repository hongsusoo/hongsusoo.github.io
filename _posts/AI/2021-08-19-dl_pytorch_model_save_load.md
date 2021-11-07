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

title: "PyTorch Model save & load"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - ai_dlbasic
tags:
  - [PyTorch]
date: 2021-08-19
last_modified_at: 2021-08-19
---

<br>  

# Model 가져오고 공유하기 

- 요즘 ImageNet에서는 이런 이미 학습된 모델을 공유하거나 가져와서 사용하는 문화가 발달했음

<br>

## Model.save()

- 학습의 결과를 저장하기 위한 함수
- 모델 형태(architecture)와 파라미터를 저장할 수 있음
- 모델 학습 중간 과정의 저장을 통해 최선의 결과모델을 선택(early stopping)
- 만들어진 모델을 외부 연구자와 공유하여 학습 재연성 향상
- 저장은 `.pt`형식으로 저장함

<br>

### [save]Model Architecture

- `torch.save()`를 활용해 Model의 architecture와 함께 저장함
- `.pt`형식으로 저장함

**📰code**
```python
torch.save(model, os.path.join(MODEL_PATH, "model.pt"))
```

### [load]Model Architecture 

- `torch.load()`를 활용하여 `.pt`파일을 불러와서 우리가 사용할 model에 저장해줌

**📰code**
```python
model = torch.load(os.path.join(MODEL_PATH, "model.pt"))
```

### [save]Model 파라미터

- `state_dict()`를 활용하면 모델의 Parameter를 가져올 수 있음
- `torch.save()`를 활용하여 `.pt`로 파라미터를 저장함

**📰code**
```python
torch.save(model.state_dict(),os.path.join(MODEL_PATH, "model.pt"))
```

### [load]Model 파라미터

- `load_state_dict()`를 활용하여 저장된 파일에서 parameter를 가져올 수 있음
- `.pt`파일을 load하여 우리가 작성한 model에 load해줌
- 당연히 Model의 형태가 같아야함

**📰code**
```python
new_model = TheModelClass()
new_model.load_state_dict(torch.load(os.path.join(MODEL_PATH, "model.pt")))
```


## Checkpoints

- 학습의 중간결과를 저장하여 최선의 결과를 선택
- early stopping 기법 사용시 이전 학습의 결과물을 저장
- loss와 metric 지속적으로 확인
- 일반적으로 epoch, loss, metric를 함께 저장함
- colab에서 지속적인 학습을 위해 필요

![image](https://user-images.githubusercontent.com/77658029/130316922-71117161-367d-4839-89ef-409074c81435.png)

**📰code**
```python
torch.save({
    'epoch': e,
    'model_state_dict': model.state_dict(),
    'optimizer_state_dict': optimizer.state_dict(),
    'loss': epoch_loss,
    }, f"saved/checkpoint_model_{e}_{epoch_loss/len(dataloader)}_{epoch_acc/len(dataloader)}.pt")
```

**💡 file 명만 봐도 어느 정도의 성능을 파악할수 있게 저장하면 편리함**

<br>

**📌reference**
- boostcourse AI tech
- [PyTorch docs](https://pytorch.org/tutorials/beginner/saving_loading_models.html)

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

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

title: "PyTorch Dataset & DataLoader 기초문법"
excerpt: "about : "
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - DL Basic
tags:
  - [PyTorch]
date: 2021-08-18
last_modified_at: 2021-08-18
---

<br>  

# Dataset & Dataloader

- 모델에 데이터를 feeding을 도와주는 API
- 우리가 사용하는 데이터는 대부분 바로 model에 투입할 수가 없음
- Model로 돌리기 위해서는 몇까지 작업들이 필요함 

    1. Data 전처리
    2. Data to Tensor(Model의 입력이 될수 있도록 tensor로 바꿔줌)
    3. model feeding

- PyTorch에서는 위 작업들을 돕기위해 3가지 package를 제공하고 있음
- Dataset, Transforms, DataLoader
- 만약 라이브러리로 사용하면 import가 필요함 (`from torchvision import datasets`, `import torchvision.transforms as transforms`)

![image](https://user-images.githubusercontent.com/77658029/130314357-f9d8c5e0-7890-4ebb-a41d-8e121516e33c.png)

<br>

## Transforms

- Data를 전처리하고, Model에 입력될 수 있는 형태(ToTensor())로 변경해주는 작업
- data augmentation 등을 진행하는 부분도 Transforms 부분에 해당함
- 최근 huggingFace, TestAI등 표준화된 라이브러리를 많이 사용함
- Dataset을 구성할때 같이 많이 사용되나, 꼭 입력할때 모든 Data를 변경하여 사용하지 않고, 필요한 시점에 변환하여 사용하기도 함
- image data같은 경우는 tensor로 변환하는 작업을 dataset의 init에서 다해줄 경우 memory를 많이 잡아먹고 시간도 오래걸리기 때문에, 
- getitem이후 dataloader에서 tensor로 변환하여 GPU로 feed해주면 loss가 줄어듦
→ (CPU에서는 Tensor로 변환하는 동안 GPU에서는 이전 image를 학습하여 병렬적으로 처리할 수 있음)

※ **huggingFace**는 인기있는 Transforms을 도와주는 라이브러리

<br>

## Dataset

- Data 입력 형태를 정의해주는 클래스
- data 형태에 따라 각 함수를 다르게 정의해줘야함(Image, Text, Audio 등등)
- Dataset은 Map-Style, Iterable-Style
- Map-Style Dataset은 Index존재하는 Data로 3가지의 요소가 갖춰지면 좋음

    1. __init__ : 데이터를 받아서 정리/저장하는 단계
    2. __len__ : 데이터의 길이를 지정하는 단계
    3. __getitem__ : 출력을 어떻게 해줄지를 설정하는 단계, return값으로는 Dict도 좋고, tensor형태로도 많이 사용함

- Iterable-Style Dataset은 Index가 존재하지 않고, data마다 batch size가 달라지는 dynamic batch size에 사용하고 2가지 요소로 이뤄짐

    1. __init__ : 데이터를 받아서 정리/저장하는 단계
    2. __iter__ : 데이터를 iterable하게 가져올 수 있음

- 데이터 셋에 대한 표준화된 처리방법을 제공하게 되면 도움이 많이됨

**Map-style Dataset**

```python
import torch
from torch.utils.data import Dataset
class CustomDataset(Dataset):
    def __init__(self, text, labels): # 초기 데이터 생성방법을 지정
        self.labels = labels
        self.data = text
    
    def __len__(self):  # Data 전체 길이
        return len(self.labels)
    
    def __getitem__(self, idx): # index값에 해당하는 data 출력
        label = self.labels[idx]
        text = self.data[idx]
        sample = {"Text": text, "Class": label}
        return sample # 출력은 dict도 좋고, tesnor 형태로도 많이 사용함
```

<br>

## DataLoader

- data의 batch를 생성해주는 클래스 
- 여러 데이터를 묶어서 model에 feeding 해줌
- 학습직전(GPU feed전) 데이터의 변환을 책임짐
- suffle=True로 해주면 순서를 섞어서 배출해주는데, 중복 없이 반환해줌

**📰code**
```python
import torch
from torch.utils.data import Dataset, DataLoader

class CustomDataset(Dataset):
    def __init__(self, text, labels):
            self.labels = labels
            self.data = text

    def __len__(self):
            return len(self.labels)

    def __getitem__(self, idx):
            label = self.labels[idx]
            text = self.data[idx]
            sample = {"Text": text, "Class": label}
            return sample

text = ['1', '2', '3', '4', '5', '6', '7', '8', '9','10']
labels = ['o','e','o','e','o','e','o','e','o','e']
MyDataset = CustomDataset(text, labels)

MyDataLoader = DataLoader(MyDataset, batch_size=2, shuffle=True)
for dataset in MyDataLoader:
    print(dataset)
```
**🔍result**
```
{'Text': ['10', '4'], 'Class': ['e', 'e']}
{'Text': ['5', '8'], 'Class': ['o', 'e']}
{'Text': ['6', '2'], 'Class': ['e', 'e']}
{'Text': ['9', '1'], 'Class': ['o', 'o']}
{'Text': ['3', '7'], 'Class': ['o', 'o']}
```

<br>

## **💡 DataLoader속 여러 parameter**

![image](https://user-images.githubusercontent.com/77658029/130314961-35034731-fd64-4afc-af92-a1f4515d2fc7.png)

### Dataset 
- 정리한 Dataset Class 입력

### batch_size 
- 데이터셋에서 data를 몇개씩 불러올지 정하는 para, (batch_size, (data.shape))형태의 tensor로 반환(data가 tensor로 입력되어야함)

### suffle 
- Dataset의 데이터를 랜덤하게 가져옴, torch.manual_seed를 활용하면 고정된 data를 출력하여 재현성을 갖게됨

### sampler 
- `torch.utils.data.Sampler` 객체를 활용해서 data index를 조정함, 이 기능을 설정하기 위해서는 suffle=False로 설정 필요함

    - SequentialSampler : 항상 같은 순서
    - RandomSampler : 랜덤, replacemetn 여부 선택 가능, 개수 선택 가능
    - SubsetRandomSampler : 랜덤 리스트, 위와 두 조건 불가능
    - WeigthRandomSampler : 가중치에 따른 확률
    - BatchSampler : batch단위로 sampling 가능
    - DistributedSampler : 분산처리 (torch.nn.parallel.DistributedDataParallel과 함께 사용)
    
### batch_sampler 
- sampler와 동일함

### num_workers 
- subprocess 개수 설정(multiprocessing), 수가 높아지면 CPU와 GPU data처리에 병목현상이 발생하여 적정한 숫자로 설정필요

### collate_fn 
- map-style 데이터셋에서 sample list를 batch 단위로 바꾸는 기능으로 zero-padding이나 Variable Size 데이터 등 데이터 사이즈를 맞추기 위해 많이 사용

### pin_memory 
- GPU(CUDA)에 고정된 메모리를 할당하여 data 처리의 시간 효율을 높이는데 사용됨

### drop_last 
- data숫자가 batch_size로 나눠떨어지지 않으면, 마지막 data가 남게 되는데 그부분을 버려주는 기능

### timeout 
- 기본값은 0이고 0보다 큰 수가 입력되면, data를 불러올때 제한시간을 걸어줌

### worker_init_fn
- num_worker는 갯수로 subprocess를 쓴다고 하면, worker_init_fn은 어떤 worker를 불러올 것인가를 리스트로 입력

<br>

**📌reference**
- boostcourse AI tech
- [Hello Subinium!](https://towardsdatascience.com/linear-regression-with-pytorch-eb6dedead817)


<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

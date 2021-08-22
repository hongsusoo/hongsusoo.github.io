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

title: "[DL Baic] Tensorboard - Monitoring tool for PyTorch"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - AI
tags:
  - [python, AI Tool, PyTorch, Tensorboard, monitoring]
date: 2021-08-19
last_modified_at: 2021-08-19
---

<br>  

# Monitoring Tool for PyTorch

- 학습시간이 오래걸려 기록에 대한 중요성이 높아짐
- 중간과정에서 더 좋은 결과를 얻을 수 있기 때문에 전체적인 흐름을 확인하는 것은 중요함
- 흐름을 확인하는 방법으로는 Print문, log, csv등 여러 방법이 있음
- 좀 더 직관적이고 괜찮은 monitoring tool로 Tensor Board와 WandB를 많이 사용함

<br>

## Tensor Board

- TensorFlow의 프로젝트로 만들어진 시각화 도구
- 학습 그래프, Metric, 학습결과의 시각화 지원
- Tensorflow에서 시작하였지만, PyTorch를 비롯해서 여러 Framwork에서 시각화 하기 위해 사용되고 있음
- DL 시각화의 기본이 되었음

**🎈 여러가지 지표 및 방식으로 표현 할 수 있음**

    - Scalar : 상수값을 표시 (acc, loss)
    - Graph : 모델의 computational graph도 표시
    - histogram : Weight 등 여러 값들의 분포를 표현
    - image : 예측값과 실제값을 비교 표시
    - text : 예측값과 실제값 글자로 비교 표시
    - mesh : 3D 형태의 데이터를 표현 가능

<br>

## Tensor Board 사용해보기

0. Tensorboard 설치하기(!pip install tensorboard)
1. Tensorboard 기록을 위한 directory 생성
2. 기록 생성 객체 SummaryWriter 생성
3. add_scalar 함수를 통해 값을 추가함

💡 아래와 같이 dictionary를 활용하면 한 그래프에 담아서 그릴 수 있음
   
<br>

**📰code - Data 생성**
```python
import os
import numpy as np
from torch.utils.tensorboard import SummaryWriter

logs_base_dir = "logs"
os.makedirs(logs_base_dir, exist_ok=True)

for i in range(1,4):
    exp  = f"{logs_base_dir}/ex{i}"
    writer = SummaryWriter(exp)
    for n_iter in range(100):
        writer.add_scalar('Loss/train', np.random.random(), n_iter)
        writer.add_scalar('Loss/test', np.random.random(), n_iter)
        writer.add_scalar('Accuracy/train', np.random.random(), n_iter)
        writer.add_scalar('Accuracy/test', np.random.random(), n_iter)
    writer.flush()
    
writer = SummaryWriter(logs_base_dir)
r = 5
for i in range(100):
    writer.add_scalars('run_14h', {'xsinx':i*np.sin(i/r),
                                    'xcosx':i*np.cos(i/r),
                                    'tanx': np.tan(i/r)}, i)
```
   
<br>

**🔍result - folder 생성**

logs 폴더에 ex1,2,3 폴더가 생성되고, data값이 피클 값으로 저장되어 있음 

![image](https://user-images.githubusercontent.com/77658029/130323547-feeb42b9-28c0-415b-865b-e4e16c3a3185.png)
   
<br>

**🔍result - Tensorboard으로 확인**

- Magic command를 활용하여 tensorboard extension(`%load_ext tensorboard`)
- Magic command를 활용하여 tensorboard load(`%tensorboard --logdir "logs"`) - logs 디렉토리를 load시켜줌

![image](https://user-images.githubusercontent.com/77658029/130323525-2034672e-9e54-42ba-ae0b-b3cf302ded5f.png)


Scalar 이외에도 다른 여러 그래프를 확인 할 수 있음

![image](https://user-images.githubusercontent.com/77658029/130324943-f96b7612-9e81-4571-a18b-21fb641fa787.png)

<br>


## 실습예제

<br>

### **📰code - Package, library import**
```python
import matplotlib.pyplot as plt
import numpy as np

import torch
import torchvision
import torchvision.transforms as transforms

import torch.nn as nn
import torch.nn.functional as F
import torch.optim as optim
```

<br>

### **📰code - Dataset 불러오기**
```python
# transforms
transform = transforms.Compose(
    [transforms.ToTensor(),
    transforms.Normalize((0.5,), (0.5,))])

# datasets
trainset = torchvision.datasets.FashionMNIST('./data',
    download=True,
    train=True,
    transform=transform)
testset = torchvision.datasets.FashionMNIST('./data',
    download=True,
    train=False,
    transform=transform)

# dataloaders
trainloader = torch.utils.data.DataLoader(trainset, batch_size=4,
                                        shuffle=True, num_workers=2)


testloader = torch.utils.data.DataLoader(testset, batch_size=4,
                                        shuffle=False, num_workers=2)

# constant for classes
classes = ('T-shirt/top', 'Trouser', 'Pullover', 'Dress', 'Coat',
        'Sandal', 'Shirt', 'Sneaker', 'Bag', 'Ankle Boot')
```

<br>

### **📰code - Network 구성, Loss 정의, Optimizer 정의**
```python
class Net(nn.Module):
    def __init__(self):
        super(Net, self).__init__()
        self.conv1 = nn.Conv2d(1, 6, 5)
        self.pool = nn.MaxPool2d(2, 2)
        self.conv2 = nn.Conv2d(6, 16, 5)
        self.fc1 = nn.Linear(16 * 4 * 4, 120)
        self.fc2 = nn.Linear(120, 84)
        self.fc3 = nn.Linear(84, 10)

    def forward(self, x):
        x = self.pool(F.relu(self.conv1(x)))
        x = self.pool(F.relu(self.conv2(x)))
        x = x.view(-1, 16 * 4 * 4)
        x = F.relu(self.fc1(x))
        x = F.relu(self.fc2(x))
        x = self.fc3(x)
        return x

net = Net()
criterion = nn.CrossEntropyLoss()
optimizer = optim.SGD(net.parameters(), lr=0.001, momentum=0.9)
```

<br>

### **📰code - Tensorboard 사용을 위한 directory 정의**
```python
from torch.utils.tensorboard import SummaryWriter

# default `log_dir` is "runs" - we'll be more specific here
writer = SummaryWriter('app/fashion_mnist_experiment_1')
```

<br>

### **📰code - Tensorboard에 graph 및 image 표현**
```python
# get some random training images
dataiter = iter(trainloader)
images, labels = dataiter.next()

# create grid of images
img_grid = torchvision.utils.make_grid(images)
print(img_grid.shape)

# show images
matplotlib_imshow(img_grid, one_channel=True)

# write to tensorboard
writer.add_image('four_fashion_mnist_images', img_grid)

writer.add_graph(net, images)
writer.close()
```

<br>

### **🔍result network graph**
![image](https://user-images.githubusercontent.com/77658029/130340692-cce073a0-5026-4077-82f7-65702484db27.png)

<br>

### **📰code - Tensorboard에 projector 표현**
```python
# helper function
def select_n_random(data, labels, n=100):
    '''
    Selects n random datapoints and their corresponding labels from a dataset
    '''
    assert len(data) == len(labels)

    perm = torch.randperm(len(data))
    return data[perm][:n], labels[perm][:n]

# select random images and their target indices
images, labels = select_n_random(trainset.data, trainset.targets)

# get the class labels for each image
class_labels = [classes[lab] for lab in labels]

# log embeddings
features = images.view(-1, 28 * 28)
writer.add_embedding(features,
                    metadata=class_labels,
                    label_img=images.unsqueeze(1))
writer.close()
```

<br>

### **🔍result projector**
![Animation](https://user-images.githubusercontent.com/77658029/130340577-6a5435e9-8792-4316-9dc9-ed570d1caaa1.gif)

<br>


### **📰code - training**
```python
running_loss = 0.0
for epoch in range(2):  # loop over the dataset multiple times
    print(epoch)
    for i, data in enumerate(trainloader, 0):

        # get the inputs; data is a list of [inputs, labels]
        inputs, labels = data

        # zero the parameter gradients
        optimizer.zero_grad()

        # forward + backward + optimize
        outputs = net(inputs)
        loss = criterion(outputs, labels)
        loss.backward()
        optimizer.step()

        running_loss += loss.item()
        if i % 1000 == 999:    # every 1000 mini-batches...

            # ...log the running loss
            writer.add_scalar('training loss',
                            running_loss / 1000,
                            epoch * len(trainloader) + i)

            # ...log a Matplotlib Figure showing the model's predictions on a
            # random mini-batch
            writer.add_figure('predictions vs. actuals',
                            plot_classes_preds(net, inputs, labels),
                            global_step=epoch * len(trainloader) + i)
            running_loss = 0.0
print('Finished Training')
```

<br>

### **🔍result training loss**

![image](https://user-images.githubusercontent.com/77658029/130340668-9f21e825-5c58-4762-b5d8-c16c1be4e718.png)

<br>

### **📰code - tensorboard pr curve 표현**
```python
# 1. gets the probability predictions in a test_size x num_classes Tensor
# 2. gets the preds in a test_size Tensor
# takes ~10 seconds to run
class_probs = []
class_label = []
with torch.no_grad():
    for data in testloader:
        images, labels = data
        output = net(images)
        class_probs_batch = [F.softmax(el, dim=0) for el in output]

        class_probs.append(class_probs_batch)
        class_label.append(labels)

test_probs = torch.cat([torch.stack(batch) for batch in class_probs])
test_label = torch.cat(class_label)

# helper function
def add_pr_curve_tensorboard(class_index, test_probs, test_label, global_step=0):
    '''
    Takes in a "class_index" from 0 to 9 and plots the corresponding
    precision-recall curve
    '''
    tensorboard_truth = test_label == class_index
    tensorboard_probs = test_probs[:, class_index]

    writer.add_pr_curve(classes[class_index],
                        tensorboard_truth,
                        tensorboard_probs,
                        global_step=global_step)
    writer.close()

# plot all the pr curves
for i in range(len(classes)):
    add_pr_curve_tensorboard(i, test_probs, test_label)
```

<br>

### **🔍result pr curve** 

![image](https://user-images.githubusercontent.com/77658029/130340654-58c52bf4-5524-493f-a6cc-51dd3918570e.png)

<br>

**📌reference**
- boostcourse AI tech
- [pytorch](https://pytorch.org/tutorials/recipes/recipes/tensorboard_with_pytorch.html)

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

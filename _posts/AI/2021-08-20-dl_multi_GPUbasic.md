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

title: "Multi GPU"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - ai_dlbasic
tags:
  - [PyTorch, Multi GPU]
date: 2021-08-20
last_modified_at: 2021-08-20
---

<br>  

# Multi GPU

- 예전에는 어떻게 하면 GPU를 적게 쓸까?
- 지금은 GPU를 많이 사용하여 성능좋은 모델을 만들자!
- 오늘날의 딥러닝은 엄청난 데이터와의 싸움(GPT-3 $10^11$ 데이터를 사용)
- 연구는 장비빨...

<br>

## 기본 개념 정리 

- single GPU : GPU 1개
- Multi GPU : GPU 2개 이상
- Node는 1대의 컴퓨터를 의미함
- Single Node Single GPU - 1대의 컴퓨터에 GPU 1개
- Single Node Multi GPU(4~8개?) - 1대의 컴퓨터에 2개 이상의 GPU
- Multi Node Multi GPU(server) - 여러대의 컴퓨터에 여러개의 GPU

<br>

## Multi GPU 사용 방법

<br>

### 1. Model Parallel

- 모델을 GPU에 따로 나눠서 돌리는 것
- 예전부터 많이 사용했던 방식 (Alexnet에 사용)
- 사실 모델의 병목현상과 파이프라인의 어려움으로, 모델 병렬화는 고난이도 과제
- 프로세스
    1. Model1,2를 각각 GPU1,2에 넣어줌
    2. network 학습 -> 중간에 데이터를 다른 GPU로 넘겨주며 병목현상 발생
    3. 마지막 결과를 GPU하나로 모아서 Loss or 결과 출력

![image](https://user-images.githubusercontent.com/77658029/130342072-623f3f65-e429-4b22-80fb-4ca2adfc03ad.png)

- 동일한 데이터를 모델을 둘로 나눠 Multi GPU를 사용함

**📰code**
```python
class ModelParallelResNet50(ResNet):
    def __init__(self, *args, **kwargs):
        super(ModelParallelResNet50, self).__init__(
        Bottleneck, [3, 4, 6, 3], num_classes=num_classes, *args, **kwargs)
        self.seq1 = nn.Sequential(self.conv1, self.bn1, self.relu, self.maxpool, self.layer1, self.layer2).to('cuda:0')# GPU1
        self.seq2 = nn.Sequential(self.layer3, self.layer4, self.avgpool).to('cuda:1') #GPU2
        self.fc.to('cuda:1') #GPU2
        
    def forward(self, x):
        x = self.seq2(self.seq1(x).to('cuda:1')) #GPU로 합쳐서 마지막 작업 진행
        return self.fc(x.view(x.size(0), -1))
```

<br>

### 2. Data Parallel

- 데이터를 Batch로 나눠서 Loss의 Gradient를 구하고 결과값의 평균으로 답을 얻음
- Minibatch와 비슷한 방식
- 프로세스
    1. GPU에 동일한 모델을 복사해서 넣어줌
    2. Data를 나눠서 각각 GPU에 Input
    3. Layer연산
    4. 연산한 값을 GPU하나로 모아서 평균을 냄 -> 한 GPU에 연산이 몰려 병목현상 발생

![image](https://user-images.githubusercontent.com/77658029/130342446-bcf2c123-44c3-445d-9c9f-4ccdc94f9962.png)

- `torch.nn.DataParallel(model)`만 추가하면 Data parallel 사용가능함

**📰code**
```python
parallel_model = torch.nn.DataParallel(model) # Encapsulate the model 

predictions = parallel_model(inputs) # Forward pass on multi-GPUs
loss = loss_function(predictions, labels) # Compute loss function
loss.mean().backward() # Average GPU-losses + backward pass
optimizer.step() # Optimizer step
predictions = parallel_model(inputs) # Forward pass with new parameters
```

<br>

### 3. DistributedDataParallel

- 각 CPU 마다 Process를 생성하여 개별 GPU에 할당 -> 기본적으로 Data parallel로 하나 개별적으로 연산의 평균을 냄
- CPU개수랑 GPU개수를 동일하게 만들어서 진행함
- Dataparallel은 Layer마다 값을 모아주고 펼쳐주는 작업이 있어지만,
- DistributedDataParallel는 연산이 끝나고 결과값만 합쳐주기 때문에 병목현상에서 좀 더 자유로옴
- DistributedDataParallel의 경우는 Multiprocessing 기법이 필요함, web 처럼 통신규약 통해서 진행되게됨

**📰code**
```python
train_sampler = torch.utils.data.distributed.DistributedSampler(train_data)
shuffle = False
pin_memory = True
trainloader = torch.utils.data.DataLoader(train_data, batch_size=20, shuffle=shuffle, pin_memory=pin_memory, num_workers=3,
shuffle=shuffle, sampler=train_sampler)


def main():
    n_gpus = torch.cuda.device_count()
    torch.multiprocessing.spawn(main_worker, nprocs=n_gpus, args=(n_gpus, ))
    
def main_worker(gpu, n_gpus):
    image_size = 224
    batch_size = 512
    num_worker = 8
    epochs = 100
    batch_size = int(batch_size / n_gpus)
    num_worker = int(num_worker / n_gpus)
    torch.distributed.init_process_group(
    backend='nccl’, init_method='tcp://127.0.0.1:2568’, world_size=n_gpus, rank=gpu) #Multiprocessing 통신 규약
    model = MODEL
    torch.cuda.set_device(gpu)
    model = model.cuda(gpu)
    model = torch.nn.parallel.DistributedDataParallel(model, device_ids=[gpu]) # DistributedDataParallel 정의
```

<br>

**📌reference**
- boostcourse AI tech
- [SIA](https://blog.si-analytics.ai/12)

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

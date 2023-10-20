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

title: "HyperParameter Tuning - Ray"
excerpt: "about : "
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - Visualization
tags:
  - [PyTorch, hyperparameter, Multi GPU]
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

- 데이터를 Batch로 나눠서 L# Hyperparameter Tuning

- 모델 학습을 할 때 사람이 정해줘야하는 몇까지 parameter들을 Hyperparameter라고 부름
- 학습률(Learning_Rate), Activation Function 등
- 성능을 높이기 위해서 크게 3가지 방법을 사용함(제일 효과가 큰 건 Data)

    1. 모델을 바꿔본다 -> 거의 고정되어 있음(CV : Resnet, CNN 계열, ViT /NLP : transformer)
    2. 데이터 추가 or 이상 데이터 -> 제일 중요함, 제일 많이 바꿈
    3. Hyperparameter Tuning -> 마른 수건도 짜보는 느낌

-> 모델 스스로 학습하지 않는 값은 사람이 지정(learning rate(NAS), 모델의 크기, Optimizer 등등)
- 예전에는 Hyperparameter에 따라서 결과가 크게 좌우됨(요즘은 차이가 크지 않음, why? 데이터를 훨씬 많이 사용하기 때문)
- 마지막 성능을 0.01, 0.001 쥐어짜야할때 시도..

<br>

## Hyperparameter를 찾는 방법

<br>

### Grid Search

- 몇개의 Hyperparameter를 특정 범위에서 변동 시키며 확인하는 방법
- 일정한 간격(log scale)으로 Grid를 만들어 최적의 hyperparameter를 찾음

![image](https://user-images.githubusercontent.com/77658029/130343528-a65de0dc-d8fa-4b6e-b665-034e9182325a.png)

<br>

### random Search

- Hyperparameter를 랜덤으로 선택하여 최적의 hyperparameter를 찾음

![image](https://user-images.githubusercontent.com/77658029/130343555-82ca4ab9-8278-467e-b679-152666b5340a.png)

<br>

### BOHB(2018)

- 베이지안 기반 기법으로 요즘 유행함
- [참고자료](http://proceedings.mlr.press/v80/falkner18a/falkner18a.pdf)

<br>

## Ray

- Multi-node Multi processing 지원 모듈
- ML/DL의 병렬 처리를 위한 개발된 모듈
- 요즘의 Python 병렬처리는 Ray가 거의 표준
- Hyperparameter Search를 위한 다양한 모듈 제공
- SPARK를 만든 연구실, 요즘은 Ray에 집중하고 있다고 함

💡 SPARK(데이터를 병렬처리하는 모듈, 하둡의 기능을 뛰어넘음) 

- ray를 활용하기 위해서는 기본적으로 4가지를 만들어줘야함

    1. 탐색할 Hyperparameter별 범위 설정(search space 지정) - dictionary형태로
    2. 어떻게 학습할지 학습 알고리즘 설정
    3. 결과를 출력 양식 설정
    4. 위 3가지를 모아서 result로 하나로 묶어주는 작업


**📰code**
```python
data_dir = os.path.abspath("./data")
load_data(data_dir)

config = {
    "l1": tune.sample_from(lambda _: 2 ** np.random.randint(2, 9)),
    "l2": tune.sample_from(lambda _: 2 ** np.random.randint(2, 9)),
    "lr": tune.loguniform(1e-4, 1e-1),
    "batch_size": tune.choice([2, 4, 8, 16])
}

scheduler = ASHAScheduler(metric="loss", mode="min", max_t=max_num_epochs, grace_period=1,reduction_factor=2)

reporter = CLIReporter(metric_columns=["loss", "accuracy", "training_iteration"])

result = tune.run(
    partial(train_cifar, data_dir=data_dir),
    resources_per_trial={"cpu": 2, "gpu": gpus_per_trial},
    config=config, num_samples=num_samples,
    scheduler=scheduler,
    progress_reporter=reporter
)
```

<br>

**📌reference**
- boostcourse AI tech
- [Random Search for Hyper-Parameter Optimization](https://dl.acm.org/doi/pdf/10.5555/2188385.2188395)

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

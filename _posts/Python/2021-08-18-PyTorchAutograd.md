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

title: "[DL Baic] PyTorch nn.Module(Autograd & Optimizer)"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - AI
tags:
  - [python, AI Tool, PyTorch, nn.Module]
date: 2021-08-18
last_modified_at: 2021-08-18
---

<br>  

# Autograd & Optimizer

<br>

## Torch.nn.Module

- 딥러닝을 구성하는 layer의 base class
- input, output, forward, backward(autograd,weight)
- 학습이 대상이 되는 parameter(tensor) 정의

![image](https://user-images.githubusercontent.com/77658029/129821395-4f9db686-a2a6-401e-a36d-41e80008047c.png)

<br>

### nn.Module의 구조

- __init__ : 각종 parameter들 정의
- forward : Network에 입력을 넣어 output을 뽑아냄
- sigmoid : activation function, 다른 함수도 구현해서 사용 가능함
- backward : forward에서 진행한 식에 대해 gradient값을 구함(weight, bias에 관해서)
- optimizer : backward에서 계산한 값을 Network에 업데이트 시켜줌(weight, bias를 업데이트함)


```python
class Example(nn.Module):
    def __init__(self, dim, lr=torch.scalar_tensor(0.01)): #dim = (inputsize,outputsize) - weight에 들어갈 
        super(Template, self).__init__()
        # intialize parameters
        self.W = torch.zeros(dim, 1, dtype=torch.float)
        self.b = torch.scalar_tensor(0)
        self.grads = {"dW": torch.zeros(dim, 1, dtype=torch.float), "db": torch.scalar_tensor(0)}
        self.lr = lr
        
    def forward(self, x):
        ## compute forward
        linear = torch.addmm(self.b, x, self.w)
        output = self.sigmoid(linear)
        return output
        
    def sigmoid(self, z):
        return 1/(1 + torch.exp(-z))
    
    def backward(self, x, yhat, y):
        ## compute backward
        self.grads["dw"] = (1/x.shape[1]) * torch.mm(x, (yhat - y).T) #gradient 계산
        self.grads["db"] = (1/x.shape[1]) * torch.sum(yhat - y) #gradient 계산
        
    def optimize(self):
        ## optimization step
        self.w = self.w - self.lr * self.grads["dw"] #gradient update
        self.b = self.b - self.lr * self.grads["db"] #gradient update
```



<br>

## Foward와 parameter

- Tensor 객체의 상속 객체 
- nn.Module내에 attribute가 될 때는 required_grad = True로 지정되어 학습 대상이 되는 Tensor
- required_grad = True가 되어 있어야 Autograd가 진행이됨
- Linear, conv 등의 layer들에 이미 parameter(weight)가 지정되어 있기 때문에 직접 지정할 일은 많지 않음
- 아래와 `nn.parameter`를 활용하여 weight를 구성한 이후 인스턴스를 동작시키게 되면 forwardpass이 일어나게 된다

**📰code**
```python
import torch
from torch import nn
from torch import Tensor

class MyLinear(nn.Module):
    def __init__(self, in_features, out_features, bias=True):
        super().__init__()
        self.in_features = in_features
        self.out_features = out_features
        
        self.weights = nn.Parameter(torch.randn(in_features, out_features))
        self.bias = nn.Parameter(torch.randn(out_features))

    def forward(self, x : Tensor):
        return x @ self.weights + self.bias
    
x = torch.randn(5, 7) # batch 5, input dim 7
print(x)
layer = MyLinear(7, 12) # input 7, output 12
print(layer(x).shape) # batch 5, output dim 12
```
**🔍result**
```
tensor([[ 0.4152,  2.4837,  0.7766, -1.4975, -0.6413, -0.0836,  1.0998],
        [ 2.0921,  0.6759, -0.5452, -1.0992, -0.3953, -0.2154,  0.6453],
        [-0.3645, -0.1517, -0.0193, -1.8220,  1.7140, -1.0767, -0.5035],
        [-0.6115,  2.9012, -1.4191, -1.2334, -1.2555, -0.4280, -1.7653],
        [ 0.1985, -1.1522,  0.2816,  0.9674, -0.0682,  0.9396, -0.7299]])
torch.Size([5, 12])
```

- 위 코드에서 MyLinear의 객체인 layer의 parameter을 확인 할 수 있다
- `layer.parameters()`형식으로 뽑으면 generator 객체로 뽑하기 때문에 for문을 사용해서 출력해 줄 수 있다
- 위 코드에서 parameter는 weight와 bias 두 종류가 있기 때문에, 출력 또한 2개의 paramter를 확인할 수 있다

**📰code**
```python
for i,weight in enumerate(layer.parameters()):
    print(i)
    print(weight)
```
**🔍result**
```
0
Parameter containing:
tensor([[-0.9773, -0.8269, -1.3366,  0.3635,  1.2686,  0.6571, -1.0801, -0.0366,
         -1.1278, -1.1030, -0.3572,  0.6733],
        [ 1.4786,  0.8860,  2.9108,  1.1033, -0.1592,  0.4273,  1.9332, -0.5062,
         -1.1353,  0.5759,  0.3554,  0.9182],
        [-1.5364,  0.6698, -1.4138, -1.1673, -0.6144, -0.2622,  0.1079,  1.5369,
         -0.7240, -0.9971,  1.1517, -0.3620],
        [ 0.3360, -0.8670, -1.4483, -0.1183,  0.4558,  0.0648, -1.7267, -1.2206,
         -0.9050,  1.2235, -1.2723, -0.6792],
        [-0.0449, -0.5937, -0.0282,  0.0487,  1.5190, -1.9477, -1.9266, -0.5821,
          0.1365, -0.9889, -0.5429,  0.0134],
        [ 0.2352,  0.3291, -0.8454,  0.5034, -1.3333, -2.3747,  0.1558,  1.0028,
         -0.1426,  1.7190,  0.3017, -0.3314],
        [-0.3310,  0.4655, -0.3544, -1.0033, -0.8208, -0.4913,  0.7759, -1.9471,
         -0.6976,  0.4412, -1.0636, -0.0432]], requires_grad=True)
1
Parameter containing:
tensor([-1.3176,  1.0029,  0.7482, -2.1537,  0.8717, -1.0003, -0.2203,  0.4989,
        -0.7009,  1.0871,  1.2747, -1.3107], requires_grad=True)
```


<br>

## Backward

- forward를 통해 만들어진 parameter들로 output(예측치)를 뽑아내는데, 이때의 예측치와 실제값간의 차이(loss)에 대해 미분 수행
- loss를 최소화 하는 방향으로 paratmeter를 업데이트 시켜줌

- 대부분 epoch마다 backward를 진행시켜줌
- backward에서는 크게 4가지 부분에 대해서 필수적으로 진행해야하는 대상

    1. optimizer.zero_grad() : 이전 미분한 gradient 값이 영향을 주지 않도록 초기화 시켜주는 작업
    2. loss 지정 : model의 예측에 기여하는 loss를 설정하여 정의해줘야함
    3. loss.backward() : loss에 대한 미분값을 계산하는 단계
    4. optimizer.step() : backward에서 계산한 미분값을 parameter에 적용시켜주는 단계
    
- 실제 Backward는 module 단계에서 직접 지정가능함
- Module에서 backward와 optimizer를 오버라이딩 했기 때문에 autograd가 가능함
- 만약 직접 지정한다고 하면, 직접 여러 layer에 대한 미분을 진행야함


**📰code**
```python
import numpy as np
import torch
from torch import nn
from torch import Tensor
from torch.autograd import Variable

class LinearRegression(torch.nn.Module):
    def __init__(self, inputSize, outputSize):
        super(LinearRegression,self).__init__()
        self.linear = torch.nn.Linear(inputSize,outputSize)
        
    def forward(self,x):
        out = self.linear(x)
        return out

# create dummy data for training
x_values = [i for i in range(11)]
x_train = np.array(x_values, dtype=np.float32)
x_train = x_train.reshape(-1, 1)

y_values = [2*i + 1 for i in x_values]
y_train = np.array(y_values, dtype=np.float32)
y_train = y_train.reshape(-1, 1)

inputDim = 1
outputDim = 1
learningRate = 0.01 
epochs = 100

model = LinearRegression(inputDim, outputDim)

criterion = torch.nn.MSELoss() 
optimizer = torch.optim.SGD(model.parameters(), lr=learningRate) 

for epoch in range(epochs):
    inputs = Variable(torch.from_numpy(x_train))
    labels = Variable(torch.from_numpy(y_train))

    optimizer.zero_grad()
    
    outputs = model(inputs)
    loss = criterion(outputs, labels)
    loss.backward()
    optimizer.step()

#     print('epoch {}, loss {}'.format(epoch, loss.item()))
    
with torch.no_grad():
    predicted = model(Variable(torch.from_numpy(x_train))).data.numpy()

for train, pred in zip(y_train,predicted):
    print(train,pred)
```
**🔍result**
```
[1.] [1.145034]
[3.] [3.124148]
[5.] [5.1032615]
[7.] [7.0823755]
[9.] [9.061489]
[11.] [11.040603]
[13.] [13.019717]
[15.] [14.998831]
[17.] [16.977945]
[19.] [18.95706]
[21.] [20.936172]
```

- 실제 backward는 Module 단계에서 직접 지정하여 진행할 수 있지만,
- 직접 backward, optimizer 함수를 오버라이딩 해서 직접 coding해줘야함


<br>

**📌reference**
- boostcourse AI tech
- [toward data science](https://subinium.github.io/pytorch-dataloader/)

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

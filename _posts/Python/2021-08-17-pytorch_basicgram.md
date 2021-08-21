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

title: "[DL Basic] PyTorch 기초 문법"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - AI
tags:
  - [python, AI Tool, PyTorch]
date: 2021-08-17
last_modified_at: 2021-08-17
---

<br>

# PyTorch Basic grammar

## PyTorch Operations

- Tensor는 PyTorch에서 다차원 Arrays를 표현하는 PyTorch의 클래스
- Tensor는 Numpy에 ndarray와 동일함(TF에서의 Tensor도 동일함)
- Numpy와 함수구성이 거의 동일함
- Tensor 생성은 list도 가능함

<br>

**📌 Numpy 기능**

1. Data Slicing
2. `tensor_1.flatten()` : 1차원으로 펴줌
3. `torch.ones_like(tensor_1)` : tensor_1과 동일한 차원에 원소는 모두 1인 Tensor 생성
4. `tensor_1.numpy()` : tensor를 numpy로 바꿔줌
5. `tensor_1.shape` : 현재 Tensor의 shape을 출력함
6. `tensor_1.dtype` : 현재 Tensor의 data type을 출력함
7. 사칙연산 : 동일 차원 Tensor사이의 사칙연산 및 scalar 연산 가능함, (내적, dot연산은 다름)


<br>

### numpy to Tensor

**📰code**
```python
import numpy as np
import torch

n_array = np.arange(10).reshape(2,5)

print("numpy :")
print(n_array)
print("ndim :", n_array.ndim, "shape :", n_array.shape)
print()
t_array = torch.FloatTensor(n_array)
print("Tensor :")
print(t_array)
print("ndim :", t_array.ndim, "shape :", t_array.shape)
```
**🔍result**
```
numpy :
[[0 1 2 3 4]
 [5 6 7 8 9]]
ndim : 2 shape : (2, 5)

Tensor :
tensor([[0., 1., 2., 3., 4.],
        [5., 6., 7., 8., 9.]])
ndim : 2 shape : torch.Size([2, 5])
```

<br>

### CUDA

- Numpy와 가장 큰 차이점으로 Tensor는 GPU를 사용할 수 있음
- `tensor명.device` 형식으로 현재 Tensor의 데이터가 GPU 메모리상에 있는지 CPU에 있는지 확인할 수 있음

**📰code**
```python
import numpy as np
import torch

n_array = np.arange(10).reshape(2,5)
t_array = torch.FloatTensor(n_array)
t_array.device

# if torch.cuda.is_available(): #GPU가 있으면 GPU에 넣어줌
#     t_array_cuda = t_array.to('cuda')
#     t_array_cuda.device
```
**🔍result**
```
device(type='cpu')
```

<br>


### Stride와 contiguous

- Tensor의 경우 stride 폭을 이용해서 차원을 건너뛰며 접근함
- 만약 [2,3,3] 차원의 tensor에서 0 차원에서 1차원으로 넘어갈때 9($3*3$)의 보폭으로 움직여 다음 차원에 접근하게됨
- 이런 경우를 contiguous한 상태라고하는데, 메모리가 연속적으로 들어 있는 경우를 의미함
- transpose를 하고나면 이런 contiguous한 상태가 깨지게 된다.
- 이럴경우 `.contiguous()` 함수를 활용하여 다시 메모리를 연속적으로 만들어 줄 수 있다.

**📰code**
```python
import numpy as np
import torch

t_array = torch.FloatTensor(np.arange(10).reshape(2,5))
print(t_array.shape)
print(t_array.stride())
trans_t_array = t_array.T
print(trans_t_array.stride())
print(trans_t_array.contiguous().stride())
```
**🔍result**
```
torch.Size([2, 5])
(5, 1)
(1, 5)
(2, 1)
```

<br>

### View vs Reshape

- view와 reshape 모두 tensor의 차원을 handling하는 함수이다
- 두 함수의 차이는 contiguous가 깨졌을 때 차이가 발생
- view는 contiguous가 깨졌을 때 error를 발생시키게 되고, `.contiguous()` 함수로 정상화 할 수 있음 → contiguity를 보장함
- reshape은 contiguous가 깨졌을 때 copy를 하여 메모리를 새로 할당하여 진행하게 되 → contiguity를 보장하지 못함
- contiguity를 보장한다 함은 기존 메모리를 계속 사용하는걸 의미함

**📰code**
```python
import torch

a= torch.zeros(3,2)
b=a.T.reshape(6)
a.fill_(1)
print(a)
print(b)
```
**🔍result**
```
tensor([[1., 1.],
        [1., 1.],
        [1., 1.]])
tensor([0., 0., 0., 0., 0., 0.])
```

<br>


### squeeze와 unsqueeze

![image](https://user-images.githubusercontent.com/77658029/129655872-b5b6cb8a-8bd1-4ea5-ad94-83e42bff1338.png)

**📰code**
```python
import numpy as np
import torch

tensor_ex = torch.rand(size=(2,1, 2))
print('1.',tensor_ex.shape)
tensor_ex=tensor_ex.squeeze()
print('2.',tensor_ex.shape)
print('3.',tensor_ex.unsqueeze(0).shape)
print('4.',tensor_ex.unsqueeze(1).shape)
print('5.',tensor_ex.unsqueeze(2).shape)
```
**🔍result**
```
1. torch.Size([2, 1, 2])
2. torch.Size([2, 2])
3. torch.Size([1, 2, 2])
4. torch.Size([2, 1, 2])
5. torch.Size([2, 2, 1])
```

<br>

### mm vs matmul

- matmul의 경우 broadcasting 지원이 되고, mm은 지원이 안됨
- 만약 아래 코드에서 a를 [[1,2]]가 아닌 [1,2]로 바꾸면 error 발생($(2)*(2,1)$연산 시 error 발생)

**📰code**
```python
a = torch.FloatTensor([[1,2]])
b = torch.FloatTensor([[3],[4]])
print(a.shape,b.shape)
print(a*b)
print(a.mm(b))
print(a.matmul(b))
```
**🔍result**
```
torch.Size([1, 2]) torch.Size([2, 1])
tensor([[3., 6.],
        [4., 8.]])
tensor([[11.]])
tensor([[11.]])
```

<br>

### nn.functional

- ML/DL에서 유용하게 사용할 수 있는 여러 함수를 지원해줌
- softmax, argmax, one_hot etc..
- `import torch.nn.functional as F` 형식으로 사용함

<br>

### Auto Gradient

- 자동 미분 기능으로 연쇄법칙도 자동을 진행해줌
- 앞으로는 Linear에 내장되어 있어서 그 기능을 사용하게 될 예정
- `requires_grad=True`가 되어 있어야 미분이 가능함


**📰code**
```python
import numpy as np
import torch

w = torch.tensor(1.0, requires_grad=True)
y = w**3
z = 10*y + 2
z.backward()
w.grad
```
**🔍result**
```
tensor(30.)
```

<br>

**📌reference**
- boostcourse AI tech
- [contiguous란?](https://titania7777.tistory.com/3)
- [stackoverflow](https://stackoverflow.com/questions/61598771/pytorch-squeeze-and-unsqueeze)

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

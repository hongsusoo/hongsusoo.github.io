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

title: "[DL Baic] Weight & Biases - Monitoring tool for PyTorch"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - AI
tags:
  - [python, AI Tool, PyTorch, WandB, monitoring]
date: 2021-08-19
last_modified_at: 2021-08-19
---

<br>  

# Weight & Biases - Monitoring Tool for PyTorch

- 학습시간이 오래걸려 기록에 대한 중요성이 높아짐
- 중간과정에서 더 좋은 결과를 얻을 수 있기 때문에 전체적인 흐름을 확인하는 것은 중요함
- 흐름을 확인하는 방법으로는 Print문, log, csv등 여러 방법이 있음
- 좀 더 직관적이고 괜찮은 monitoring tool로 Tensor Board와 WandB를 많이 사용함

<br>

## Weight & Biases

- 머신러닝 실험을 원활히 지원하기 위한 사용도구(기본적인 기능만 무료로 제공됨)
- 협업, Code Versioning, 실험결과 기록 등 제공
- Github처럼 실험했던 기록들을 남겨줘, 분석에 용이하고 다른 개발자와 협업하기 좋음
- MLOps의 대표적인 툴
- github의 commit처럼 내 실험 기록을 남겨줌

<br>

## Weight & Biases 사용해보기

1. 설치 : `!pip install wandb -q`
2. [Weight & Biases](https://wandb.ai/site) 가입하기
3. 가입 후 Project 만들기
4. `wandb` import 후 project명과 내 ID 입력하여 연결해주기 - wandb에서 내 공간을 할당해줌
    ```python
    import wandb
    wandb.init(project='example_wandb', entity='hongsusoo')
    ```
5. config에 log로 남길 대상들 입력해줌
    ```python
    config={"epochs": EPOCHS, "batch_size": BATCH_SIZE, "learning_rate" : LEARNING_RATE}
    ```
6. project에 config 정보 초기화 

    ```python
    wandb.init(project="example_wandb", config=config)
    ```
7. log를 활용하여 데이터를 넣어줌(tensorboard의 `add_함수`와 동일한 기능)

    ```python
    wandb.log({'accuracy': train_acc, 'loss': train_loss})
    ```

<br>

### **🔍result**

**config에서 정의한 항목을 기록으로 남겨줌**
![image](https://user-images.githubusercontent.com/77658029/130341410-5c761568-4485-4a5b-a2ae-831f8a935806.png)

**system에 대한 기록도 남겨줌**
![image](https://user-images.githubusercontent.com/77658029/130341422-9991286d-6ccd-46e7-b689-7ae234e59928.png)


<br>

**📌reference**
- boostcourse AI tech

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

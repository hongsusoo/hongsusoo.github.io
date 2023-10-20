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

title: "Weight anb Bias 시작 Code sample"
excerpt: "about : "
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - DL
tags:
  - [wandb, monitoring]
date: 2021-11-27
last_modified_at: 2021-11-27
---

<br>

## .py 파일 형식

**📰code**
```python
import wandb

wandb.init(project='NPDH', name=args.model + args.kfold_train + str(learning_rate), ##arg
    config={
    "batch size": batch_size,
    "epochs" : epochs,
    "learning rate": learning_rate,
})

### log 출력부
wandb.log({
        "val Accuracy" : acc, 
        "val Specificity" : spec,
        "val Sensitivity" : sens,
        "val Precision" : prec,
        "val Negative_Predicable_Value" : npv,
        "val F1score" : f1,
        "val total_mean" : (acc+spec+sens+prec+npv+f1)/6
})
```
**🔍result**

![image](https://user-images.githubusercontent.com/77658029/143613868-aecc60d8-7524-444d-afc5-7e3c6ac25b87.png)


## .ipynb 파일 형식

**📰code**
```python
import wandb

os.environ['WANDB_NOTEBOOK_NAME'] = 'code.ipynb'
wandb.init(project='NPDH', name='NB1D_final_data',
    config={
    "batch size": batch_size,
    "epochs" : epochs,
    "learning rate": learning_rate,
    # "backborn" : 'se_resnext101_32x4d', 
    # "architecture" : 'Deeplabv3+', 
})

### log 출력부
wandb.log({
        "train Accuracy" : acc, 
        "train Specificity" : spec,
        "train Sensitivity" : sens,
        "train Precision" : prec,
        "train Negative_Predicable_Value" : npv,
        "train F1score" : f1,
        "train total_mean" : (acc+spec+sens+prec+npv+f1)/6
    })
```
<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

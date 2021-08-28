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

title: "[CV Project] 마스크 착용 상태 분류 - DataSet🌓"
excerpt: "about : Image Classification Competition"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - AI_project
tags:
  - [CV, Modeling, Pstage-01]
date: 2021-08-25
last_modified_at: 2021-08-25
---

<br>

# DataSet

- `__int__` : image의 path와 label, transform 방식을 받아서 변수로 정의
- `__len__` : path 개수를 len으로 출력
- `__getitem__` : DataLoader를 통해 idx를 받으면 idx에 대한 image와 target값을 반환

<br>

## Class 정의

```python
class MyDataset(Dataset):
    def __init__(self, path, label, transform):
        
        self.X = path
        self.y = label
        self.transform = transform

    def __len__(self):
        len_dataset = len(self.X)
        return len_dataset

    def __getitem__(self, idx):
        X,y = self.X[idx], self.y[idx]
        img = cv2.imread(X)
        img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
        X = self.transform(image=X)['image']  # transforms를 사용하시는 분은 X = self.transform(X)
        return X, y
```

<br>

## Class 사용

```python
dataset_train = MyDataset(path=train_df['full_path'].values,
                          label=train_df['label'].values,
                          transform=train_transform)
```

<br>

## DataSet transform 정의

```python
train_transform = albumentations.Compose(
  [
      albumentations.Resize(299,299),
      albumentations.Normalize((0.548, 0.504, 0.479), (0.237, 0.247, 0.246)),
      albumentations.pytorch.transforms.ToTensorV2()
  ]
)
```

<br>

**📌reference**
- boostcourse AI tech


<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

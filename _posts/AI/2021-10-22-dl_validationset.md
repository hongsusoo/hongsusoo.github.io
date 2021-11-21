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

title: "Validation Set 만들기"
excerpt: "about : "
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - DL Basic
tags:
  - [Validationset]
date: 2021-10-22
last_modified_at: 2021-10-22
---

<br>

# Validation Dataset

- Competition을 진행함에 있어서 Validation dataset을 먼저 찾는것이 중요함
- 한 정된 Leader board 제출횟수로 Model에 대한 결과 평가가 애매하기 때문에 LB와 비슷한 경향을 가지는 Validation Set을 구축하여 실험하는 것이 앞으로 만들 model를 평가하는데 큰 지표가 된다

## K-fold

- dataset을 k개로 sampling하는 방식
- 다른 data의 특성을 고려하지 않고 단순 갯수로 나눠 사용하게 됨

![image](https://user-images.githubusercontent.com/77658029/139793068-9a0d5be7-1d5a-4b85-8a40-51509c5b6d41.png)

<br>

**📰code**
```
import numpy as np
from sklearn.model_selection import KFold

X = ["0", "1", "2", "3", "4", "5", "6", "7", "8", "9"]
kf = KFold(n_splits=2)
for train, test in kf.split(X):
    print("%s %s" % (train, test))
```

<br>

**🔍result**
```
[5 6 7 8 9] [0 1 2 3 4]
[0 1 2 3 4] [5 6 7 8 9]
```

## Repeated K-fold

- k-fold를 n_repeats 만큼 반복하여 여러개의 dataset을 제공해줌

<br>

**📰code**
```
import numpy as np
from sklearn.model_selection import RepeatedKFold
X = ["0", "1", "2", "3", "4", "5", "6", "7", "8", "9"]
random_state = 0
rkf = RepeatedKFold(n_splits=2, n_repeats=2, random_state=random_state)
for train, test in rkf.split(X):
    print("%s %s" % (train, test))
```

<br>

**🔍result**
```
[0 3 5 6 7] [1 2 4 8 9]
[1 2 4 8 9] [0 3 5 6 7]
[0 4 6 7 8] [1 2 3 5 9]
[1 2 3 5 9] [0 4 6 7 8]
```

## Leave One Out(LOO)

- 교차검증 방법으로 하나의 샘플을 제외하는 방식으로 모든 샘플을 추출하여 dataset을 생성함
- 데이터 수가 적을때 사용될 수 있음

<br>

**📰code**
```
from sklearn.model_selection import LeaveOneOut

X = ["0", "1", "2", "3", "4", "5"]
loo = LeaveOneOut()
for train, test in loo.split(X):
    print("%s %s" % (train, test))
```

<br>

**🔍result**
```
[1 2 3 4 5] [0]
[0 2 3 4 5] [1]
[0 1 3 4 5] [2]
[0 1 2 4 5] [3]
[0 1 2 3 5] [4]
[0 1 2 3 4] [5]
```

## Leave P Out(LPO)

- 교차검증의 한 방법으로 여러 샘플을 제외하는 방식으로 모든 샘플을 추출하여 Dataset를 구성해줌
- LOO와 방식은 동일하지만, 추출 샘플 수가 1개가 아닌 p개로 설정해 줄 수 있음


<br>

**📰code**
```
from sklearn.model_selection import LeavePOut

X = ["0", "1", "2", "3", "4", "5"]
lpo = LeavePOut(p=2)
for i, (train, test) in enumerate(lpo.split(X)):
    print("%s %s" % (train, test), end = "   ")
    if i%2==1: print()
```

<br>

**🔍result**
```
[2 3 4 5] [0 1]   [1 3 4 5] [0 2]   
[1 2 4 5] [0 3]   [1 2 3 5] [0 4]   
[1 2 3 4] [0 5]   [0 3 4 5] [1 2]   
[0 2 4 5] [1 3]   [0 2 3 5] [1 4]   
[0 2 3 4] [1 5]   [0 1 4 5] [2 3]   
[0 1 3 5] [2 4]   [0 1 3 4] [2 5]   
[0 1 2 5] [3 4]   [0 1 2 4] [3 5]   
[0 1 2 3] [4 5]   
```

## SuffleSplit

- 샘플을 무작위로 섞은뒤 Dataset을 나눔
- random_state 값을 정해두어 결과 재현이 가능함

![image](https://user-images.githubusercontent.com/77658029/139794219-a39e2cc5-da07-428a-b6f0-308f8f0ab90d.png)


<br>

**📰code**
```
from sklearn.model_selection import ShuffleSplit

X = ["0", "1", "2", "3", "4", "5", "6", "7", "8", "9"]
ss = ShuffleSplit(n_splits=5, test_size=0.25, random_state=0)
for train_index, test_index in ss.split(X):
    print("%s %s" % (train_index, test_index))
```

<br>

**🔍result**
```
[9 1 6 7 3 0 5] [2 8 4]
[2 9 8 0 6 7 4] [3 5 1]
[4 5 1 0 6 9 7] [2 3 8]
[2 7 5 8 0 3 4] [6 1 9]
[4 1 0 6 8 9 3] [5 2 7]
```

## Stratified K-Fold

- Class의 불균형이 있을때 Class의 비율이 포함된 상태로 Dataset을 추출해줌

![image](https://user-images.githubusercontent.com/77658029/139794444-83a107e4-634b-4413-a720-9ada9e49caca.png)

<br>

**📰code**
```
import numpy as np
from sklearn.model_selection import StratifiedKFold, KFold

X, y = np.ones((20, 1)), np.hstack(([0] * 15, [1] * 5))
skf = StratifiedKFold(n_splits=3)
skf.get_n_splits(X, y)

for train_index, test_index in skf.split(X, y):
    y_train, y_test = y[train_index], y[test_index]
    print("TRAIN:", y_train, "TEST:", y_test)
```

<br>

**🔍result**
```
TRAIN: [0 0 0 0 0 0 0 0 0 0 1 1 1] TEST: [0 0 0 0 0 1 1]
TRAIN: [0 0 0 0 0 0 0 0 0 0 1 1 1] TEST: [0 0 0 0 0 1 1]
TRAIN: [0 0 0 0 0 0 0 0 0 0 1 1 1 1] TEST: [0 0 0 0 0 1]
```

## Stratified Shuffle Split

- Class의 비율은 유지하며 무작위로 분할 추출함

![image](https://user-images.githubusercontent.com/77658029/139795459-821308b9-8ae9-4c3f-ad03-0714281aad25.png)


**📰code**
```
import numpy as np
from sklearn.model_selection import StratifiedShuffleSplit
X, y = np.ones((20, 1)), np.hstack(([0] * 15, [1] * 5))
sss = StratifiedShuffleSplit(n_splits=5, test_size=0.2, random_state=0)
sss.get_n_splits(X, y)

for train_index, test_index in sss.split(X, y):
    y_train, y_test = y[train_index], y[test_index]
    print("TRAIN:", y_train, "TEST:", y_test)
```

<br>

**🔍result**
```
TRAIN: [0 1 0 0 0 1 1 0 0 0 0 1 0 0 0 0] TEST: [0 0 0 1]
TRAIN: [0 1 0 0 0 1 0 0 0 0 1 0 0 1 0 0] TEST: [0 0 1 0]
TRAIN: [0 0 0 0 0 0 0 1 0 0 0 1 0 1 0 1] TEST: [1 0 0 0]
TRAIN: [0 0 1 0 0 0 1 0 1 0 0 1 0 0 0 0] TEST: [1 0 0 0]
TRAIN: [0 0 0 0 0 0 0 0 1 0 1 0 0 1 0 1] TEST: [0 0 0 1]
```

## Group K-Fold

- 동일한 Group이 검등 Dataset에 동시에 포함되지 않도록 하는 방법

![image](https://user-images.githubusercontent.com/77658029/139796436-78d079a6-1b85-4724-a0a8-067328648a21.png)

**📰code**
```
from sklearn.model_selection import GroupKFold

X, y = np.ones((16, 1)), np.hstack(([0] * 11, [1] * 5))
groups = np.array(['a','a','a','a','b','b','b','b','c','c','c','c','d','d','d','d'])
gkf = GroupKFold(n_splits=3)
gkf.get_n_splits(X, y,groups = groups)

for train_index, test_index in gkf.split(X, y,groups):
    groups_train, groups_test = groups[train_index], groups[test_index]
    print("TRAIN:", groups_train, "TEST:", groups_test)
```

<br>

**🔍result**
```
TRAIN: ['b' 'b' 'b' 'b' 'c' 'c' 'c' 'c'] TEST: ['a' 'a' 'a' 'a' 'd' 'd' 'd' 'd']
TRAIN: ['a' 'a' 'a' 'a' 'b' 'b' 'b' 'b' 'd' 'd' 'd' 'd'] TEST: ['c' 'c' 'c' 'c']
TRAIN: ['a' 'a' 'a' 'a' 'c' 'c' 'c' 'c' 'd' 'd' 'd' 'd'] TEST: ['b' 'b' 'b' 'b']
```

## Stratified Group K-Fold

- 동일한 Group이 검등 Dataset에 동시에 포함되지 않도록 하는 방법

![image](https://user-images.githubusercontent.com/77658029/139796436-78d079a6-1b85-4724-a0a8-067328648a21.png)

**📰code**
```
import numpy as np
from sklearn.model_selection import StratifiedGroupKFold

X, y = np.ones((16, 1)),np.array(['a','a','a','a','b','b','b','b','c','c','c','c','d','d','d','d'])
groups = np.array([1,2,3,4,1,2,3,4,1,2,3,4,1,2,3,4])
sgk  = StratifiedGroupKFold(n_splits=3)
for train_index, test_index in sgk .split(X, y, groups=groups):
    groups_train, groups_test = groups[train_index], groups[test_index]
    print("TRAIN:", groups_train, "TEST:", groups_test)
```

<br>

**🔍result**
```
TRAIN: [2 3 2 3 2 3 2 3] TEST: [1 4 1 4 1 4 1 4]
TRAIN: [1 3 4 1 3 4 1 3 4 1 3 4] TEST: [2 2 2 2]
TRAIN: [1 2 4 1 2 4 1 2 4 1 2 4] TEST: [3 3 3 3]
```

## Leave One Group Out

- LOO와 비슷한 방법이지만 한 샘플이 아닌 Group에 대한 교차 검증 dataset를 제공해줌

**📰code**
```
from sklearn.model_selection import LeaveOneGroupOut

X, y = np.ones((16, 1)), np.hstack(([0] * 11, [1] * 5))
groups = np.array(['a','a','a','a','b','b','b','b','c','c','c','c','d','d','d','d'])
logo = LeaveOneGroupOut()
for train_index, test_index in logo.split(X, y, groups=groups):
    groups_train, groups_test = groups[train_index], groups[test_index]
    print("TRAIN:", groups_train, "TEST:", groups_test)
```

<br>

**🔍result**
```
TRAIN: ['b' 'b' 'b' 'b' 'c' 'c' 'c' 'c' 'd' 'd' 'd' 'd'] TEST: ['a' 'a' 'a' 'a']
TRAIN: ['a' 'a' 'a' 'a' 'c' 'c' 'c' 'c' 'd' 'd' 'd' 'd'] TEST: ['b' 'b' 'b' 'b']
TRAIN: ['a' 'a' 'a' 'a' 'b' 'b' 'b' 'b' 'd' 'd' 'd' 'd'] TEST: ['c' 'c' 'c' 'c']
TRAIN: ['a' 'a' 'a' 'a' 'b' 'b' 'b' 'b' 'c' 'c' 'c' 'c'] TEST: ['d' 'd' 'd' 'd']
```

## Leave P Group Out

- LOO와 LPO의 관계와 같이 Group을 1개가 아닌 여러개를 선택하여 Dataset을 구축

**📰code**
```
from sklearn.model_selection import LeavePGroupsOut

X, y = np.ones((16, 1)), np.hstack(([0] * 11, [1] * 5))
groups = np.array(['a','a','a','a','b','b','b','b','c','c','c','c','d','d','d','d'])
lpgo  = LeavePGroupsOut(n_groups=2)
for train_index, test_index in lpgo .split(X, y, groups=groups):
    groups_train, groups_test = groups[train_index], groups[test_index]
    print("TRAIN:", groups_train, "TEST:", groups_test)
```

<br>

**🔍result**
```
TRAIN: ['c' 'c' 'c' 'c' 'd' 'd' 'd' 'd'] TEST: ['a' 'a' 'a' 'a' 'b' 'b' 'b' 'b']
TRAIN: ['b' 'b' 'b' 'b' 'd' 'd' 'd' 'd'] TEST: ['a' 'a' 'a' 'a' 'c' 'c' 'c' 'c']
TRAIN: ['b' 'b' 'b' 'b' 'c' 'c' 'c' 'c'] TEST: ['a' 'a' 'a' 'a' 'd' 'd' 'd' 'd']
TRAIN: ['a' 'a' 'a' 'a' 'd' 'd' 'd' 'd'] TEST: ['b' 'b' 'b' 'b' 'c' 'c' 'c' 'c']
TRAIN: ['a' 'a' 'a' 'a' 'c' 'c' 'c' 'c'] TEST: ['b' 'b' 'b' 'b' 'd' 'd' 'd' 'd']
TRAIN: ['a' 'a' 'a' 'a' 'b' 'b' 'b' 'b'] TEST: ['c' 'c' 'c' 'c' 'd' 'd' 'd' 'd']
```

## Group Shuffle Split

- LOO와 LPO의 관계와 같이 Group을 1개가 아닌 여러개를 선택하여 Dataset을 구축
- Group을 선정할때 Test_size가 group의 개수만큼 나눠지지 않을 경우, 올림하여 계산하게됨(만약 4개의 group으로 이뤄져 있을때, test_size가 0.1로 group 1개보다 적게 될 경우 올림 처리하여 group 1개를 Test로 가져가게 됨)

![image](https://user-images.githubusercontent.com/77658029/139797596-dc1ffe46-b695-4e7a-81ff-f85b9ea109a2.png)

**📰code**
```
from sklearn.model_selection import GroupShuffleSplit

X, y = np.ones((16, 1)), np.hstack(([0] * 11, [1] * 5))
groups = np.array(['a','a','a','a','b','b','b','b','c','c','c','c','d','d','d','d'])
gss = GroupShuffleSplit(n_splits=4, test_size=0.25, random_state=0)
for train_index, test_index in gss .split(X, y, groups=groups):
    groups_train, groups_test = groups[train_index], groups[test_index]
    print("TRAIN:", groups_train, "TEST:", groups_test)
```

<br>

**🔍result**
```
TRAIN: ['a' 'a' 'a' 'a' 'b' 'b' 'b' 'b' 'd' 'd' 'd' 'd'] TEST: ['c' 'c' 'c' 'c']
TRAIN: ['b' 'b' 'b' 'b' 'c' 'c' 'c' 'c' 'd' 'd' 'd' 'd'] TEST: ['a' 'a' 'a' 'a']
TRAIN: ['a' 'a' 'a' 'a' 'b' 'b' 'b' 'b' 'c' 'c' 'c' 'c'] TEST: ['d' 'd' 'd' 'd']
TRAIN: ['a' 'a' 'a' 'a' 'c' 'c' 'c' 'c' 'd' 'd' 'd' 'd'] TEST: ['b' 'b' 'b' 'b']
```

## Time Series Split

- 첫 Fold는 Train, 두번째 Fold를 Test 세트로 분할
- 다음 Dataset은 두번째 Fold까지 Train, 세번째 Fold를 Test로 분할
- 연속적인 훈련 데이터 세트는 이전 훈련 및 검증 데이터를 포함한 상위 집합으로 구성됨
- 고정 시간 간격으로 관측된 시계열 데이터 샘플을 교차 검증할때 사용함

![image](https://user-images.githubusercontent.com/77658029/139798167-f2505415-5d1b-46e7-82b9-b87669698769.png)

**📰code**
```
from sklearn.model_selection import TimeSeriesSplit

X, y = np.ones((16, 1)), np.hstack(([0] * 11, [1] * 5))
tscv = TimeSeriesSplit(n_splits=3)
for train_index, test_index in tscv .split(X, y, groups=groups):
    y_train, y_test = y[train_index], y[test_index]
    print("TRAIN:", y_train, "TEST:", y_test)
```

<br>

**🔍result**
```
TRAIN: [0 0 0 0] TEST: [0 0 0 0]
TRAIN: [0 0 0 0 0 0 0 0] TEST: [0 0 0 1]
TRAIN: [0 0 0 0 0 0 0 0 0 0 0 1] TEST: [1 1 1 1]
```

**📌reference**
- boostcourse AI tech
- [존스유 k-fold](https://jonsyou.tistory.com/23)

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

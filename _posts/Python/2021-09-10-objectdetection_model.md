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

title: "[AI Model] Object Detection Model 소개"
excerpt: "about : Object Detection"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - AI
tags:
  - [CV, AI Model, Object Detection]
date: 2021-09-10
last_modified_at: 2021-09-28
---

<br>

# Object Detection

- 응용 분야가 많아 많은 스타트업에서 시도하고 있음
- 산업가치가 크기 때문에 관심을 많이 받고 있음

<br><br>

## Object Detection 이란

- Semantic Sementation과 Class를 구별하는 건 동일
- Object Detection은 동일 Class에서도 객체를 구별할 수 있음
- 같은 사람,자동차 Class여도 객체를 구별할 수 있음

![image](https://user-images.githubusercontent.com/77658029/132781732-671dbe62-7f5a-4d2e-ace4-61c9ca208d02.png)

<br>

- Object Detection은 **Classification**과 **Box localization**를 합친 문제라고 생각할 수 있음

![image](https://user-images.githubusercontent.com/77658029/132782561-9a0b70d8-e938-4174-a7ca-8768fad5ab77.png)

<br><br><br>

## 과거 Object Detection 방법

<br>

### Gradient-based detector

- 경계선 특징을 Modeling하여 학습하여 사람의 실루엣을 찾아냄

![image](https://user-images.githubusercontent.com/77658029/132783452-cf36075c-80b5-4987-961b-9aa49db50263.png)

<br><br><br>

### Selective Search

- 만약 Sliding window 방식으로 후보군을 추출하게 되면 너무 많은 후보군이 생겨, 문제가 발생할 수 있음
- 이 문제를 해결하기 위해 Selective Search 방식이 도입됨
- 처음 여러개의 bounding box로 over Segmentation을 진행
- 그 다음 색이나, 질감, Gradient분포가 비슷한 부분들을 merge시키는 작업을 진행(이때 비슷한 부분을 추출하는 방법을 미리 정해줘야함)
- 확률이 큰 Segmentation에 타이트한 바운딩 박스를 그려 object 후보군을 만듬

![image](https://user-images.githubusercontent.com/77658029/132783738-10901ffa-af7e-4d53-a66f-0dcfea7d9f59.png)

<br><br><br>

## Object Detection의 구분

- Object Detection은 크게 Two Stage, One Stage detection 방식으로 구분됨
- **Two Stage 방식** : 1)Object가 있을 위치를 제안해주는 Stage, 2)Object를 Detection Stage
    + 장점 : Object에대한 정확한 위치를 확인하여 분류할 수 있음
    + 단점 : Object 위치를 제안하기 위한 Process가 진행되어 One Stage 방식에 비해 속도가 느림
    + 관련 모델 : RCNN, SPPNet, Fast RCNN, Faster RCNN
- **One Stage 방식** : Object에 대한 위치를 default된 영역에서 추출, 1) Object Detection Stage
    + 장점 : Two Stage 방식에 비해 처리 속도가 기하급수적으로 빨라짐
    + 단점 : Two Stage 방식에 비해 정확도가 떨어짐 -> 현재는 더 빠르고 정확해짐
    + 관련 모델 : YOLO, SSD, RetinaNet
    
    
![image](https://user-images.githubusercontent.com/77658029/132936787-44ac96f2-f02c-4a67-93a5-ca6ca8173b14.png)

<br><br><br>

## Two-Stage Detection

<br>

### R-CNN(Region-based CNN)_Detection, Localization

![image](https://user-images.githubusercontent.com/77658029/129477391-2d20150a-f54b-4651-9ea7-70dc5eeda8d8.png)

<br><br>

**알고리즘 흐름**
1. Input으로 들어온 이미지에서 2k정도의 후보 영역(Region proposal)을 뽑아냄 -> Selective Search 알고리즘
2. 후보 영역을 잘라내어 CNN Input의 고정된 크기로 Warping
3. CNN 분류모델(AlexNet)을 활용하여 feature를 뽑음

+) pre-trained된 AlexNet + fine tune(Object Detection용 데이터 셋 사용)

4. CNN을 통해 나온 feature map을 사용하여 벡터를 추출하고 클래스 별로 SVM Classifier 학습, regressor를 통한 Bounding Box Regression을 진행한다.

+) 2k의 bounding box는 SVM 이후 클래스별 확률값을 갖게 된다. 2k의 bounding box을 모두 사용하는 것이 아닌 Score 값이 가장 큰 Bounding box만을 사용하기 위해 Non-Maximum Suppression 알고리즘을 사용하여 박스 하나를 추출해 낸다. 이때 알고리즘 내부에서 IoU(Intersection over Union)를 활용하여 두 bounding box의 교집합을 합집합으로 나눠준 값을 기준으로 bounding box를 추출해낸다.

![image](https://user-images.githubusercontent.com/77658029/132794440-5e9bdf3d-8f67-4a76-b391-8e144bbad63c.png)

+) Bounding Box Regression을 사용하는 이유는 Selective Search를 통해 찾은 박스 위치가 부정확하기 때문에 모델의 성능을 높이기 위해 박스 위치를 교정하기 위해 사용한다. 박스의 위치를 조절하는 과정은 박스의 좌표 및 너비 높이를 조정하는 함수의 가중치를 곱하며 선형 회귀 학습을 시키기 때문에 Regression이 함께 들어가 있다.

<br><br>

**🔎 RCNN 학습**

- CNN : AlexNet을 FineTuning 하여 사용
- fine Tuning시 Dataset 구성
    - IoU > 0.5 : Positive Samples
    - IoU < 0.5 : Negative Samples
    - 한 Batch당 Positive Samples 32, Negative Samples 96

- Linear SVM Dataset 구성
    - Ground Truth : Positive Samples
    - IoU < 0.3 : Negative Samples
    - 한 Batch당 Positive Samples 32, Negative Samples 96

- Hard Negative mining 기법 활용
    - Hard Negative : False Positive
    - 배경으로 예측하기 어려운 Sample들을 다음번에 Negative samples로 강제로 편입시킴, 모델이 구분하기 어려운 Sample를 강제로 추가시켜 보완시키는 방법

- BBox Regressor 
    - Dataset 구성 : IoU > 0.6 : Positive Samples
    - Loss function : MSE Loss

<br><br>

**🚨 RCNN의 단점**

1. 2000개의 crop image를 다시 처리해야하기 때문에 1장의 이미지 구분 시 시간이 오래 걸림(59s/image on CPU)
2. Crop image를 뽑은 후 warping으로 인한 image의 특징이 변경됨

+) CNN를 하기 위해서는 FC layer의 size를 맞추기 위해서 input image의 크기를 맞춰줘야함

3. 여러번의 학습단계가 필요함(fine-tuning(FC layer), SVM training, Bounding Box Regression)

<br><br><br>

### SPP-Net(Spatial Pyramid Pooling)

<br>

💡 Localization 작업을 CNN 이후로 옮겨, CNN 계산에 들어가는 시간을 단축

**🔎 CNN이후로 옮겼을 때의 문제점 → SPP로 해결함**

- CNN 이후로 Localization을 진행할 경우 FC Layer로 입력시 input size가 달라지는 문제가 발생(RCNN에서는 Warping으로 진행)
- FC layer input size를 맞추기 위해 SPP 기법 도입

<br>

![image](https://user-images.githubusercontent.com/77658029/129479633-4a165da2-0744-47d7-8c27-d7a734e145cc.png)

<br><br>

**알고리즘 흐름**

1. input image를 CNN 진행하여 feature map을 뽑음(R-CNN에서는 Selective Search를 통한 2k개의 후보영역 wrapping 하여 CNN 진행)
2. crop된 feature를 SPP하는 작업을 진행
    
+) SPP(Spatial Pyramid Pooling) : pooling시 여러 kernel size를 활용하여 max pooling 진행하여 FC Layer의 input size를 맞춰줌, 여러 사이즈(1x1,2x2,3x3,6x6, 논문에서 사용한 사이즈)의 pooling영역을 지정해 둬서 사용하는데 이 부분를 pyramid라고 불림
    
+) 여기서 `bin`이라는 용어가 나오는데, `bin`이란 한 번의 max pooling의 연산으로 발생한 하나의 값을 bin이라고 함, 만약 64x64x256사이즈의 feature를 4x4 maxpooling을 하면 bin의 사이즈는 16x16x256가 됨

![image](https://user-images.githubusercontent.com/77658029/135023849-2b73f2db-1ddf-422b-b449-12c3234d8d02.png)

3. 생성된 `bin`를 flatten 하게 만들어 Classification 진행함

    R-CNN : ① image input → **② extract crop image(RoI) → ③ resize crop image(wrapping) → ④ CNN** → ⑤ Classify

    SPP-Net : ① image input → **② CNN → ③ SPP** → ④ Classify

<br><br>

**🚨 SPP-Net의 단점**

1. SPPNet도 결국은 여러개의 tensor를 뽑아내서 하나의 벡터로 만들고 다시 분류하는 작업 필요하기 때문에 시간이 오래걸림
2. 여러번의 학습단계가 필요함(fine-tuning(FC layer), SVM training, Bounding Box Regression)

<br><br><br>

### Fast R-CNN

<br>

💡 RoI Pooling으로 Crop image feature를 Neural Network 안으로 끌어드림

<br>

![image](https://user-images.githubusercontent.com/77658029/129481619-c2da7843-9fbd-418f-b52c-c9d501c03978.png)

<br><br>

**알고리즘 흐름**
1. input image를 CNN 진행하여 feature map을 뽑음(SPPNet과 동일함)
2. Selective Search 알고리즘을 통한 RoI(Region of Interest) 지정
3. `RoI Pooling`을 진행 고정된 크기의 feature vector 얻음

+) SPP에서 1개의 pyramid Layer를 사용하여 Feature Vector를 구하는 방식과 비슷함

![image](https://user-images.githubusercontent.com/77658029/132802142-94f075ad-7989-4c69-b919-830f686df56c.png)

4. `feature vector`를 fully connected layer에 통과시킨 후 2개의 브랜치로 나눠줌
5. 하나의 브랜치는 softmax를 통해 RoI Classification 진행
6. 남은 하나의 브랜치는 bouding box regression을 통해서 selective search로 찾은 박스의 위치를 조정
7. `Multi Task loss`를 활용하여 bounding box의 위치 loss와 Classification loss를 한번에 처리해줌

+) 기존엔 FC Layer까지만 학습하여 사용했었는데, CNN의 fine-tuning 까지 가능해졌음

<br><br>

**+) Multi Task Loss**

- feature vector를 통해 얻은 Classifier와 bounding box regression의 loss를 통해 back propagation하여 전체 모델을 학습
- classificaiton loss와 bounding box regression을 적절하게 엮어주는 것이 `multi task loss`
- Loss Function
    + Classification : Cross Entropy
    + BB Regressor : Smooth L1
- Dataset 구성
    + IoU > 0.5 : Positive Samples
    + 0.1 < IoU < 0.5 : Negative samples
    + Batch : Positive samples 25%, negative samples 75%
- Hierarchical sampling
    + 한 배치에 한 이미지의 RoI만 포함 -> 배치 안에서 메모리 공유가능하여 효율성 증가
    + 기존 RCNN의 경우 전체 이미지에 존재하는 RoI를 전부 저장해 사용 -> 메모리 공유 어려움

<br><br>

**수식**

![image](https://user-images.githubusercontent.com/77658029/132802521-e41c060d-af7e-4f66-acb1-077fcdd52242.png)

-> bounding box regression loss에서 사용된 Smooth 수식은 아래와 같다

![image](https://user-images.githubusercontent.com/77658029/132802691-8b770500-c224-4830-b569-1b84a0b80465.png)

- 예측 값과 라벨 값의 차가 1보다 작으면 0.5x^2 (L2 distance)
- 예측 값과 라벨 값의 차가 1보다 클 경우 |x|-0.5 (L1 distance)
- 저자들이 실험중 라벨 값과 지나치게 차이가 많이나는 Outlier예측 값이 나왔을 경우 L2 distance로 계산하면 Gradient가 exploding되는 현상이 관찰되어 거리가 커지면 L1 distance로 custom 해줌

<br><br>

**RoI Pooling**

- RCNN과 동일하게 Selective Search 방식으로 image BBOX 정보를 추출함
- 하지만 Image에서 crop하는 것이 아닌 CNN 이후 Feature map에서 ROI를 진행함
- 그러면서 BBOX에 대한 정보도 Feature map에 project 시켜서 사용하게됨

![image](https://user-images.githubusercontent.com/77658029/135024731-5c4aa36e-6f0c-48bc-9312-1187331ba7d9.png)

<br><br>

**🚨 Fast R-CNN의 단점**

1. Selective search를 이용하여 결국은 2000개의 region를 무작위로 뽑아서 학습하게됨
2. R-CNN과 동일하게 Multi-stage pipline 형태가 유지됨

<br><br><br>


### Faster R-CNN

<br>

💡 Selective Search 방식을 RPN을 통해 RoI를 학습시키는 방법으로 Network 안으로 끌어들임(2K image → 0.8k image)

+) 첫 End-to-End 방식의 Object detection 모델

+) Selective Search은 CPU내에서 돌기 때문에 GPU로 돌리기 위한 시도

<br>

![image](https://user-images.githubusercontent.com/77658029/132805516-ce98fb41-5a46-451b-834d-6dd59feaa298.png)

<br>

**알고리즘 흐름**
1. image를 받으면 CNN을 통해 Feature를 추출
2. 1번과 동시에 `RPN(Region proposal Network)`을 통해 객체가 있을 만한 곳의 위치를 제안함

+) RPN(Region proposal Network)의 동작 원리는 sliding window 방식으로 돌면서 미리 선정한 `anchor box`를 그려 그 안에 1)object가 있는지 예측값과, 2) bbox(bounding box)의 위치정보를 함께 전달함

![image](https://user-images.githubusercontent.com/77658029/135025660-b1e6523e-7709-4846-abdc-ad6a0f40669e.png)

+) `anchor box` : anchor box에 의해서 여러개의 bbox가 생성되었을때, 모든 Box를 사용하게 될 경우 너무 많은 bbox가 생성되기 때문에, 이 숫자를 줄여주기 위해 NMS 기법을 사용함

![image](https://user-images.githubusercontent.com/77658029/135025446-589523b3-30b9-4581-916a-b82ec6dcc28d.png)

+) NMS(Non-Max Suppression) : 비슷한 bbox를 제거하는 알고리즘으로 특정 Threshold 값으로 IoU 값이 나오는 bbox는 지워주는 작업을 진행함

3. RPN을 통해 얻은 영역을 RoI Pooling을 진행
4. FC layer를 거쳐 Softmax를 통해 Classification loss를 구함
5. FC layer를 거쳐 Box Offset Regressor loss를 구함
6. 두 Loss로 RPN과 CNN, FC layer를 학습시킴

+) Train의 경우 `anchor box`(Bounding Box)와 GT(Ground Truth) 사이에 IoU를 진행해 loss를 구하고 이 값으로 train 진행함

+) loss 함수는 아래와 같이 bbox와 classification 두 가지 영역의 loss 합으로 계산함 

![image](https://user-images.githubusercontent.com/77658029/132936632-ef6eb071-9e7c-4ca8-b35d-25f5993003f5.png)

<br><br>

**RPN Loss 함수**

![image](https://user-images.githubusercontent.com/77658029/135026441-9fbd71ba-937b-4e0d-aab5-4012d9d676ab.png)

- RPN 단계에서 classification과 regressor학습을 위해 앵커박스를 positive/negative samples 구분
- 데이터셋 구성
    + IoU > 0.7 or highest IoU with GT: positive samples
    + IoU < 0.3: negative samples
    + Otherwise : 학습데이터로 사용 X

<br><br>

**Fast RCNN Loss 함수 **

- Loss 함수 : Fast RCNN과 동일
- 데이터셋 구성
    - IoU > 0.5: positive samples → 32개
    - IoU < 0.5: negative samples → 96개
    - 128개의 samples로 mini-bath 구성

<br><br>

**Further Question**

- Q : 두 가지 분류기로 class 예측 부분과 bbox의 예측 좌표값을 따로 예측하는데 어떻게 Class 예측은 어떻게 GT에서 정답 위치를 가져올 수 있을까?

- A : 예측된 bbox를 GT에 매칭 시켜 IoU를 통해 위치에 대한 pixel별 label를 얻어 올 수 있음

<br><br><br>

### R-CNN vs Fast R-CNN vs Faster R-CNN

<br>

![image](https://user-images.githubusercontent.com/77658029/132846102-fb0f2624-44a0-4d91-a760-02d6cbf120e6.png)

<br><br><br>

## One-Stage Detection

<br><br>

### YOLO(You Only Look Once)

<br>

💡 하나의 신경망으로 Bounding Box과 Class 확률 예측까지 한번에 이루어짐

+) Class 확률의 경우는 Bounding Box와 GT의 IoU로 계산함

**특징**
- Faster R-CNN보다 7배가량 속도가 빠름 -> 실시간으로 Object Detection이 가능함
- Real Time으로 처리하나, 정확도는 약간 떨어짐(Real-time Object Detection)
- 훈련단계에서 Image 전체를 한번에 읽어 학습하기 때문에 Background에 대한 구분이 Two Stage 구조에 비해 잘됨

<br>

![image](https://user-images.githubusercontent.com/77658029/129485947-eda52b4c-6902-41bf-b9ee-acff2781d944.png)

<br>

**알고리즘 흐름**
1. Image를 특정 Grid로 나누어 줌(논문에서는 7x7 grid로 진행)
2. Network 진행을 하면 2가지 Feature 영역으로 반환

+) 첫 번째 Feature 영역 : 각 Grid 별로 Bounding Box의 예측 좌표와 그에 대한 예측 Object Score값을 반환

![image](https://user-images.githubusercontent.com/77658029/132978363-c701aef1-bab6-48d6-a8fd-0efa39bc403c.png)

+) 두 번쨰 Feature 영역 : Grid 별로 Class의 확률 계산 -> 기존 classfication과 동일한 방식으로 grid 하나에 대한 확률을 나타냄

![image](https://user-images.githubusercontent.com/77658029/132978555-b085d405-ca36-4878-8924-8105cdf829a5.png)

+)예측하는 BBox를 구하기 위해서 Non-Max Suppression 방식으로 Score가 높은 이미지를 추려냄


3. 두 Feature 값 두개를 받아 우선적으로 Score가 높은 BBox를 추려내는 작업 진행(Non Maximum Suppression)

![image](https://user-images.githubusercontent.com/77658029/132981278-27128794-870b-4a95-8ef6-ae57081fd005.png)

<br>

4. 3번에서 예측한 BBox의 좌표 정보와 label 정보로 Loss를 산출하여 Training 진행

<br>
<br>

**+) Multi Task Loss function**

![image](https://user-images.githubusercontent.com/77658029/133112047-d57d60bb-abbd-4384-9167-e9183e250f72.png)

<br><br>

**Further Question**

- Q : VOLO 영상에서는 동일 class도 여러개 인식하던데, 위에 설명을 생각해보면 NMS로 인해 Class별로 하나의 bbox만 그려지게 될것같은데, 뭐가 다를까요?

- A : VOLO v1에서 관련 문제가 있어서, 추후 version을 update하면서 개선함

<br><br><br>

### SSD(Single Shot MulitBox Detector)

<br>

- YOLO에서 정확성과 속도 두 마리 토끼를 모두 잡은 모델
- YOLO의 단점은 그리드별로 BBOX 예측으로 인한 그리드 크기보다 작은 물체를 잡기 어려웠음
- Conv의 마지막 feature만 사용하기 떄문에 Coarse 한 정보만 남게 되어 정확도 떨어짐

<br>

![image](https://user-images.githubusercontent.com/77658029/133112840-b3d440f2-d754-4649-a3e1-4406a538f7a8.png)

<br><br><br>

## Model에 따른 성능 비교

<br>

![image](https://user-images.githubusercontent.com/77658029/133112218-d755d0f9-e5e0-4736-8879-b0ee8609a383.png)


<br><br>

**📌reference**
- boostcourse AI tech
- [Robot Sapiens](https://medium.com/@sapiensrobot/real-time-object-detection-705c2d26b6f7)
- [공부하려고 만든 블로그](https://welcome-to-dewy-world.tistory.com/110)
- [갈아먹는 머신러닝](https://yeomko.tistory.com/17?category=888201)
- [귀퉁이 서재](https://bkshin.tistory.com/entry/%EB%85%BC%EB%AC%B8-%EB%A6%AC%EB%B7%B0-YOLOYou-Only-Look-Once)
- [CURG YOLO](https://medium.com/curg/you-only-look-once-%EB%8B%A4-%EB%8B%A8%EC%A7%80-%ED%95%9C-%EB%B2%88%EB%A7%8C-%EB%B3%B4%EC%95%98%EC%9D%84-%EB%BF%90%EC%9D%B4%EB%9D%BC%EA%B5%AC-bddc8e6238e2)
- [YOLO 교육 자료](https://docs.google.com/presentation/d/1aeRvtKG21KHdD5lg6Hgyhx5rPq_ZOsGjG5rJ1HP7BbA/pub?start=false&loop=false&delayms=3000&slide=id.g137784ab86_4_767)
- [약초의 숲](https://herbwood.tistory.com)

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

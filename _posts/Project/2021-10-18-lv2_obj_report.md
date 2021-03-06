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

title: "[object detection] Wrap up Report"
excerpt: "about : object detection"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - AI
tags:
  - 
date: 2021-10-18
last_modified_at: 2021-10-18
---

<br>
# ๐์ฌํ์ฉ ํ๋ชฉ ๋ถ๋ฅ๋ฅผ ์ํ Object Detection Report๐

# ๋ชฉ์ฐจ

- [๋ํ ๊ฐ์](#๋ํ-๊ฐ์)
- [๋ฌธ์  ์ ์](#๋ฌธ์ -์ ์)
- [์คํ ๋ด์ฉ](#๋ฌธ์ ์-๋ํ-์คํ)
- [Modeling ๋ฐ Ensemble](#Modeling-๋ฐ-Ensemble)
- [ํ๊ณ ](#ํ๊ณ )


# ๋ํ ๊ฐ์

![](https://i.imgur.com/PnOdQ0L.png)

๋ฐ์ผํ๋ก ๋๋ ์์ฐ, ๋๋ ์๋น์ ์๋. ์ฐ๋ฆฌ๋ ๋ง์ ๋ฌผ๊ฑด์ด ๋๋์ผ๋ก ์์ฐ๋๊ณ , ์๋น๋๋ ์๋๋ฅผ ์ด๊ณ  ์์ต๋๋ค. ํ์ง๋ง ์ด๋ฌํ ๋ฌธํ๋ '์ฐ๋ ๊ธฐ ๋๋', '๋งค๋ฆฝ์ง ๋ถ์กฑ'๊ณผ ๊ฐ์ ์ฌ๋ฌ ์ฌํ ๋ฌธ์ ๋ฅผ ๋ณ๊ณ  ์์ต๋๋ค.

๋ถ๋ฆฌ์๊ฑฐ๋ ์ด๋ฌํ ํ๊ฒฝ ๋ถ๋ด์ ์ค์ผ ์ ์๋ ๋ฐฉ๋ฒ ์ค ํ๋์๋๋ค. ์ ๋ถ๋ฆฌ๋ฐฐ์ถ ๋ ์ฐ๋ ๊ธฐ๋ ์์์ผ๋ก์ ๊ฐ์น๋ฅผ ์ธ์ ๋ฐ์ ์ฌํ์ฉ๋์ง๋ง, ์๋ชป ๋ถ๋ฆฌ๋ฐฐ์ถ ๋๋ฉด ๊ทธ๋๋ก ํ๊ธฐ๋ฌผ๋ก ๋ถ๋ฅ๋์ด ๋งค๋ฆฝ ๋๋ ์๊ฐ๋๊ธฐ ๋๋ฌธ์๋๋ค.

๋ฐ๋ผ์ ์ฐ๋ฆฌ๋ ์ฌ์ง์์ ์ฐ๋ ๊ธฐ๋ฅผ Detection ํ๋ ๋ชจ๋ธ์ ๋ง๋ค์ด ์ด๋ฌํ ๋ฌธ์ ์ ์ ํด๊ฒฐํด๋ณด๊ณ ์ ํฉ๋๋ค. ๋ฌธ์  ํด๊ฒฐ์ ์ํ ๋ฐ์ดํฐ์์ผ๋ก๋ ์ผ๋ฐ ์ฐ๋ ๊ธฐ, ํ๋ผ์คํฑ, ์ข์ด, ์ ๋ฆฌ ๋ฑ 10 ์ข๋ฅ์ ์ฐ๋ ๊ธฐ๊ฐ ์ฐํ ์ฌ์ง ๋ฐ์ดํฐ์์ด ์ ๊ณต๋ฉ๋๋ค.

์ฌ๋ฌ๋ถ์ ์ํด ๋ง๋ค์ด์ง ์ฐ์ํ ์ฑ๋ฅ์ ๋ชจ๋ธ์ ์ฐ๋ ๊ธฐ์ฅ์ ์ค์น๋์ด ์ ํํ ๋ถ๋ฆฌ์๊ฑฐ๋ฅผ ๋๊ฑฐ๋, ์ด๋ฆฐ์์ด๋ค์ ๋ถ๋ฆฌ์๊ฑฐ ๊ต์ก ๋ฑ์ ์ฌ์ฉ๋  ์ ์์ ๊ฒ์๋๋ค. ๋ถ๋ ์ง๊ตฌ๋ฅผ ์๊ธฐ๋ก๋ถํฐ ๊ตฌํด์ฃผ์ธ์! ๐

- **Input :** ์ฐ๋ ๊ธฐ ๊ฐ์ฒด๊ฐ ๋ด๊ธด ์ด๋ฏธ์ง์ bbox ์ ๋ณด(์ขํ, ์นดํ๊ณ ๋ฆฌ)๊ฐ ๋ชจ๋ธ์ ์ธํ์ผ๋ก ์ฌ์ฉ๋ฉ๋๋ค. bbox annotation์ COCO format์ผ๋ก ์ ๊ณต๋ฉ๋๋ค. (COCO format์ ๋ํ ์ค๋ช์ ํ์ต ๋ฐ์ดํฐ ๊ฐ์๋ฅผ ์ฐธ๊ณ ํด์ฃผ์ธ์.)
- **Output** : ๋ชจ๋ธ์ bbox ์ขํ, ์นดํ๊ณ ๋ฆฌ, score ๊ฐ์ ๋ฆฌํดํฉ๋๋ค. ์ด๋ฅผ submission ์์์ ๋ง๊ฒ csv ํ์ผ์ ๋ง๋ค์ด ์ ์ถํฉ๋๋ค. (submission format์ ๋ํ ์ค๋ช์ ํ๊ฐ๋ฐฉ๋ฒ์ ์ฐธ๊ณ ํด์ฃผ์ธ์

### Data ๊ตฌ์ฑ

- ์ด๋ฏธ์ง ๊ฐ์ : 9754์ฅ(train : 4883์ฅ, test : 4871์ฅ(50% public LB, 50% private LB))
- ๊ตฌ๋ถ Class : 10๊ฐ์ง (General trash, Paper, Paper pack, Metal, Glass, Plastic, Styrofoam, Plastic bag, Battery, Clothing)
- ์ด๋ฏธ์ง ํฌ๊ธฐ : 1024x1024
- annotation file : COCO format
    - images :
        - id: ํ์ผ ์์์ image ๊ณ ์  id, ex) 1
        - height: 1024
        - width: 1024
        - filename: ex) train/0002.jpg
    - annotations :
        - id: ํ์ผ ์์ annotation ๊ณ ์  id, ex) 1
        - bbox: ๊ฐ์ฒด๊ฐ ์กด์ฌํ๋ ๋ฐ์ค์ ์ขํ (xmin, ymin, w, h)
        - area: ๊ฐ์ฒด๊ฐ ์กด์ฌํ๋ ๋ฐ์ค์ ํฌ๊ธฐ
        - category_id: ๊ฐ์ฒด๊ฐ ํด๋นํ๋ class์ id
        - image_id: annotation์ด ํ์๋ ์ด๋ฏธ์ง ๊ณ ์  id

- ์ด๋ฏธ์ง ์์
![image](https://user-images.githubusercontent.com/77658029/137053907-a7c23950-5fef-4d56-9b1c-32d5da9f31d4.png)


### ํ๊ฐ ๋ฐฉ๋ฒ


- mAP score๋ก ํ๊ฐ
    + mAP : Object Detection์์ ์ฌ์ฉํ๋ ๋ํ์ ์ธ ์ฑ๋ฅ ์ธก์  ๋ฐฉ๋ฒ, Ground Truth ๋ฐ์ค์ Prediction ๋ฐ์ค๊ฐ IoU(Intersection Over Union, Detector์ ์ ํ๋๋ฅผ ํ๊ฐํ๋ ์งํ)๊ฐ 50์ด ๋๋ ์์ธก์ ๋ํด True๋ผ๊ณ  ํ๋จํฉ๋๋ค.
- Submission Format
    - Test ์ด๋ฏธ์ง ๋ด์๋ 1๊ฐ ์ด์์ ๊ฐ์ฒด ํฌํจ๋จ
    - ์ด๋ฏธ์ง ๋ณ๋ก ์์ธกํ ๊ฐ์ฒด์ ClassID, confidence_score, bbox(xmin, ymin, xmax, ymax) ๊ฐ๋ค์ space๋ก ์ด์ด ๋ถ์ฌ ์๋ ฅ
    - ๋ง์ฝ ์ฌ๋ฌ๊ฐ์ ๊ฐ์ฒด๋ฅผ ์์ธกํ๋ฉด space๋ก ๋๊ณ  ๊ณ์ ์ด์ด ๋ถ์ฌ์ค

- ๊ธฐํ ๊ท์น
    1. ์ธ๋ถ ๋ฐ์ดํฐ์ ์ฌ์ฉ ๊ธ์ง
    2. pretrained weight์ ๊ฒฝ์ฐ ImageNet, COCO, ํ์ค์นผ VOC Dataset์ผ๋ก ํ์ต๋ ๊ฒฝ์ฐ๋ง ํ์ฉ
    3. test data ์ง์  Labelingํ๋ ํ์ ๊ธ์ง


- Example of IoU  
![image](https://user-images.githubusercontent.com/77658029/137634593-01330886-88f3-46f1-ad02-94a90b09fad5.png)

- metric  
![image](https://user-images.githubusercontent.com/77658029/137634744-50099b32-78c0-46b7-8053-bdf6315748cb.png)

        
- Example of mAP50  
![image](https://user-images.githubusercontent.com/77658029/137634821-c186c507-21e7-472f-9fb9-8dcc6183da15.png)

        
- **Orange**
    - TP = 1, FP = 1
    - ์ด 2๊ฐ์ Orange ๋ฐ์ค ์ค ํ๋จ์ ๋ฐ์ค 1๊ฐ๋ ๊ฐ์ฒด๋ฅผ ์ detectionํ์์ต๋๋ค. (TP) 
        ์๋จ์ ๋ฐ์ค 1๊ฐ๋ Blue category์ ํด๋นํ๋ ๊ฐ์ฒด๋ฅผ Orange category๋ก ์์ธกํ์๊ธฐ ๋๋ฌธ์ ์๋ชป๋ detection์๋๋ค. (FP)
            
![image](https://user-images.githubusercontent.com/77658029/137634813-50e77a65-ec9d-4b7c-a867-ad75d38f83f4.png)

        
- **Blue**
    - TP = 2, FP = 1  
    - ์ด 3๊ฐ์ Blue ๋ฐ์ค ์ค ๋ ๊ฐ์ ๋ฐ์ค๋ ๊ฐ์ฒด๋ฅผ ์ detectionํ์์ต๋๋ค. (TP) 
        ์ฐ์ธก ํ๋จ์ ๋ฐ์ค๋ ๊ฐ์ฒด ์์น๋ฅผ ์ ํํ detectionํ์ง ๋ชปํ์ต๋๋ค. (FP)

![image](https://user-images.githubusercontent.com/77658029/137634804-ffe3e31d-9ae1-4bd0-950b-03b58ed3db2b.png)
        
- **mAP**

    ๋ชจ๋  ์ด๋ฏธ์ง์ ๊ฐ ํด๋์ค๋ณ AP ๊ณ์ฐ ํ, ํ๊ท ๋ด์ด ์ต์ข ์ ์๊ฐ ๊ตฌํด์ง๋๋ค.
            
![image](https://user-images.githubusercontent.com/77658029/137634795-bb8297f5-5c17-4c59-a699-1509ce57b933.png)
        





# ๋ฌธ์  ์ ์

- __์๊ฐํ__

![image](https://user-images.githubusercontent.com/77658029/137634832-f8d75e18-8a4f-49e9-b6ac-8d7c2a16afcc.png)

์ ์ด๋ฏธ์ง์์ ๋ณด์ด๋ ๋ฐ์ ๊ฐ์ด Class๋ณ bbox ์์ ๋ถ๊ท ํ์ด ์ฌํ๊ณ , ๋ฐฐํฐ๋ฆฌ์ ๊ฒฝ์ฐ ๋ฐ์ดํฐ ์๊ฐ 159๊ฐ(ํ๊ท  2,314 ๊ฐ)๋ฟ์๋๋ค.

<p align="center"><img src="https://i.imgur.com/DFKDvXF.png"></p>
<p align="center"><img src="https://i.imgur.com/H27mkEx.png"></p>


โ  Class Dependency
- ์ ๋จ์ง์ ๊ฒฝ์ฐ ์ผ๋ฐ ์ฐ๋ ๊ธฐ์ ์ข์ด ๋ ๊ฐ์ง๋ก annotation๋์ด ์์
- ์ ๋ฆฌ์ ํฌ๋ช ํ๋ผ์คํฑ์ด ๋งค๋ํ ํ๋ฉด, ํฌ๋ชํจ ๋ฑ ์ด๋ฏธ์ง์์์ ์ ์ฌํ ํน์ง์ ๋ณด์
- ์์ ๋ฌผ์ฒด(๋ธ๋์ด๋ ์ค ๋ฑ)์ ๋ํ background Error๊ฐ ์์ฃผ ๋์ ๊ฒฝํฅ์ ๋ณด์

โก Class Imbalance
- Figure 1์์ ์ฒ๋ผ Class๋ณ bbox ์์ ๋ถ๊ท ํ์ด ์ฌํจ
- ๋ฐฐํฐ๋ฆฌ์ ๊ฒฝ์ฐ, ๋ฐ์ดํฐ ์๊ฐ 159๊ฐ(ํ๊ท  2,314 ๊ฐ)๋ฟ

โข Various Dataset Environment
- Figure 2 ์ ๊ฐ์ด ๋ค์ํ ํ๊ฒฝ์์ ์ดฌ์๋ ์ด๋ฏธ์ง





# ๋ฌธ์ ์ ๋ํ ์คํ

## ์คํ ๊ฒฐ๊ณผ

### Issue ๋ฐ ์ฑ๋ฅ ๊ฐ์ ์ ์ํ ์๋

โ  Data Cleansing : Figure 3๊ณผ ๊ฐ์ train image์ ์๋ชป๋ labeling์ด๋ annotation์ ์์ ํด ์ฑ๋ฅ ํฅ์์ ์ํจ  
โก Data Augmentation : Class Imbalance ๋ฐ Image์ ์ดฌ์ ํ๊ฒฝ ๋ณด์์ ์ํ ๋ค์ํ Augmentation ๊ธฐ๋ฒ ์๋  
โ Randomfog, Blur, RandomBrightness, Cutmix, Mixup, Mosaic, Resize, normalization, MultiScale, RandomFlip  
โข Model Selection : Inductive bias๋ฅผ ์ต์ํํ๊ธฐ ์ํด ๋ค์ํ backbone model์ ์ฌ์ฉํ์ฌ ํ์ต  
โฃ Generalization : ์ฌ๋ฌ Augmentation๊ณผ Noise๋ฅผ ๋ฃ์ด ์๋,  TTA์๋  
โค Pseudo Labeling: ํ์ตํ ๋ชจ๋ธ๋ก test ๋ฐ์ดํฐ๋ฅผ inferenceํ ํ, ๊ทธ ๊ฒฐ๊ณผ๋ก ์ถ๊ฐ ํ์ต  
โฅ Ensemble : 1-stage model ๊ณผ 2-stage model์ Ensemble ํจ์ผ๋ก์ Robustํ ๋ชจ๋ธ ๊ฐ์  ์๋  
โฆ Binary Classification : ๊ฐ๊ฐ์ single class๋ฅผ binary classification ๋ก ํ์ต  


## ์คํ ํ์คํ ๋ฆฌ
<p align="center"><b>Wandb๋ฅผ ํ์ฉํ ์คํ ๊ด๋ฆฌ</b></p>

![](https://i.imgur.com/D44tEOj.png)

<p align="center">Yolo-V5 augmentation test</p>

![](https://i.imgur.com/o9KD9yU.png)

<p align="center">UniverseNet101 augmentation test</p>

![](https://i.imgur.com/h5pEg83.png)


## ๊ฒ์ฆ ์ ๋ต

- class๋ณ๋ก AP๋ฅผ ํ์ธํ๋ฉด์ ์ด๋ค ์ ํ์ ํ๋ฆฌ๊ณ  ์๋์ง ํ์
- Stratified validation๊ณผ Confusion Matrix๋ฅผ ํตํด ๋ถ๋ฅ ๋ชจ๋ธ ํ๊ฐ


<p align="center"><img src="https://i.imgur.com/xK3RTJ3.png"></p>


<br>
<br>


![image](https://user-images.githubusercontent.com/77658029/137634885-be71bffc-441b-4cb3-8360-e784a15e4424.png)





# Modeling ๋ฐ Ensemble

<table class="c76"><tbody><tr class="c54"><td class="c63" colspan="1" rowspan="1"><p class="c2"><span class="c0"><b>Model</b></span></p></td><td class="c82" colspan="1" rowspan="1"><p class="c2"><span class="c0"><b>๊ฐ์  ์๋</b></span></p></td><td class="c64" colspan="1" rowspan="1"><p class="c2"><span class="c0"><b>mAP</b></span></p></td></tr><tr class="c5"><td class="c17" colspan="1" rowspan="8"><p class="c2"><span class="c3">UniverseNet101</span></p></td><td class="c8" colspan="1" rowspan="1"><p class="c2"><span class="c3">Mixup</span></p></td><td class="c23" colspan="1" rowspan="1"><p class="c2"><span class="c3">0.573</span></p></td></tr><tr class="c5"><td class="c8" colspan="1" rowspan="1"><p class="c2"><span class="c3">Mosaic / Adam / batch_size 16 / LR 0.0001 / Cutmix Dataset</span></p></td><td class="c23" colspan="1" rowspan="1"><p class="c2"><span class="c3">0.419</span></p></td></tr><tr class="c5"><td class="c8" colspan="1" rowspan="1"><p class="c2"><span class="c3">Mosaic / Adam / batch_size 16 / LR 0.0001</span></p></td><td class="c23" colspan="1" rowspan="1"><p class="c2"><span class="c3">0.451</span></p></td></tr><tr class="c5"><td class="c8" colspan="1" rowspan="1"><p class="c2"><span class="c3">HueStauration / Adam / batch_size 16 / LR 0.0001</span></p></td><td class="c23" colspan="1" rowspan="1"><p class="c2"><span class="c3">0.619</span></p></td></tr><tr class="c5"><td class="c8" colspan="1" rowspan="1"><p class="c2"><span class="c3">&nbsp;RandomFog / batch_size 16 / LR 0.0001</span></p></td><td class="c23" colspan="1" rowspan="1"><p class="c2"><span class="c3">0.623</span></p></td></tr><tr class="c5"><td class="c8" colspan="1" rowspan="1"><p class="c2"><span class="c3">RandomBrightness / batch_size 16 / LR 0.002</span></p></td><td class="c23" colspan="1" rowspan="1"><p class="c2"><span class="c0"><b>0.624</b></span></p></td></tr><tr class="c5"><td class="c8" colspan="1" rowspan="1"><p class="c2"><span class="c3">Blur, RandomFog, RandomBrightness, Mixup / Adam / batch_size 16 / LR 0.0001 /Data Cleaning</span></p></td><td class="c23" colspan="1" rowspan="1"><p class="c2"><span class="c3">0.613</span></p></td></tr><tr class="c5"><td class="c8" colspan="1" rowspan="1"><p class="c2"><span class="c3">Data cleaning / RandomBrightness / batch_size 16 / LR 0.002</span></p></td><td class="c23" colspan="1" rowspan="1"><p class="c2"><span class="c3">0.590</span></p></td></tr><tr class="c5"><td class="c17" colspan="1" rowspan="5"><p class="c2"><span class="c3">Swin-T,S</span></p></td><td class="c8" colspan="1" rowspan="1"><p class="c2"><span class="c3">Swin-T / Adam / batch_size 4 / LR 0.0001 </span></p></td><td class="c23" colspan="1" rowspan="1"><p class="c2"><span class="c3">0.523</span></p></td></tr><tr class="c5"><td class="c8" colspan="1" rowspan="1"><p class="c2"><span class="c3">Swin-T / MultiScale / Adam / batch_size 4 / LR 0.0001</span></p></td><td class="c23" colspan="1" rowspan="1"><p class="c2"><span class="c3">0.550</span></p></td></tr><tr class="c5"><td class="c8" colspan="1" rowspan="1"><p class="c2"><span class="c3">Swin-S / MultiScale / AdamW / batch_size 4 / LR 0.0001</span></p></td><td class="c23" colspan="1" rowspan="1"><p class="c2"><span class="c3">0.561</span></p></td></tr><tr class="c5"><td class="c8" colspan="1" rowspan="1"><p class="c2"><span class="c3">Swin-S / MultiScale, Mixup / AdamW / batch_size 4 / LR 0.0001</span></p></td><td class="c23" colspan="1" rowspan="1"><p class="c2"><span class="c3">0.571</span></p></td></tr><tr class="c5"><td class="c8" colspan="1" rowspan="1"><p class="c2"><span class="c3">Swin-S / Randomfog, RandomBrightnessContrast, ShiftScaleRotate, MultiScale, Mixup / AdamW / batch_size 4 / LR 0.0001</span></p></td><td class="c23" colspan="1" rowspan="1"><p class="c2"><span class="c0"><b>0.586</b></span></p></td></tr><tr class="c5"><td class="c17" colspan="1" rowspan="5"><p class="c1"><span class="c3"></span></p><p class="c2"><span class="c3">Yolo-V5</span></p></td><td class="c8" colspan="1" rowspan="1"><p class="c2"><span class="c3">baseline (Yolo v5x6 default) / 300 epoch</span></p></td><td class="c23" colspan="1" rowspan="1"><p class="c2"><span class="c0"><b>0.586</b></span></p></td></tr><tr class="c5"><td class="c8" colspan="1" rowspan="1"><p class="c2"><span class="c3">label smoothing (T=0.05) / 300 epoch</span></p></td><td class="c23" colspan="1" rowspan="1"><p class="c2"><span class="c3">0.583</span></p></td></tr><tr class="c5"><td class="c8" colspan="1" rowspan="1"><p class="c2"><span class="c3">single class / 300 epoch </span></p></td><td class="c23" colspan="1" rowspan="1"><p class="c2"><span class="c3">0.008</span></p></td></tr><tr class="c5"><td class="c8" colspan="1" rowspan="1"><p class="c2"><span class="c3">random fog / 50 epoch</span></p></td><td class="c23" colspan="1" rowspan="1"><p class="c2"><span class="c3">0.573</span></p></td></tr><tr class="c5"><td class="c8" colspan="1" rowspan="1"><p class="c2"><span class="c3">pseudo labeling (conf_threshold=0.6) / train data(10epoch x 3), pseudo data(10epoch x 2) ๋ฒ๊ฐ์๊ฐ๋ฉฐ ํ์ต / pseudo data ํ์ต์ obj loss ์ ์ธ / 50 epoch</span></p></td><td class="c23" colspan="1" rowspan="1"><p class="c2"><span class="c3">0.559</span></p></td></tr><tr class="c35"><td class="c17" colspan="1" rowspan="3"><p class="c2"><span class="c13">PVTv2-B3</span></p></td><td class="c8" colspan="1" rowspan="1"><p class="c2"><span class="c13">baseline epoch 30 / batch size 4 / scheduler step / LR 0.002 / </span><span class="c97">fp16</span></p></td><td class="c23" colspan="1" rowspan="1"><p class="c2"><span class="c3">0.541</span></p></td></tr><tr class="c35"><td class="c8" colspan="1" rowspan="1"><p class="c2"><span class="c3">batch size 3 / LR 0.0001 / &nbsp;Adam / score_thr = 0</span></p></td><td class="c23" colspan="1" rowspan="1"><p class="c2"><span class="c0"><b>0.573</b></span></p></td></tr><tr class="c35"><td class="c8" colspan="1" rowspan="1"><p class="c2"><span class="c3">batch size 2 / LR 0.0001/ mixup, RandomFog, blur, randbright / Adam / Data cleaning</span></p></td><td class="c23" colspan="1" rowspan="1"><p class="c2"><span class="c3">0.526</span></p></td></tr></tbody></table>

๋ ์์ธํ ๊ธฐ๋ก์ [๋๋ณด๊ธฐ...](https://docs.google.com/spreadsheets/d/1xw11I8pUZY8CGaE0jXeE4KGokvK-zbpxHdKKYsyt_SI/edit#gid=265349216)

## ์ต์ข Ensemble๋ ๋ชจํ
<p align="center"><img src="https://i.imgur.com/2BvTb4c.png"></p>
๊ฐ model๋ณ๋ก ๊ฐ์ฅ LB score๊ฐ ์ข์๋ ๋ฒ์  5๊ฐ๋ฅผ Ensembleํ์ฌ ์ต์ข ๋ชจ๋ธ์ ์์ฑ  

# ํ๊ณ 

## ์ํ๋ ์ 
- mmdetection ๋ผ์ด๋ธ๋ฌ๋ฆฌ๋ฅผ ํ์ฉํ์ฌ object detection์ ์ ๋ฐ์ ์ธ task๋ฅผ ์ํํด ๋ณผ ์ ์์์ต๋๋ค.
- mAP, NMS, WBF๋ฑ object detection๊ณผ ๊ด๋ จ๋ ์ฉ์ด๋ค์ ๋ํด ๊ณต๋ถ ํ  ์ ์์์ต๋๋ค.
- object detection์ ๊ด๋ จ๋ ๋ค๋ฅธ ๋ํ๋ค(Kaggle, Dacon)์ ์ฐพ์๋ณด๊ณ  ๋ํ์์ ํ์ฉ๋ ๊ธฐ๋ฒ๋ค์ ์ด๋ฒ ๋ํ์ ์ ์ฉ์์ผ ๋ด์ผ๋ก์จ ์ฑ๋ฅ ๋ณํ๋ ์ค์ ๋ก ์ ์ฉ์์ผฐ์ ๋์ ์ด๋ ค์ ๋ฑ์ ๊ฒฝํํด๋ณด๊ณ  ์ด์ ๊ด๋ จ๋ ๋ด์ฉ์ผ๋ก ํ์๋ค๊ณผ ์ํตํ์ฌ ์ฑ์ฅ์ ๋๋ชจํ์ต๋๋ค.
- mmdetection ์ธ์ yolov5, Universenet๊ณผ ๊ฐ์ ๋ค๋ฅธ ๋ผ์ด๋ธ๋ฌ๋ฆฌ๋ฅผ ์ฌ์ฉํด ๋ณด๋ ๋ฑ  ๋ค์ํ ์๋๋ฅผ ํ์์ต๋๋ค.

![](https://i.imgur.com/LVSLYC5.png)


## ์์ฌ์ ๋ ์ 

- mmdetection๊ณผ ๊ด๋ จ๋ ๋ค์ํ ๋ผ์ด๋ธ๋ฌ๋ฆฌ๋ฅผ ์ฒ์ ํ์ฉํจ์ ์ด๋ ค์์ด ์์ด์ ๋ด๊ฐ ์ํ๋ ๋ชจ๋ธ์ ๊ตฌํํ๋๋ฐ ์๊ฐ์ด ์ค๋ ๊ฑธ๋ ธ์ต๋๋ค. ์๋กญ๊ฒ ๋ฐฐ์๊ฐ๋ค๋ ๋๋๋ณด๋ค mmdetection ๋ผ์ด๋ธ๋ฌ๋ฆฌ๋ฅผ ํตํด ๊ธฐ๊ณ์ ์ผ๋ก ํ๋ผ๋ฏธํฐ ํ๋์ ํ์ฌ ์ฑ๋ฅ์ ํฅ์์ํจ๋ค๋ ๋๋์ด ๊ฐํด์ ์์ฌ์ ์ต๋๋ค.
- object detection์ ์ฒ์ ์๋ฌธํจ์ ์์ด์ ๋ค์ํ ํ์คํธ๋ฅผ ํด๋ด์ผ ํ๋๋ฐ ๊ฒฐ๊ณผ๋ฅผ ๋ณด๊ธฐ๊น์ง์ ์๊ฐ์ด ๋๋ฌด ์ค๋ ๊ฑธ๋ ธ๊ณ , ์ด๋ก ์ธํด ๋ค์ํ ์คํ์ ๊ธฐ๊ฐ ๋ด์ ํด๊ฒฐํ์ง ๋ชปํ์ต๋๋ค.
- test dataset๊ณผ ์ ์ฌํ validation dataset์ ์ฐพ๊ธฐ ์ด๋ ค์ ์ฐ๊ตฌ๊ฐ ์งํ๋ ์๋ก model์ ๊ฐ์ ์ํค๊ธฐ ์ํ ๋๋ ทํ ํ๋จ์ ๊ทผ๊ฑฐ๊ฐ ๋ถ์กฑํ์ต๋๋ค.
- LB mAP๋ฅผ ๋์ด๊ธฐ ์ํด์๋ bounding box๋ฅผ ๋ง์ด ์น๋ ๊ฒ์ด ํจ๊ณผ๊ฐ ์์๊ณ  ๊ทธ๋ฌ๋ค ๋ณด๋ ๋์ถ๋ ๊ฒฐ๊ณผ๋ฅผ ํ์ธํ์๋ ์ด๊ฑธ detectionํ๋ค๊ณ  ํ  ์ ์๋์ง ์๋ฌธ์ด ๋ค์๊ณ  mAP๊ฐ ํ๊ฐ ์งํ๋ก ์ ํฉํ๊ฐ ์๋ฌธ์ด ๋ค์์ต๋๋ค.


<table align="center">
    <tr>
        <td><img width="340" src="https://i.imgur.com/IjbLt9r.jpg" /><br/>
            <p align='center'> mAP 0.672</p>
        </td>
        <td><img width="300" src="https://i.imgur.com/OuI6iNY.png" /><br/>
            <p align='center'> mAP 0.482</p>
        </td>
    </tr>
</table>

## ํ์๋ค์ ํ๋ง๋

- ํ๊ฑด์ฐ : ์ธ๋ถ ๋ผ์ด๋ธ๋ฌ๋ฆฌ๋ฅผ ์ฌ์ฉํ  ๋๋ ํญ์ ๊ฒ์ฆํ๊ณ  ์ฌ์ฉํด์ผํ๋ค๋ ์ ์ ๋ค์ ํ๋ฒ ๋๋ผ๊ฒ ๋์์ต๋๋ค.
- ๋ฐ์คํ : ์ฒซ object detection ๋ํ๋ฅผ ๊ฒฝํํจ์ผ๋ก์ ๋ง์ ์ด๋ ค์์ด ์์์ผ๋ ํ์๋ค๊ณผ์ ์ํต์ผ๋ก ์ ํด๊ฒฐํด๋๊ฐ๊ณ , ์์ผ๋ก๋ ์ด๋ฐ object detection task์ ๋ํ ๊ฐ์ ์ป์ ์ ์์ด์ ์ข์์ต๋๋ค. ํ์ ๋ชจ๋ ๋ํ๋ฅผ ์ด์ฌํ ์งํํด์ฃผ๊ณ  ๊ฐ์ด ๊ณ ๋ฏผํด์ฃผ์ด์ ๊ฐ๋์ด์์ด์~!
- ํ์ํ : ๋ผ์ด๋ธ๋ฌ๋ฆฌ์ ์ต์ํด์ง๋๋ฐ ์๊ฐ์ด ์ค๋ ๊ฑธ๋ ค ๋ ๋ง์ ์คํ์ ๋ชปํ๋๋ฐ ๋ค์ ๋ํ์๋ ๋ ๋ง์ ์๋๋ฅผ ํด๋ณด๊ณ  ์ถ์ต๋๋ค!
- ํฉ์์ : ์ด์  ๊ฐ์ ์ก์๊ฐ๋ ๊ฒ ๊ฐ์ต๋๋ค. ๋ค์ ๋ํ ๋๋ ๋ ์๊ฐ๋ด์๋ค.
- ๋ฐ๋ฒ์ : ๋๋ฒ์งธ competition์ด์ง๋ง ์์ง๋ ๋ถ์กฑํ๊ฒ ๋ง๋ค๊ณ  ๋๋ผ๋ ๋ํ์์ต๋๋ค. ์์ผ๋ก๋ ์กฐ๊ธ ๋ ์ฒด๊ณ์ ์ผ๋ก ๋ํ๋ฅผ ์งํํด์ผ๊ฒ ๋ค๋ ๊ฑธ ๊นจ๋ฌ์์ต๋๋ค.
- ์ํฌ์ : ํ์์ ์ค์ํ๋ค๊ณ  ์๊ฐํด ์๋๋ฐ ๋ค์ํ ๋ผ์ด๋ธ๋ฌ๋ฆฌ๋ก ์คํ์ ์งํํด์ผ ํ๋ ์ํฉ์์๋ ์ฐ์ ์ ํ์ง ์์ ํ์๋ ์๋ค๊ณ  ๊นจ๋ซ๊ฒ ๋์๊ณ , ์ ๋ฐ์ ์ธ detection task๋ฅผ ์์๊ฐ ์ ์์๋ค๋ ์ ์์ ์๋ฏธ ์์ง๋ง ๋ผ์ด๋ธ๋ฌ๋ฆฌ ํ๋๋ง ํ๋ค ๋๋ฌ๋ค๊ณ  ์๊ฐ์ด ๋ค๊ธฐ๋ ํด์ ์์ฌ์ด ๋ง์์ด ๋จ์ต๋๋ค. ๋ชจ๋ ์๊ณ  ๋ง์ผ์จ์ด์!
- ์กฐํ์ : Object detection ๋ชจ๋ธ๋ค์ ์ง์  ํ์ตํด๋ณผ ์ ์์ด์ ์ข์์ผ๋, ๋ชจ๋ธ ๊ตฌ์กฐ์ ๋ํด ๊น์ด์๊ฒ ํ์ํ์ง ๋ชปํ ๋ฑ์ ์์ฌ์๋ ๋ง์ด ๋จ๋ ๋ํ์์ต๋๋ค. ํ์๋ถ๋ค ๋ชจ๋ ์๊ณ ๋ง์ผ์จ์ด์!


<br>

**๐reference**
- boostcourse AI tech
- [naver connect - ์ฌํ์ฉ ์ฐ๋ ๊ธฐ ๋ฐ์ดํฐ์ / CC BY 2.0](https://stages.ai/competitions/76/overview/description)

<br>

```
๐ก ์์  ํ์ํ ๋ด์ฉ์ ๋๊ธ์ด๋ ๋ฉ์ผ๋ก ์๋ ค์ฃผ์๋ฉด ๊ฐ์ฌํ๊ฒ ์ต๋๋ค!๐ก 
```

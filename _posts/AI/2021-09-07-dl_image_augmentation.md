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

title: "Image Data Augmentation_(cv2,PIL)"
excerpt: "about : Image Augmentation"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - ai_dlbasic
tags:
  - [augmentation]
date: 2021-09-07
last_modified_at: 2021-09-07
---

<br>

# Image Data Augmentation

<br><br><br>

## 왜 Data Augmentation이 필요할까?

- image Data의 경우는 실제 Data와 다름
- 대부분의 Dataset은 **특정 시점, 각도**에 따라서 한정된 Data를 가지게 됨
- 이런 부분들 때문에 Training 할 Dataset과 현실속 실제하는 전체 Data와 Gap이 발생하게 됨

<p align="left">
    <img src="https://user-images.githubusercontent.com/77658029/132330568-54fc28bc-f174-44e6-a0c9-7c9ed1b3c670.png">
</p>

![image](https://user-images.githubusercontent.com/77658029/132330568-54fc28bc-f174-44e6-a0c9-7c9ed1b3c670.png)


**🔑 Augmentaion 사용하여 Training Dataset과 Real Data사이의 Gap을 줄여줌**

<p align="left">
    <img src="https://user-images.githubusercontent.com/77658029/132330793-4ccc1fd1-fd66-40b4-94fe-009203895112.png">
</p>

![image](https://user-images.githubusercontent.com/77658029/132330793-4ccc1fd1-fd66-40b4-94fe-009203895112.png)

<br><br><br>

## Augmentation 종류

- Crop, Affine(Shear), Brightness, Perspective, Rotate 등을 활용하여 Training Dataset 내 Image를 변환하여 Data 수를 늘리는 효과를 줄 수 있음

<p align="left">
    <img src="https://user-images.githubusercontent.com/77658029/132335531-4b31f875-fb9c-4025-ad7c-88768ff7df5b.png">
</p>


![image](https://user-images.githubusercontent.com/77658029/132335531-4b31f875-fb9c-4025-ad7c-88768ff7df5b.png)


<br><br><br>


## Image handling

<br><br>

### CV2

- 설치 : `pip install opencv-python`
- import : `import cv2`
- 불러오기 : `cv2.imread("image 경로")` 형식으로 경로 기반으로 Image를 불러옴
- 불러온 image는 `ndarray`타입으로 여러 연산이 가능하고, matplotlib.pyplot 라이브러리를 이용하여 img를 출력할 수 있음
- image의 사이즈도 numpy의 shape 함수를 활용하여 확인 가능함
- cv2의 출력은 BGR 순서로 이루어져 있기 때문에, RGB로 변경해야 원본 image를 확인 할 수 있음

**📰code**
```python
import cv2
import matplotlib.pyplot as plt
img = cv2.imread("cat.png")
img = cv2.cvtColor(img,cv2.COLOR_BGR2RGB)

print(type(img),img.shape)
# numpy.ndarray, shape : (height, width, channel)
plt.imshow(img)
```
**🔍result** RGB로 변경 시

<p align="left">
    <img src="https://user-images.githubusercontent.com/77658029/132369764-f63529d5-2ec3-412f-9547-b5fb49ad4bc0.png">
</p>

<br>

**🔍result** BGR로 출력 시, `# img = cv2.cvtColor(img,cv2.COLOR_BGR2RGB)`

<p align="left">
    <img src="https://user-images.githubusercontent.com/77658029/132369946-9d64f39f-87c0-4e8f-a597-69ea23e04788.png">
</p>

<br><br>

#### Image crop

- 별도의 함수 필요없이 numpy slicing을 통해 Crop 할 수 있음

**📰code**
```python
import cv2
import matplotlib.pyplot as plt
img = cv2.imread("cat.png")
img = cv2.cvtColor(img,cv2.COLOR_BGR2RGB)
img=img[200:700,600:1200,:]
plt.imshow(img)
```
**🔍result**

<p align="left">
    <img src="https://user-images.githubusercontent.com/77658029/132370340-0e0aeb05-2e9f-4f90-87b2-b1c502c2d7eb.png">
</p>

<br><br>

#### Image save

- `imwrite` 함수를 활용해 image를 저장할 수 있음

**📰code**
```python
import cv2

img = cv2.imread("cat.png")

x, y = 600, 200
dx, dy = 600, 500
crop_img = img[y:y+dy, x:x+dx,:]

cv2.imwrite("crop_img.png", crop_img)
```
**🔍result**

<p align="left">
    <img src="https://user-images.githubusercontent.com/77658029/132371849-e14743bb-05f6-43d4-baf3-7cd194fbe75a.png">
</p>

<br><br>

#### cv2 지원 image format

- Windows bitmap (bmp)
- Portable image formats (pbm, pgm, ppm)
- Sun raster (sr, ras)
- JPEG (jpeg, jpg, jpe)
- JPEG 2000 (jp2)
- TIFF files (tiff, tif)
- Portable network graphics (png)


<br><br><br>

### PIL(Python Imaging Library)

- 설치 : `pip install pillow`
- import : `from PIL import Image`
- 불러오기 : `Image.open('image 경로')`형식으로 경로 기반으로 Image를 불러옴
- 불러온 image는 `PIL.PngImagePlugin.PngImageFile` 타입으로 PIL package에 있는 연산으로 접근하거나 조작할 수 있음

**📰code**
```python
from PIL import Image

img = Image.open('cat.png')
img.show()
```
**🔍result**

<p align="left">
    <img src="https://user-images.githubusercontent.com/77658029/132358146-e03faaa5-cb7d-4f10-9129-d93582f7130d.png">
</p>

<br><br>

#### Image size 확인

**📰code**
```python
from PIL import Image

img = Image.open('cat.png')
img.size
```
**🔍result**
```
(1280, 960)
```

<br><br>

#### Image crop 

- crop 함수를 이용하여 이미지를 잘라낼 수 있음
- 필요한 좌표는 사각형의 왼쪽 위, 오른쪽 아래 좌표가 필요함 
- `[ x1, y1, x2, y2]` -> x1, y1 : 좌측 상단 좌표,  x2, y2 : 우측 하단 좌표

**📰code**
```python
from PIL import Image

img = Image.open('cat.png')
crop_img = img.crop([600,200,1200,700])
crop_img.show()
```
**🔍result**

<p align="left">
    <img src="https://user-images.githubusercontent.com/77658029/132364857-9e3ef046-da79-4ee7-a4c9-04393e6a0044.png">
</p>


<br><br>

#### Image with drawBox

- ImageDraw Package를 활용하여 도형을 넣을 수 있음

**📰code**
```python
from PIL import Image, ImageDraw

img = Image.open('cat.png')

draw = ImageDraw.Draw(img)
draw.rectangle([100,200,800,700], outline="blue", fill = "blue")
display(img)
```
**🔍result**

<p align="left">
    <img src="https://user-images.githubusercontent.com/77658029/132366222-c34a1d55-bc72-4f6f-97ec-27e2b263f2c5.png">
</p>

<br><br>

#### Image to Numpy array

- image를 ndarray 형태로 바꿀 수 있음
- numpy로 바꿔서 이후 plt을 통해 image를 그릴수도 있고 여러 image를 합치거나 brightness를 변경할 수 있음
- cv2도 ndarray형식으로 출력이 나오기 때문에 연산의 자유도가 높아짐

**📰code**
```python
import numpy as np
from PIL import Image
import matplotlib.pyplot as plt

img = Image.open('cat.png')
num_img = np.array(img)
print(type(num_img), num_img.shape)
plt.imshow(num_img)
```
**🔍result**
<p align="left">
    <img src="https://user-images.githubusercontent.com/77658029/132367384-30b29d36-9fcb-40ca-beaf-d6be3e31db4a.png">
</p>

<br><br>

####  Numpy array to Image (cv2 -> PIL)

- ndarray에서 PIL형태로 변경할 수 있음
- cv2가 ndarray형식이기 때문에 CV2 -> PIL 형식으로 변환으로 생각할 수 있음

**📰code**
```python
import cv2
import matplotlib.pyplot as plt
from PIL import Image
img = cv2.imread("cat.png")
img = cv2.cvtColor(img,cv2.COLOR_BGR2RGB)

pil_Image = Image.fromarray(img)
pil_Image.show()
```
**🔍result**
<p align="left">
    <img src="https://user-images.githubusercontent.com/77658029/132371037-539806e9-95ef-4ad8-99fa-4eb30fe5599c.png">
</p>

<br><br>

#### Image save

- image 저장하기

**📰code**
```python
from PIL import Image

img = Image.open('cat.png')
img.save("저장할이름.jpg")
```
<p align="left">
    <img src="https://user-images.githubusercontent.com/77658029/132367792-576e1317-fb4f-42e6-bd46-e3cd56183c5e.png">
</p>

<br><br>

#### PIL 지원 image format 

|지원여부|Image Format|
|---|---|
|읽기/쓰기 모두 지원|BMP, DIB, EPS, GIF, ICNS, ICO, IM, JPEG, JPEG 2000, MSP, PCX, PNG, PPM, SGI, SPIDER, TGA, TIFF, Webp|
|읽기만 지원|BLP, CUR, DCX, DDS, FLI, FLC, FPX, FTEX, GBR, GD, IMT, IPTC/NAA, MCIDAS, MIC, MPO, MCD, PIXAR, PSD, WAL, WMF, XPM|
|쓰기만 지원|PALM, PDF, XV Thumbnails|

<br><br><br>

**📌reference**
- boostcourse AI tech
- [앱피아_PIL](https://appia.tistory.com/353)
- [new_challenge PIL,CV2](https://soyoung-new-challenge.tistory.com/112)

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

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

title: "[boostcourse] Day82 학습기록_팀명뭘로하조"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - boostcourse
tags:
  - []
date: 2021-12-01
last_modified_at: 2021-12-01
---

## 학습 내용

- Optuna 통해서 돌리는데, WandB Sweep랑 연동 실패,, 원인 파악이 안되어 
- Optuna로 best f1 model 저장하는 방식으로 진행

<br>

## 피어세션 👨‍👨‍👦‍👦 👨‍👨‍👦

- 최종프로젝트

  - 데이터 : aihub K-pop 안무 영상 ([https://aihub.or.kr/aidata/34116](https://aihub.or.kr/aidata/34116))

- 목표 : **춤 영상에 맞춰서 device를 통해 실시간으로 내 모습과 매칭시켜서 비교 측정**

([https://github.com/HwangToeMat/PoseEstimation_Scoring-Your-Video](https://github.com/HwangToeMat/PoseEstimation_Scoring-Your-Video))

- 참고 Github 
    
    ([https://github.com/edvardHua/PoseEstimationForMobile](https://github.com/edvardHua/PoseEstimationForMobile)
    ([https://github.com/tucan9389/PoseEstimation-CoreML](https://github.com/tucan9389/PoseEstimation-CoreML))
    ([https://www.youtube.com/watch?v=HSZDcLWZB1k](https://www.youtube.com/watch?v=HSZDcLWZB1k))
    ([https://www.youtube.com/c/NicholasRenotte/videos](https://www.youtube.com/c/NicholasRenotte/videos))
    
- Data 전처리? aihub 에는 annotation 이 절대값으로 나와있고 pipeline 에는 0-1값
- 모델 구축 : mediapipe ⇒ mediapipe를 사용한다면 모델/성능 개선은 할 수 없음!
- Metric 구성 및 성능 평가: DTW(Dynamic Time Warping), Scaling, normalize
    - ([https://www.kci.go.kr/kciportal/ci/sereArticleSearch/ciSereArtiView.kci?sereArticleSearchBean.artiId=ART002672820](https://www.kci.go.kr/kciportal/ci/sereArticleSearch/ciSereArtiView.kci?sereArticleSearchBean.artiId=ART002672820))
- 서빙 웹
- 정리

**Video inpainting 을 왜 그만 두었는가**

- 글씨 영상 데이터를 구축해야 함
- 서빙이 불가능 할 것 같고, 그렇다고모델 성능 개선을 하는건 논문을 쓰는게 나을지도
- 현실적으로 3주안에 불가능하다고 생각함
- Video inpainting 관련 레퍼런스 ([https://github.com/1900zyh/Awesome-Image-Inpainting#video-inpainting](https://github.com/1900zyh/Awesome-Image-Inpainting#video-inpainting))
- image inpainting (https://github.com/ewrfcas/MST_inpainting)
- 이것은 왜 안돌아가는가([https://www.zspapapa.com/zllrunning/video-object-removal](https://www.zspapapa.com/zllrunning/video-object-removal))


<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

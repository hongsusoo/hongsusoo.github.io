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

title: "AI Model의 경량화 필요성"
excerpt: "about : 경량화"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - AI ETC
tags:
  - [경량화]
date: 2021-11-22
last_modified_at: 2021-11-22
---

<br>

# 경량화 목적

- On Device, On Cloud(server)로 AI 가 돌아가는 환경에 제약이 많아짐
- On device limitation
    - power usage(battery)
    - RAM Memory Usage
    - Storage
    - Computing power
- On Cloud limitation
    - Latency
    - Throughput
    - e.g. 한 요청의 소요시간, 단위 시간당 처리 가능한 요청수
    
❕❓ 만약 같은 자원(=돈, 시간)으로 더 적은 Power usage, Memory Latency와 더 큰 Throughput이 가능하다면

현재 AI 모델은 2012년 이후 3,4 개월마다 두배로 증가해옴

**경량화는?**

- 모델의 연구와 별개로, 산업에 적용되기 위한 필수 과정
- 요구조건(하드웨어 종류, Latency제한, 요구 Throughput, 성능)들 간의 Trade-off를 고려하여 모델 경량화/최적화를 수행

## 경량화 분야

### 네트워크 구조관점

- Efficient Architecture design(+AutoML, NAS(Neural Architecture Search))
    - Software의 새로운 단계 : Software 1.0 - 사람이 짜는 모듈, Software 2.0 - 알고리즘이 찾는 모듈
        - 사람의 직관보다 상회하는 성능의 모듈들의 찾아낼 수 있음
- Network Pruning - 활발한 연구가 되고 있지만, 일반화 어려움
    - 중요도가 낮은 파라미터 제거(좋은 중요도를 정의하는 것이 하나의 토픽)
    - Structured Pruning : 그룹단위로 Pruning하는 기법(Channel/filter,Layer 전체를 Pruning)
    - Unstructured Pruning : 파라미터 각각을 독립적으로 Pruning하는 기법, 내부의 행렬이 점점 Sparse해짐, Sparse computation에 최적화된 S/W혹은 H/W에 적합한 기법
- Knowledge Distillation - 활발한 연구가 되고 있지만, 일반화 어려움
    - 학습된 큰 네트워크를 작은 네트워크의 학습보조로 이용하는 방법
    - 단순 모델 학습시에는 Hard target(Ground Truth Label)과 비교하여 학습하지만, Knowledge distillation 방법을 쓸경우 기 학습된 큰 모델의 Soft target과 Hard Target을 함께 학습할 수 있기 때문에 더 많은 정보로 학습할 수 있음
- Matrix/Tensor Decomposition - 수학적으론 복잡하나, 간단한 구현으로 좋은 효과가 있음
    - 하나의 Tensor를 작은 Tensor들의 조합으로 표현하는 것
    ![image](https://user-images.githubusercontent.com/77658029/142868840-213d8e5b-79cb-4fd6-a7b2-1e07a7d4400d.png)

### Hardware 관점

- Network Quantization
    - 양자화 : 일반적인 Float32 데이터를 int8, Float16등 작은 데이터 타입으로 변환하여 연산 수행후 복원
    - Quantization Error가 발생하고, 일반적으로 성능이 떨어짐
- Network Compiling
    - 학습이 완료된 Network를 Deploy하려는 Target Hardware에서 Inference가 가능하도록 Compile진행
    - 사실상 **속도에 가장 큰 영향**을 주는 기법
    -  e.g. TensorRT(NVIDIA), Tflite(Tensorflow), TVM(apache), ...
    - 각 Library마다 성능차이가 발생(tf의 경우 약 200개의 Rule로 최적화를 진행하게됨)
    - 하지만, Framework와 Hardware backends 사이의 수많은 조합이 있어 generalized 하기 어려움(Layer Fusion 조합에 따라 성능 차이가 발생)

<br><br><br>

**📌reference**
- boostcourse AI tech

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

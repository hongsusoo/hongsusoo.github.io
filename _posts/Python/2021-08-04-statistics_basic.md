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

title: "[AI basic] 통계론(statistics)"
excerpt: "about : python"
toc: true
toc_sticky: true
toc_label: "Label"
categories:
  - AI
tags:
  - [python, AI Math]
date: 2021-08-04
last_modified_at: 2021-08-04
---
<br>

# 통계학

- 많은 경우 데이터의 정확한 확률분포를 알고있는 경우는 많지 않음
- 그러기 때문에 통계학적인 가정위에서 Data의 확률분포를 추정(inference)하기 위해 통계학을 사용함
- 결국 어떤 확률분포를 사용해야하는지.. 선택의 문제
- 유한한 개수의 데이터로 모집단을 정확하게 알아내는건 불가능함 → 근사적 확률분포로 추정해야함
- 확률론과 마찬가지로 데이터와 추정방법의 불확실성을 고려하여 예측의 위험(risk)을 최소화 하는 방향으로

**💡 어떤 확률분포를 사용해야할까 ❓**

![image](https://user-images.githubusercontent.com/77658029/128618642-f072c2c1-e070-491d-a9ed-3f1991c363c1.png)

<br>

## 모수(parameter)

- 모수란 모집단을 표현해주는 데이터를 의미(모평균, 모표준편차, 모분산 등)
- 모수는 결국 모집단을 표현해주는 지표!
- 데이터에 맞는 적절한 모수를 구하는 것이 숙제
- 확률분포를 추정할 때, 두 가지 방법이 있는데 모수적방법론과 비모수적(non-parametric) 방법론이 있다

💡 모수적(parametric) 방법론

- 선험적(a priori)으로 확률분포를 미리 가정하고 모수를 추정하는 방법론
- 만약 정규분포라 가정했으면
    모수 → 평균, 분산 선정
    데이터를 학습시켜 모수를 추정(평균, 분산)
    
💡 비모수적(non-parametric) 방법론

- 모수가 없는게 아니라, 모수를 미리 정해두지 않고 모델의 구조나 모수의 개수를 유연하게 변경하며 추정하는 방법론
- 모수가 유기적으로 변하는것, 가정을 따로 하지 않음

<br>

## 확률분포 가정하기 

- 우선 히스토그램을 통해 모양을 관찰함
- 만약 데이터가 2개의 데이터만 갖음 -> 베르누이,이항분포
- n개의 이산적인 값을 가지는 경우 -> 카테고리 분포
- 데이터가 [0,1]사이에서 값을 가지는 경우 -> 베타분포
- 데이터가 0이상의 값을 가지는 경우 -> 감마분포, 로그정규분포
- 데이터가 R전체에서 값을 가지는 경우 -> 정규분포, 라플라스분포

💡 기계적으로 확률분포를 가정하면 안되고, 데이터를 생성하는 원리를 먼저 고려하는것이 원칙!

💡 모수 추정후 통계적 검정까지 이뤄져야함

<br>

## 데이터로 모수를 추정해보자

- 정규분포의 모수는 평균 μ,분산 $σ^2$
- 표본분산을 구할때 N-1로 나눠주면 불편(unbiased)추정량을 구할 수 있다
- N-1은 자유도와 관련이 있는데, 자유도는 독립변수의 개수
- 불편추정량 -> 편의가 없는 추정량

![image](https://user-images.githubusercontent.com/77658029/128619511-26157340-a1e5-421f-a242-bb69b2bdd0ae.png)

통계량의 확률분포를 표집분포(sampling distribution)라 부르며, 특히 표본평균의 표집분포는 N이 커질수록 정규분포 $\mathscr N(\mu,\sigma^2/N)$를 따른다

- 중심극한정리(Central Limit Theorem)이라 부르며 모집단의 분포가 정규분포를 따르지 않아도 성립함

💡 표본분포(sample distribution)랑, 표집분포(sampling distribution)는 다름 

베르누이 분포(이항분포)에서 N에 따른 표집분포의 변화

![image](https://user-images.githubusercontent.com/77658029/128109141-413c5190-c62e-4a8b-bc7c-01a7ef532cb3.png)

<br>

## 가능도(likelihood)

- 가능도(likelihood) 함수는 모수 $\theta$를 따르는 분포가 X를 관찰할 가능성(확률이랑은 다름)
- 확률은 어떤 모수($\theta$)에서 $x$가 일어날 확률을 의미하고, 가능도는 어떤 $x$가 일어났을때 모수($\theta$)에 대한 확률을 의미함
- 하지만 가능도 함수(우도함수)의 경우는 확률분포가 아님(전체를 다 더하면 1이 되지 않고, $x$에 따라서 변화함)
- 변하는 모수($\theta$)에서의 확률분포$P(x|\theta)$라고 하면 $X = x_1,x_2,...,x_n$가 독립적으로 일어날때 확률은 그 값을 모두 곱한값으로 표현 가능함

$$ L(\theta|x) = P(x | \theta) = p(X= x_1,x_2,...,x_n| \theta) = P(x_1| \theta)*P(x_2| \theta)*...*P(x_n| \theta) = \prod_{k=1}^{n}P(x_k|\theta)$$

<br>

## 최대가능도 추정법(Maximum likelihood estimation, MLE)

- MLE는 대표적인 모수적 추정 방법임
- 표본평균이나 표본분산은 유용한 통계량이지만, 확률분포마다 사용하는 모수가 다르므로 적절한 통계량이 달라지게됨
- 이론적으로 가장 가능성이 높은 모수를 추정하는 방법 중 하나가 최대가능도 추정법
- 위 가능도 식이 최대가 되는 $\theta$를 구하는게 목적

![image](https://user-images.githubusercontent.com/77658029/128110103-39764d71-a8a9-4d60-ba30-9bea1cb5d0c2.png)

- 데이터 집합 X가 독립적으로 추출되었을 경우 로그가능도를 최적화
- 0~1사이의 숫자를 수억번 곱해주게 되면, 컴퓨터 오차가 커지게 된다. 그렇기 때문에 log화 시킨 후 덧셈으로 처리하여 오차를 최소화 시킬수 있다
- 경사하강법으로 가능도를 최적화 할때 미분연산을 사용하게 되는데, 로그 가능도를 사용하면 연산량을 $O(n^2)$에서 $O(n)$으로 줄여줌
- 대부분의 손실함수의 경우 경사하강법을 사용하므로 음의 로그가능도(negative log-likelihood)를 최적화함

![image](https://user-images.githubusercontent.com/77658029/128110058-da01c2e6-a08f-4752-af82-e61991998654.png)

<br>

### 최대가능도 추정법 예제: 정규분포


- 모수가 평균 $\mu$와 분산 $\sigma^2$ **정규분포**(가우시안 분포)로 가정하면

$$ \theta = (\mu, \sigma^2) $$

- 정규분포에서 $n$개의 표본 ($x_1, x_2, \cdots, x_n$)을 독립적으로 추출

$$ f_{X_i}(x_i;\theta) = \frac{1}{\sigma\sqrt{2\pi}} \exp\left(-\frac{(x_i-\mu)^2}{2\sigma^2}\right) , \,\,i=1, \cdots, n $$

$$L(\theta|x) = \log P(x|\theta) = \sum_{i=1}^{n}\log\frac{1}{\sigma\sqrt{2\pi}}\exp\left(-\frac{(x_i-\mu)^2}{2\sigma^2}\right) $$

- 가능도 함수를 최대로 하는 $\theta$ 값을 구하기 위해 theta로 미분해서 극댓값을 찾을 수 있다. 
- $ \theta = (\mu, \sigma^2) $ 이기 때문에 $\mu$와 $\sigma$로 각각 편미분하여 0이 되는 값을 극댓값으로 볼수 있다

**1. $\mu$로 편미분**
$$\frac{\partial L(\theta|x)}{\partial \mu}
= -\frac{1}{2\sigma^2}\sum_{i=1}^{n}\frac{\partial}{\partial \mu}\left(x_i^2-2x_i\mu+\mu^2\right) = 0 $$

$$ \hat{\mu} = \frac{\sum_{i=1}^{n}x_i}{n}$$

**2. $\sigma$로 편미분**
$$ \frac{\partial L(\theta|x)}{\partial \sigma} = \frac{\partial\left(-n\log\sigma-n\log\sqrt{2\pi}-\frac{1}{2\sigma^2}\sum_{i=1}^{n}(x_i-\mu)^2\right)}{\partial \sigma} $$ 

$$\sigma^2= \frac{\sum_{i=1}^{n}(x_i-\mu)^2}{n}$$ 

<br>

## Futher Question

### 1. 확률과 가능도의 차이
(개념적인 차이, 수식에서의 차이, 확률밀도함수에서의 차이)

- 개념적인 차이 

    확률 : 고정된 모수에서 데이터에 따른 확률을 나타냄
    
    가능도 : 고정된 데이터에서 모수에 따른 확률을 나타냄(가능도 함수는 확률분포를 이루진 않음)
    
- 수식에서의 차이 ($\theta$는 모수를 의미함

    가능도 표현 : $\mathscr P(X=x_0,x_1,...,x_n|\theta)$
    
    확률 표현 : $\mathscr L(\theta|X=x_0,x_1,...,x_n)$
    
- 확률밀도함수에서의 차이 
    
    기본적으로 확률질량함수에서는 특정 데이터에 대한 가능도와 확률은 같지만,
    확률밀도함수에서 확률은 면적을 의미하고, 가능도는 밀도함수에 대응되는 값을 의미한다
    (확률밀도함수에서 하나의 데이터에 대한 확률은 0으로 본다)

<br>
    
### 2. 확률 대신 가능도를 사용하였을 때의 이점

- 확률밀도함수에서 범위가 아닌 데이터가 주어졌을 때에 적절한 모수를 구할 수 있음
- 모집단에 대한 정확한 분포를 알 수 없을 때, 여러 모수로 비교하여 그 순간에 최적의 모수를 구할 수 있음  

<br>

### 3. 미지의 확률분포에서 최적의 모수 찾기

최대 우도법으로 한번 생각해보면, 

theta를 어떤 모수라고 생각했을때

$\mathscr L(\theta|X)$ = $\mathscr P(X|\theta)$ = $\theta^3(1 - \theta)^7$

간단하게 양변에 로그를 취하면 

$log\mathscr L(\theta|X)$ = $log\mathscr P(X|\theta)$ = $log\theta^3(1 - \theta)^7$
$= 3log\theta + 7log(1-\theta)$

$\theta$로 미분하면

$\partial \mathscr L(\theta|X)\over\partial \theta $
= $\partial 3log\theta + 7log(1-\theta)\over\partial \theta$
= $3\over\theta$ + $7\over(1-\theta)$

이 값이 0이 되는 점에서 likelihood값을 최대로 갖음

$3\over\theta$ + $7\over(1-\theta)$ = 0

$3(1-\theta)$ = $7\theta$

$10\theta)$ = $3$

$\theta = 0.3$

```
이 분포에 대해서 생각해봤을 때 
10번의 게임을 했는데 3번 이기고, 7번 졌을때
만약 100번의 게임을 하면 몇 번이나 이길까? 에 대한 문제로 바꿔볼 수 있음
```

<br>

**📌reference**
- boostcourse AI tech
- [Taxonomy of univariate distributions](https://priorprobability.com/2016/09/18/taxonomy-of-univariate-distributions/)
- [공돌이의 수학정리노트](https://angeloyeo.github.io/2020/07/17/MLE.html)
- [불편추정량](https://1992jhlee.tistory.com/19)

<br>

```
💡 수정 필요한 내용은 댓글이나 메일로 알려주시면 감사하겠습니다!💡 
```

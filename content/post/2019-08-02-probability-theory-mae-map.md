---
title: 'Probability Theory: MLE & MAP'
author: Jiho Yeo
date: '2019-08-02'
slug: probability-theory-mae-map
categories:
  - Study
  - Statistics
tags: []
subtitle: ''
summary: ''
authors: []
lastmod: '2019-08-02T17:38:26+09:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---

본 포스팅은 MLE와 MAP를 보다 체계적으로 정리하고 학습하기 위한 기록이다.
이 글은 나의 글이 아니며 http://sanghyukchun.github.io/58/ 이곳에 있는 글을 공부하면서 옮겨 적은 것이다.

-----

## **Maximun Likelihood Estimation (MLE)**

> MLE는 random variable의 parameter를 estimation하는 방법 중 하나인데, 오직 주어진 Observation들을 토대로 parameter를 estimation하는 방법이다.가장 간단한 예를 들어보자. 만약 우리가 p의 확률로 앞면이 나오고 1−p의 확률로 뒷면이 나오는 동전을 던져서 p를 예측한다고 생각해보자. MLE로 p를 계산하기 위해서는 간단하게 앞면이 나온 횟수를 전체 횟수로 나누면 된다.

Probability density function $f_0$가 있다고 가정해보자. 그리고 $X = (x_1,x_2,...,x_n)$을 $f_0$를 통해 생성되는 observations라고 하자. 그리고 density function $f_0$는 $\theta$로 parameterize된 어떤 분포이다, i.e. ${f(.|\theta)}$. 만약 $f$가 가우시안이라면 $\theta$는 평균 $\mu$와 분산 $\sigma$가 될것이며, Bernoulli라면 $0<p<1$ 이 될 것이다. 이렇게 정의하면 Likelihood는 다음과 같이 정의할 수 있다. 

$\mathcal{L}(\theta;x_1,x_2,...,x_n)=\mathcal{L}(\theta;X)=f(X|\theta)=f(x_1,x_2,...,x_n|\theta)$

어떻게 보면, $\theta$가 주어졌을 때 해당 observations들이 튀어나올 확률로 해석할 수 있겠다. 실상은 observations들이 주어졌을 때의 $\theta$를 구하는 것이지만 말이다. 

즉 MLE는 $\theta$를 estimate하는 방법으로, likelihood를 최대로 만드는 값을 $\theta$로 선택하는 것이다. 만약 우리가 그 값을 $\hat{\theta}$이라고 한다면 MLE는 다음과 같은 방법으로 계산된다.

$\hat{\theta} = argmax_\theta\mathcal{L}(\theta;X) = argmax_\theta f(X|\theta)$

만약 observation이 i.i.d. (identically independently distributed)라면, $f(X|\theta)=\Pi_i f(x_i|\theta)$가 되며, 여기에 log를 취해 덧셈형식으로 변환할 수 있다. 따라서 많은 경우 likelihood가 아니라 log likelihood를 기반으로 parameter를 estimation 한다. 

MLE는 직관적이며 간단한 parameter estimation method지만 observation에 따라 그 값이 너무 민감하게 변한다는 단점이 있다고 한다. 

-----

## **Maximum a Posteriori Estimation (MAP)**

MLE의 단점을 해결하기 위해 MAP라는 방법을 사용하기도 한다. 이 방법은 $\theta$가 주어지고, 그 $\theta$에 대한 데이터들의 확률을 최대화 하는것이 아니라, 주어진 데이터에 대해 최대 확률을 가지는 $\theta$를 찾는다. 수식으로 표현하면 다음과 같다. 

$\hat{\theta} = argmax_\theta f(\theta|X)$

MLE와 비교해서 MAP는 보다 더 자연스러운 값을 얻는다. MLE로 parameter estimation을 하게 되면 오직 지금 주어진 데이터만 잘 설명하는 parameter를 찾게 된다. 하지만 우리가 원하는 것은 지금까지 들어온 값에 대해서만 잘 설명을 하는 것이 아니라 보다 일반적인 값을 원한다. 여러 parameter들 중에 데이터가 주어졌을 때 가장 확률이 높은 $\theta$를 고를 수 있다면 가장 좋은 결과를 얻을 수 있을 것이다.

하지만 MAP를 계산하기 위해 필요한 $f(\theta|X)$는 계산이 불가능하며 우리는  $f(X|\theta)$밖에 관측할 수가 없다. 만약 f가 정규분포라고 한정지어 생각해보면, 어떤 관측값 X가 있을 때 얘네들이 어떤 평균과 분산을 가지는 모분포에서 왔을지는 알 수 가 없는 것과 같은 이치이다. 우리는 오직 모수가 주어졌을 때 해당 분포가 나올 확률만을 계산할 수 있다. 

$f(\theta|X)$를 계산하기 위해선 Bayes's Theorem이라는 새로운 개념이 필요하다

-----

## **Bayes' Theorem**

Bayes’ Theorem은 $p(Y|X)$와 $p(X|Y)$의 관계를 표현하는 식이다. 식의 꼴은 매우 간단하지만, 이 theorem은 많은 의미를 가지고 있다. Thoerem은 다음과 같다.

$p(Y|X) = {p(X|Y)p(Y) \over p(X)}$

이를 지금 우리의 문제에 적용시키면 아래와 같이 쓸 수 있다. 

$f(\theta|X) = {f(X|\theta)f(\theta) \over f(X)}$


이때 

- $f(\theta|X)$: posterior (주어진 데이터에 대한 현상의 확률)
- $f(X|\theta)$: likelihood of Observation
- $f(\theta)$: prior(현상에 대한 사전정보)

를 나타낸다. 

이 수식이 중요한 이유는 우리가 관측할 수 있는 데이터 이외에도 데이터에 대한 적절한 가정이 있다면 **관측 데이터만을 사용하는 것보다 더 우수한 parameter estimation**을 가능하게 하기 때문이다. 

다시 MLE와 MAP로 돌아가보면, Bayes' Theorem을 사용하면 MAP와 MLE의 관계를 다음과 같이 적을 수 있다.

$\hat{\theta} = argmax_{\theta} f(\theta|X)$

$= {argmax_\theta {f(X|\theta)f(\theta) \over f(X)}}$

$= {argmax_\theta {\mathcal{L}(\theta;X)f(\theta) \over f(X)}}$

이 때 $f(X)$는 $\theta$에 영향을 받는 term이 아니기 때문에 다음과 같이 적을 수 있다. 

$\hat{\theta} = argmax_\theta \mathcal{L}(\theta;X)f(\theta)$

위의 MLE식과 비교해서 $f(\theta)$ (prior)이 추가된 것을 알 수 있다. 
따라서 만약 $f(\theta)$를 알고 있다면, MLE가 아니라 MAP를 하는 것이 가능하다. 즉 $\theta$에 대한 assumption을 사용해 결과를 더 향상시킬 수 있다. 예를들어 우리가 시험성적의 gaussian distribution을 estimation하고 있다고 생각해보자. 이 경우 mean은 반드시 시험점수 범위 안에 포함되어야 하고, 그 값을 벗어날 수 없다. 그리고 이전 시험들의 성적을 살펴보면 그 값이 대체로 40~60점 사이에 몰려있다는 등의 정보가 있다고 가정해보자. MLE로는 이런 정보를 활용하는 것이 불가능하지만, $f(\theta)$를 가정하고, 이를 사용해 MAP를 사용할 수 있게 된다. 즉 만약에 우리가 데이터에 대한 적절한 가정을 할 수 있다면 더 나은 추론을 하는 것이 가능한 것이다. 이를 prior이라고 한다. 만약 우리가 옳은 prior를 선택한다면 MLE보다 MAP가 더 좋겠지만 잘못된 prior을 선택하게 된다면 오히려 성능이 더 떨어질 수 있다. 쉽게 생각해 **prior은 일종의 '선입견'**이다. 따라서 데이터에 대한 좋은 prior을 선택하는 것이 매우 중요하다. 참고로, prior가 uniform distribution이라면 MLE와 MAP는 정확하게 같은 문제를 푸는 것과 같다. 

정리하자면, Bayes’ Theorem은 더 좋은 가정이 있다면 더 좋은 유추를 할 수 있음을 보여주는 수식이다. 많은 Machine Learning Technique들이 Bayes Theorem에 근거하여 만들어졌으며, 데이터 관측과 데이터에 대한 가정을 통해 더 정확한 추론인 MAP를 가능하게 만들어주는 강력한 방법론이기도 하다.

-----

## **Advanced Topic: Conjugate Prior**

보통 prior는 exponential family에서 고르는 경우가 많다. Bernoulli, binomial, Poisson, Gaussian, Laplace, gamma, beta distribution 등등이 exponential family에 속한다. Exponential family를 많이 선택하는 이유는 대부분의 데이터들이 이 모양을 띄고 있기 때문이기도 하며, 만약 likelihood가 exponential family일 때, prior를 ‘좋은’ exponential family로 선택하게 되면 posterior와 prior가 같은 family에 속하게 되기 때문이다. 예를 들어 likelihood가 Bernoulli라고 하면, prior를 beta distribution으로 선택하게 되면 posterior도 beta distribution이 되며 이를 conjugate prior라고 한다.

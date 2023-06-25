---
layout: post
title:  "softmax / log-softmax / loss들"
excerpt: "딥러닝 공부 1"

tags:
  - [Blog, jekyll, Github, Python]

toc: true
toc_sticky: true
 
date: 2023-06-25
last_modified_at: 2023-06-25
---
{% include toc.html %}
### 1. softmax 함수 
소프트맥스(softmax)는 주로 k차원의 벡터를 0에서 1사이의 값으로 만들고, 합이 1이되게 해서 어떤 클래스에 속할지 예측하는 과정에 주로 사용되며 수식은 다음과 같다.
$$
P_j = \frac{e^{z_j}}{\sum_{k=1}^{K}e^{z_j}} 
j = 1,2,...,K
$$
K는 클래스 숫자를 나타내고, $z_j$는 소프트맥스의 입력값이다. $P_j$를 직관적으로 해석하게 되면 j번째 입력값/입력값의 합 으로 나타낼 수 있는데, 여기서 왜 지수함수 $e$를 해줘야하면 미분가능한 값으로 만들어주기 위해서 해준다.
즉 입력값 중 큰 값은 더 크게, 작은값은 더 작게 만들어서 입력된 벡터를 잘 구분될 수 있게 만들어준다. softmax를 통해서 나온 값은 특정 클래스가 정답일 확률을 나타내며 여기서 실제 값과 예측값(softmax값)과의 오차를 구하고 이 오차를 가지고 역전파를 통해서 가중치를 업데이트한다.

더해서 softmax는 logit값과 역함수 관계를 가지고 있고, softmax함수에서 클래스 갯수를 2개로 두면 sigmoid함수가 되고, sigmoid함수를 k개 클래스로 이랍ㄴ화하면 softmax가 된다. 신경망에서 sigmoid는 보통 활성화함수로 사용하지만 수학적으로는 같은 함수이다.

하지만 이런 softmax함수는 NLL Loss에는 사용될 수 없다(수치적으로 불안정하게 나와서 NaN의 결과가 나올 수 있음)

따라서 log_softmax의 개념이 나왔다

### 2. log softmax함수
log_softmax함수는 그냥 softmax에 log를 해준것과 동일하다. 하지만 함수를 불러와서 사용할 경우 두 연산을 따로 진행하는 것보다 더 빠르고 수치적으로 안정적이라고 한다(이유는 ,, 잘 모름)

둘다 torch.nn.functional에서 불러와서 사용가능하다.

{% highlight css %} 
import torch.nn.functional as F
a = F.softmax(x, dim=1) # dim = 1 은 1차원을 대상으로 잡고 진행한다는 뜻
b = F.log_softmax(x, dim=1)
a = log(a)
if a == b :
    print('True')
{% endhighlight %}
하면 True가 출력된다.

### 3. CrossEntropyLoss
이 함수는 log_softmax와 nll_loss가 하나의 함수로 합쳐진 것이다.

{% highlight css %} 
import torch.nn.functional as F
loss = F.nll_loss(F.log_softmax(x,dim=1),y)
loss2 = F.cross_entropy(x,y)
{% endhighlight %}
이 두개의 결과는 동일하다.
즉 cross_entropy 를 사용하게 된다면 raw output을 사용하는 것이 좋다.(어차피 과정에 포함되어있기 때문에)
하지만 중복으로 사용해도 값은 동일한데, 그렇다고해서 굳이 연산을 늘릴필요는 없기 때문이다.

### 4. loss 함수들
순서가 이상하긴하지만 이번에 다시 공부하는 김에 적어놓으려고한다.
loss함수란 한마디로 예측값과 실제 정답값의 차이를 구하는 방법이라고 한다. 이 함수의 값이 최소가 되도록 weight와 bias를 찾는 것이 딥러닝이다.

#### 4-1. MSE(Mean Squared Error)
가장 간단하고 편리한 평균 제곱 오차이다. 
수식은 다음과 같다.
$$
MSE = \frac{1}{N}\sum_{N}^{i=1}(y_i-\hat{y}_i)^2
$$
간단하게 실제 값과 예측값의 차이를 제곱하고 그것을 다 더해준 뒤 더해준 갯수로 나눠주면 된다.
제곱으로 인하여 값이 차이가 크다면 더 벌어지게 만들어주며, 양수이던 음수이던 값을 누적시켜준다.
#### 4-2. RMSE(Root Mean Squared Error)
기본적으로 다 동일하고 단순히 MSE에 루트를 씌워준다.
오류의 제곱으로 인하여 실제 error보다 커져서 왜곡이 생기는 것을 방지한다.

#### 4-3. binary crossentropy
2개의 클래스를 대상으로 예측을 할때, 즉 이진분류를 할 때 사용하면 좋음
단 다중클래스 분류와 다르게 이진분류시에는 1차원으로 펴줘서 바로 진행함
{% highlight css %} 
import torch.nn as nn
x = nn.Sigmoid(x)
loss = nn.BCELoss(x,y)
{% endhighlight %}

#### 4-4. categorical crossentropy
클래스가 2개 이상일 경우 binary가 아닌 categorical을 사용한다. 보통 softmax이후에 사용하기 때문에 softmax loss라고도 불린다.()
이 경우는 원핫인코딩이 되어있어야함

#### 4-5. sparse categorical crossentropy
categorical crossentropy와 동일하게 멀티 클래스 분류에 사용되는 loss이다.
원핫인코딩일 필요없이 정수 인코딩인 상태에서 사용 가능하다.
라벨이 1,2,3,4 처럼 되어있을 경우 바로 사용가능하다. 하지만 그냥 원핫인코딩으로 처리해서 사용하는 경우가 많다. 
알아만 두자

#### 4-6. focal loss
focal loss는 분류 에러에 근거한 loss에 가중치를 부여한다. 샘플이(data point가)이미 올바르게 분류가 된다면 그것에 대한 가중치는 감소하고 더 문제가 있는 loss에 집중하여서 모델을 학습한다.
불균형한 클래스 문제를 해결할 때 사용한다.

### 5. Entropy는 뭘까?
앞에서 loss함수를 정리하면서 entropy라는 개념이 계속해서 등장했다. 그러면 entropy는 뭘 말할까?
엔트로피는 불확실성의 척도이고, 엔트로피가 높다는 것은 정보가 많고 확률이 낮다는 것을 의미한다.
이 설명은 와닿지 않고, 어느 블로그에서 정리하면서 본인은 어떤 데이터가 나올지 예측하기 어려운경우가 불확실성이라고 이해했다고 한다.

#### 5-1. 동전 vs 주사위
동전과 주사위를 예시로 들어보자, 동전은 앞/뒷면 각각 1/2씩 나올 가능성이 있지만 주사위는 6개의 경우의 수를 가진다. 이는 즉 주사위가 불확실성이 크다는 것이다.

이와같은 예시로 엔트로피를 생각할 수 있다. 수학적으로도 증명이 된다. 

그러면 Cross-Entropy는 뭘까?
#### 5-2. Cross-Entropy
cross entropy는 두 확률 분포의 차이를 구하기 위해서 사용된다.
모델이 예측한 확률분포 q와 실제 데이터의 확률분포 p와의 차이를 계산할때 사용된다.
이 차이를 계산하여서 최소화 시킨다면, 실제 데이터와 모델의 예측값의 차이가 최소화된다는 것이고 이를 통하여 모델을 학습시킬 수 있다.

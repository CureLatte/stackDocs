## Deep Learning 
***


<br>


머신러닝의 한 종류이다. 

> 인공지능 
>> 머신러닝
>>>  딥러닝 


<br>

`Deep Learning`은 `Linear Regression`, `Logistic Regression` 과는 다르게 비선형인 레이어를 
넣었다는 것이 차이점이고   
해당 레이어를 'Deep' 하게 쌓는다고 해서 `Deep Learning` 이라한다. 


* `Linear Regression` = `H(x)`를 찾는 것
* `Logistic Regression` = `H(x)` + `Sigmoid Function` (이전 분류) + `Softmax Function` (다중 분류)
* `Deep Learning` = {`H(x)` + `activation Function` (비선형 함수)} * N + `Softmax Function` (다중 분류)


이때 비선형 함수들을 `Activation Function` 이라한다. 

<br>

#### 비선형 함수들
* `Sigmoid`
* `tanh`
* `ReLU`
* `Leaky ReLU`
* `Maxout`
* `ELU`


<br>

#### Overfitting, Underfitting

Deep Learning의 설계/ 튜닝 과정에서 가끔 `Training loss`는 낮아지지만 
`Validation loss` 가 높아지는 시점이 존재한다. 

이때 가장 낮은 `validation loss`를 기점으로 Error가 높은쪽이   
`Underfitting(과소적합)` - 아직 학습이 부족해 문제를 푸지 못하는 상태

Error가 높은 쪽이 

`Overfitting(과적합)` - 복잡도가 높아 실제 문제를 풀지 못하는 경우이다. 


***


### Deep Learning의 주요 skill 

* Data augmentation (데이터 증강 기법): 데이터의 개수를 늘려 학습을 더잘 시키는 방법으로 기존의 데이터를 일부 변형시킨다.(회전, 대칭,자르기 등등)
* Dropout : 과적합을 해결하기 위한 방법으로 랜덤하게 일부 노드의 선을 삭제하는 것 - 복잡도를 해결하기 위한 방법
* Ensemble(앙상블) : Computer Power가 충분할 때 사용할 것!, 여러개의 모델을 만들어 출력을 기반으로 투표하는 것.
* Learning rate decay : 원하는 결과에 빨리 도달하기 위해 처음에는 큰 폭으로 Learning rate를 잡고 결과값에 도달할수록 그 폭을 줄이는 것


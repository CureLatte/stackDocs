## Logistic regression - 논리 회귀

0 과 1만의 결과가 있는 문제에서 푸는 방법으로 

예를 들어 해당 과목의 이수 여부를 판단하는 문제가 있다.

>Ex) N 시간을 공부했을 때 해당 과목을 이수 할 지(1) 말 것인지(0)
    에 대한 문제를 풀는 방법

* 직선을 찾는 논리 회귀로는 논리 문제를 풀수 없기에 (선을 나눌 수 없음 ) 새로운 함수를 이용

해당 함수를 `Sigmoid function` 이라한다. 

해당 함수를 이용 하여 선형회귀 후 `Sigmoid function`을 이용해야 한다. 

* ##### `Logistic Regression` = `Linear Regeression` + `Sigmoid function` 

### 다항 논리 회귀 

다항 논리 회귀란 결과가 하나만 파악하는 것이 아니라 분류를 하는 것으로 

클래스를 분류하는 과정이다. 

Ex) 
```
* A -> 1
* B -> 2
* C -> 3
```
의 상황으로 분류를 하는 것인데 이 때 꼭 필요한 것이 `One-hot encoding`이다.

컴퓨터가 잘 이해할 수 있도록 클래스 분류를 해주는 것인데 

```angular2html
* A -> 1 -> [1,0,0]
* B -> 2 -> [0,1,0]
* C -> 3 -> [0,0,1]
```
총 배열을 0으로 만들고 각 클래스에 맞는 부분만 1로 만드는 것이다. 

다중 논리 회귀는 이전의 논리 회귀에 `Softmax`라는 함수를 이용하여 확률로 표현한다. 

이때 `softmax` 의 함수는 모든 결과를 더했을 때 1로 만들어주는 함수이고 각 데이터의 가중치에 따라 다르게 

값이 계산된다. 

* `Multinomial logistic regression` = `Linear regression` + `Logistic regression` + `Softmax`
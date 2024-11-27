## CNN(Convolutional Neural Networks) - 합성곱 신경망 

<br>

### 개요
***
`Deep Learning`의 다양한 신경망 중 하나로 이미지 처리에 가장 좋은 성능과 효율을 낼 수 있다. 
`image processing`에서 사용하는 `covoultion`를 사용하기 때문에 `CNN`이라함 

<br>

### 용어 
***

* Filter(or Kernal) : 합성곱을 할 때 사용되는 일정한 크기의 배열
* Stride : Filter가 움직이는 간격 
* Padding : 합성곱을 실행할 때 원래 크기를 유지 하기 위해 빈 레이어를 외곽에 주는 것
* Pooling : 이미지의 특정한 부분을 추출하는 역할 
  * Max polling : 필터 내 이미지 중 가장 큰값을 추출 하는 방법
  * Average polling : 필터내 이미지 중 평균을 추출 하는 방법
* Flatten layer : 이미지의 2차원 배열을 1차원으로 바꾸는 과정 

<br>
<br>

### 구성 
***

* `Convolution` + `ReLU` 
* `Pooling`
* `Convolution` + `ReLU` 
* `Fully Connected`
* `Fully Connected`
* `Output predictions`

<br>
<br>


### 종류
*** 

* `AlexNet`
* `VGGNet`
* `GoogleNet(= Inception V3)`
* `ResNet`
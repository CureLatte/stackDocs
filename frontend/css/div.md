## ```<div>```


***

### 정의   

*  #### HTML에서 가장 많이 쓰이는 태그로써 구분하기 위해 주로 사용된다.

***

### 특징

* #### 정해진 문법이 없으며 Class 와 id로 구분해주어 사용

***

### 속성

<br>

* ```background-color``` - ```색깔```: div의 배경색을 설정
* ```background-img``` - ```url("이미지 경로")```: div의 배경을 img로 설정
* ```background-position``` 
  * default  ```center```
  * ```center``` ```left``` ```right```
  * ```top``` ```center``` ```bottom``` 조합
* ```background-repeat``` : 배경이미지 반복 설정
  * default ```repeat```
  * ```repeat-x``` : x축 방향(가로축) 으로 반복
  * ```repeat-y``` : y축 방향(세로축) 으로 반복
  * ```no-repeat``` : 반복 설정 x
* ```overflow``` : 안의 내용물이 div 보다 클 경우
  * default  ```auto``` : 넘치는 방향으로 스크롤 생성
  * ```scroll``` : 스크롤 넣기
  * ```hidden``` : 보이지 않게 하기
    * ```.classname::-webkit-scrollbal``` : 스크롤관련 css

***

### 주의 사항

<br>

* #### div 값을 줄 때 안에 내용물이 없다면 표시되지 않는다
* #### div의 크기를 설정할 때 하위 항목에 절대 수치 vw,vh,px가 없다면 역시 내용을 표기하지 않는다

* #### 구분을 위해서 CSS를 정하지 않아도 구분함 






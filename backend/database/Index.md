# DB INDEX
*** 

데이터 베이스의 데이터가 많아질 경우

조회의 속도가 굉장히 느려질 수 있다.

느려지는 이유는 트랜잭션 `Lock`, 검색 범위가 넓은 경우, 불필요한 `Join` 등등

단순히 데이터가 많아진 경우라면 `Index` 를 이용하면 훨씬 빠르게 데이터 조회가 가능하다.



## INDEX 란?

이름에서 알수 있듯이 색인 목록 즉 정보를 찾기위한 지름길의 역할을 한다.

기본적으로 `DataBase` 에서는 기본키인 `Primary key` 를 기반으로 인덱스가 정해져있다.

이러한 `PrimaryKey` 는 `AutoGenerate` 형식으로 `ID` 가 새로 증가할 수밖에 없으므로

순서정렬이 되어있는 상태이기 때문에

특정 `ID` 를 검색을하면 데이터가 얼마나 많이 존재하던 빠르게 조회가 가능하다.


이것이 가능한 이유는 `B-Tree` 구조로 순서정렬이 되어있기 때문에

`절반 조회` -> `절반 조회` -> ... 방식을 거쳐 몇번의 방법만에 조회가 가능하다.


이걸 기본 `KEY` 말고 다른 `Column` 에게도 적용하는 것이 인덱스를 생성/적용한다고 한다.


### 하나만 가능할까?

인덱스는 하나의 `Column` 만 가능한 것이 아닌 여러가지 `Column` 을 적용할 수 있고 이를 복합 인덱스 라고 한다.

이때 선언 순서에 따라 순서정렬을 진행하므로 순서에 유의하면서 적용해야한다.

### 단점
해당 방식은 순서정렬을 위해 보인는 거와 다르게 Database 가 숨겨진 정렬 데이터를 갖고 있는데
이는 조회할 때는 문제가 되질 않지만
해당 `Table` 에서 `Create`, `Update`, `Delete` 가 실행이 될 때마다
숨겨진 정렬조건을 다시 재 정렬해야하는 문제가 발생한다.

즉 테이블의 변화가 가장 많이 일어나는 곳에서는 사용할수록 성능이 오히려 나빠지는 단점이 존재한다.



<br>

## 동작 방식
`Query` 를 작성하고 실제 명령어를 실행할 때 `DataBase` 에서는

해당 쿼리를 빠르게 찾을 만한 방법을 찾게 되는데 이때 찾아야하는 조건 중
해당 `Column` 이 `Index` 가 걸려있다면 해당 `Index` 를 이용하여 더 빠르게 찾게 된다.

만약 `Index` 가 걸려있지 않다면 당연히 전체 `Table` 을 하나씩 확인하는 `Full Scan` 을 하게 된다.

이떄 실행계획을 미리 확인해 볼 수 있는데

방법은 `Query` 앞에 `explain` 이라는 명령어를 넣게 된다면
어떤 식으로 데이터를 찾을지 `Table` 형식으로 알려준다.

<table>
<thead>
    <tr>
        <td>id</td>
        <td>select_type</td>
        <td>table</td>
        <td>partitions</td>
        <td>type</td>
        <td>possible_keys</td>
        <td>key</td>
        <td>key_len</td>
        <td>ref</td>
        <td>rows</td>
        <td>filtered</td>
        <td>Extra</td>
    </tr>
</thead>
<tbody>
    <tr>
        <td>-</td>
        <td>조회 방식</td>
        <td>조회 테이블</td>
        <td>-</td>
        <td>조회 방식</td>
        <td>사용 가능 한 INDEX</td>
        <td>사용 INDEX</td>
        <td>index Key 길이</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
        <td>-</td>
    </tr>
</tbody>
</table>



이중 `PossibleKey` 와 `type`, `key` 를 확인해보면 `Index` 를 이용한지 확인할 수 있다.

특히
`type` 에서 `ALL` 이라고 조회된다면 `Full SCAN` 을 한 것이다.

<br>


## 적합한 `INDEX` 사용 방법

적합한 `Index` 를 사용하기 위해선 어떻게 해야 순서정렬에 용인한가? 를 기준으로 봐도 좋을 것같다.

### 1. 데이터 중복이 적은 `Column` 일 수록 좋다.

즉 하나의 `100 만건`에 대한 `Data` 중에 단순히 `4가지`의 값만 존재 하는 데이터와  
`100만 건` 중  `80만건`이 서로 다른 값인 데이터 중 순서정렬을 할때 더 명확해 지는 데이터는
당연히 후자이자

이러한 부분이 데이터 중복이 적을 수록 `Index` 를 이용하기 정합하다 라고 할 수있다.

이걸 용어로는 `Cardinality(중복도)` 가 높다 라고 표현한다.


### 2. 인덱스로 설정된 `Column` 그대로 사용해야한다.

`Index` 로 `testColumn` 을 지정한다면

`Index` 를 이용하기 위해선 `where` 절에서 `testColumn` 자체로 정렬을 해야만한다.


그렇지 않고 `testColumn + 3` 이라는 조건이 들어간다면 전체 데이터에 `3`을 더해야 하기 때문에

`DataBase` 는 순서를 다시 정렬해야만 한다.

따라서 전체 `Table` 을 확인해봐야하기 때문에 무의미하게 된다.


<br>


## 주의 할점 

`Index` 를 사용하더라도 `DataBase` 별로 있는 최적화 엔진에 의해서
`Index` 를 사용할 수도 없을 수도 있다.

다양한 경우가 있는데 

* 기본적으로 설정된 `Primary` 값인 `ID` 로 조회했을 때 더 빠른경우
* 경우의 수가 많이 없는 `Index` 경우
* `Index` 를 상용하지 않은 `WHERE` 문인 경우
* 데이터가 적은 경우 


등등 `INDEX` 를 탈 경우는 주의해야할 부분이 많다.

그렇기 때문에 꼭 설정후 테스트는 필수로 하는 것이 좋다고 생각한다!



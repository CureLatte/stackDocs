# JPA LOCK 설정 
***

SPRING 의 대표 ORM 인 jpa 에서 database 에게 직접 쿼리를 날릴수도 있고  

JPQL 을 이용해서 간단한 쿼리를 날릴 수가 있는데 이때 동시성에 대한 문제를 해결 하기 위해  

LOCK 을 설정할 수 있다.

기본적으로 `LockModeType` 에 정의 되어있다.


## LOCK 종류
***
* 비관적 LOCK
  * `LockModeType.PESSIMISTIC_WRITE`
  * `LockModeType.PESSIMISTIC_READ`
  * `LockModeType.PESSINISTIC_FORCE_INCREMENT`
* 낙관적 LOCK 
  * `OPTIMISTIC`
  * `OPTIMISTIC_FORCE_INCREMENT`


통상적으로 알고있는 [데이터 베이스 LOCK](../../../database/lock.md)  
의 기능을 갖고 있지만 세부적으로 권한이 나누어 지게 된다.

<br>


### `LockModeType.PESSIMISTIC_WRITE`

역시 비관적 `LOCK` 의 방식으로 적용이 되며 

`X-LOCK` 을 사용 하여 다른 트랜잭션에서 읽거나 쓰질 못하는 방식이다.


### `LockModeType.PESSIMISTIC_READ`

기본적으로 비관적 `LOCK` 이 걸리게 되지만 읽기 권한은 있는 상태라 

다른 트랜잭션에서 읽을 수 있다.

대신 쓰기 권한이 없는 경우이다.

즉, `S-LOCK` 을 이용하여 비관적 `LOCK` 을 구현하는 것 같다.


### `LockModeType.PESSINISTIC_FORCE_INCREMENT`

위와는 다르게 `Version` 이라는 키를 이용하는 비관적 `LOCK` 이다.

`Version` 이라는 정보는 낙관적 `LOCK` 을 사용할 때  

사용하는 것 같지만 비관적 `LOCK` 에서도 사용하는 것같다. 

> FORCE 가 들어간 걸로 보아 강제로 Version 을 올려가며 수정하는 것 같음


### `LockModeType.OPTIMISTIC`

낙관적 LOCK 이 구현된 것이다.

### `LockModeType.OPTIMISTIC_FORCE_INCREMENT`

강제로 Version 을 올리는 방법이다.




## 사용 방법
***


### 낙관적 LOCK

``` java

  // BASE
  class CustomRepository extends JpaRespository<CustomEntity, Long> {
     
      @Lock(LockModeType.PESSIMISTIC_WRITE)
      public void newSelectQueryMethod();
  }

  
  // JPQL
  class CustomRepository extends JpaRespository<CustomEntity, Long> {
     
      @Query(value ="""
        select * 
        from CustomEntity
      """) 
      @Lock(LockModeType.PESSIMISTIC_WRITE)
      public void newSelectQueryMethod();
  }
  
  // Native Query
  class CustomRepository extends JpaRespository<CustomEntity, Long> {
     
      @Query(value ="""
        select * 
        from CustomEntity
        for share
      """) 
      @Lock(LockModeType.PESSIMISTIC_WRITE)
      public void newSelectQueryMethod();
  }
  
  
```

### 비관적 LOCK

``` java
  // Base
  class CustomRepository extends JpaRespository<CustomEntity, Long> {
     
     
      @Lock(LockModeType.PESSIMISTIC_WRITE)
      @QueryHints({@QueryHint(name = "javax.persistence.lock.timeout", value = "10000")})
      public void newSelectQueryMethod();
  }

  
  // JPQL
  class CustomRepository extends JpaRespository<CustomEntity, Long> {
      
      @Query(value ="""
        select * 
        from CustomEntity
      """) 
      @Lock(LockModeType.OPTIMISTIC_FORCE_INCREMENT)
      @QueryHints({@QueryHint(name = "javax.persistence.lock.timeout", value = "10000")})
      public void newSelectQueryMethod();
  }
  
  // Native Query
  class CustomRepository extends JpaRespository<CustomEntity, Long> {
     
      @Query(value ="""
        select * 
        from CustomEntity
        for lock
      """) 
      @Lock(LockModeType.PESSIMISTIC_WRITE)
      @QueryHints({@QueryHint(name = "javax.persistence.lock.timeout", value = "10000")})
      public void newSelectQueryMethod();
  }
  
```

* 비관적 `LOCK` 일경우 잊지 말고 `TIMEOUT` 설정을 해주자 --> 잠금을 확인하자마자 `ROLLBACK` 될 수 있음


<br>

### 참조 블로그
***

# Spring Redis 연결
*** 


`Spring` 에서도 당연 `Redis` 를 이용하기 위한 방법이 존재한다.

그래서 `Redis` 를 등록하는 과정을 정리하고자 합니다.

## 라이브러리 설치

Gradle 상황에서 설치를 했기 때문에 `build.gradle` 파일에 적어준다.

``` java
    implementation 'org.springframework.boot:spring-boot-starter-data-redis'
```



## Redis Bean Container 설정

설정 파일을 위해 `RedisConfig.java` 라는 파일 을 만들어 

`@Configuration` 을 붙여 `Bean` 등록을 할 수 있도록 하고 

환경변수 인 `Application.properties` 에 저장된 `HOST`, `PORT` 을 가져와 

해당 클래스의 `HOST`, 와 `PORT` 를 입력해 줍니다. 
이때 `@Value` 어노테이션으로 지정해줍니다.

```
# application.properties
# redis
spring.data.redis.host=localhost # Redis 주소
spring.data.redis.port=6379 # Redis 포트번호


```

``` java
package io.hhplus.tdd.hhplusconcertjava.common.config;

import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.data.redis.connection.RedisConnectionFactory;
import org.springframework.data.redis.connection.lettuce.LettuceConnectionFactory;

@Configuration
public class RedisConfig {
    @Value("${spring.data.redis.host}")
    private String host;

    @Value("${spring.data.redis.port}")
    private int port;

    @Bean
    public RedisConnectionFactory redisConnectionFactory() {
        // RedisConnection!
        return new LettuceConnectionFactory(host, port);
    }

  
}

```



`RedisConnectionFactory` 은 Redis 서버와 연결을 관리 하는데 

이 인터페이스를 구현하는 구현채가 `LettuceConnectionFactory` 와 `JedisConnectionFactory` 가 존재한다.  

일반적으로는 위의 예시처럼 `LettuceConnectionFactory` 를 사용하고  
`JedisConnectionFactory` 은 클러스터 연결에 더 뛰어나다고 한다.    

이에 대한 비교는 따로 정리가 필요해 보인다.


우선은 일반적으로 사용되는 `LettuceConnectionFactory` 으로 이용!


`RedisConnectionFactory` 를 이용하여 `Redis` 서버와 연결을 했다면 

해당 명령어를 쉽게 보낼 수 있도록 지원하는 

`RedisTemplate` 을 추가로 등록해주면된다.



``` java
package io.hhplus.tdd.hhplusconcertjava.common.config;

import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.data.redis.connection.RedisConnectionFactory;
import org.springframework.data.redis.connection.lettuce.LettuceConnectionFactory;
import org.springframework.data.redis.core.RedisTemplate;

@Configuration
public class RedisConfig {
    @Value("${spring.data.redis.host}")
    private String host;

    @Value("${spring.data.redis.port}")
    private int port;

    @Bean
    public RedisConnectionFactory redisConnectionFactory() {
            
        return new LettuceConnectionFactory(host, port);
    }

    // RedisTemplate 사용을 위한 추가
    @Bean
    public RedisTemplate<?, ?> redisTemplate() {
    
        RedisTemplate<?, ?> redisTemplate = new RedisTemplate<>();
        redisTemplate.setConnectionFactory(redisConnectionFactory());
        return redisTemplate;
    }

}

```

이제 Redis 를 사용하는 곳에 가서 redisTemplate 을 호출하여 명령어를 날리면된다!

[공식문서](https://docs.spring.io/spring-data/redis/reference/api/java/org/springframework/data/redis/core/package-summary.html) 에서 찾아볼 수도 있다!




## 기본적인 사용법
Redis 는 Key-Value 형태로 구현되어 있고 내부 여러가지 자료구조를 통해 이루어져 있다.


해당 자료구조 목록은 다음과 같다. 
* `String`
* `Hash`
* `List`
* `Set`
* `Sorted set `
* `Stream`
* `Bitmap`
* `Bitfield`
* `Geospatial`


각 자료구조별 `Operation` 을 얻어 사용하거나 `RedisTemplate` 의 `Method` 를 이용하여 사용하면 된다.

### String 
```java

    class TestService {
    
    // Bean 으로 주입 받음
    @Autowired
    RedisTemplate<String, String> redisTemplate;
    
    public void testFunction(){
        
        // operation 얻기 
        ValueOperation<String, String> operation = redisTemplate.opsForValue();
        
        // KEY-VALUE 등록
        operation.set("key", "value");
        
        // VALUE 조회
        String cachedValue = operation.get("key");
        
    }
    
}


```


<br>

### LIST
```java

    class TestService {
    
    // Bean 으로 주입 받음
    @Autowired
    RedisTemplate<String, String> redisTemplate;
    
    public void testFunction(){
        
        // operation 얻기 
        ValueOperation<String, String> operation = redisTemplate.opsForList();
        
        // KEY-VALUE 등록
        operation.rightPush("key", "value1");   // Redis: key: [ "value1" ]
        operation.rightPush("key", "value2");   // Redis: key: [ "value1", "value2" ]
        operation.leftPush("key", "value3");   // Redis: key: [ "value3", "value1", "value2"]
        
        // range(Key, 시작 Index, 끝 Index);
        List<String> getList = operation.range("key", 0, -1); // ["value3", "value1", "value2" ]
        
        String value2 = operation.index("key", 2); // "value2"
        
        String value3 = operation.rightPop("key"); // "value3", Redis: key: [ "value1", "value2"]
        
        // VALUE 조회
        String cachedValue = operation.get("key", 0);
           
    }
    
}

```
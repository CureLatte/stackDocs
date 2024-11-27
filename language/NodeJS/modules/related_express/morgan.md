# morgan
***


> express 미들웨어 중 하나  
> 서버를 킨 이후 클라이언트로 부터 어떤 요청이 왔는지 서버에 로그를 남겨주는 미들웨어  



<br> 
<br>

## 사용법 
***

### import

```javascript
const morgan = require('NodeJS/modules/related_express/morgan')
```

<br> 

### 개발용 과 배포용으로 나눠진다. 

<br>

### 개발용 

```javascript
// 개발용 으로 사용 
app.use(morgan('dev'))
```
__[출력]__
```shell
GET / 304 1.449 ms - -
```

<br>

### 배포용

```javascript
// 배포용 으로 사용 
app.use(morgan('combined'))
```
__[출력]__
```shell
::1 - - [07/Jul/2022:01:58:13 +0000] "GET / HTTP/1.1" 304 - "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.0.0 Safari/537.36"  
```

> 더 자세한 설명이 나온다.  
> 접속시간, 요청에 대한 정보, 브라우저 정보 등

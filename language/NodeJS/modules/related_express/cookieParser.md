# CookieParser Module
***
> 쿠키를 파싱해주는 모듈로 기존 방법보다 훨씬 간단해 졌다. 

<br> 
<br>

## 사용법
***


### import
```javascript
const cookieParser = require('cookie-parser')
```

<br>

### 쿠키 조회
```javascript
//server.js

// 평문 쿠키 
app.use(cookieParser())

app.get('/', (req, res)=>{
    req.cookies // {mycookie: 'test'}
})
```
* `req.cookies` 안에 모든 `cookie` 들이 `Object` 로 정렬 되어 있다. 
* 해당 Value 가 한글을로 `encodeURIComponent` 가 되었다면 `deencodeURIComponent` 으로 `decoding` 하여 봐야 한다. 
  ```javascript
  // cookie = { 'name' : '%EA%B9%80%EC%9E%AC%EC%84%B1 '} 이라면
  
  deencodeURIComponent(req.cookie['name'])
  ```
* 암호화 키 설정
  ```javascript
  app.use(cookieParser('암호화할 키값'))
  ```

<br>

### 쿠키 생성
```javascript
app.get('/', (req, res)=>{
    // 함수 형식으로 생성
    req.cookie('name', 'hong', {
        expires: new Date(),
        httpOnly : true,
        path: '/',
    })
    // cokies : { 'name': 'hong'}
  
})

```
* Options
  * `expires` : 쿠키 만료 기간
  * `httpOnly` : `http` 로만 생성 하기, 중간에 가로 챌수 없게 하기 위해 
  * `path` : 해당 `URL` 이 들어간 곳 아래 `URL` 에서 사용 가능
    * `URL`가 다르면 쿠키를 다시 발급 하자! 
  * `signed` : 암호화 할 것인지
    * `true` : 암호화 o 
    * `false` : 암호화 x 

<br>

* `value`에 한글을 넣고 싶다면 `encodeURIComponent` 를 사용 해야 됨
  ```javascript
  req.cookie('name', encodeURIComponent('홍길동'), {})
  ```

### 


### 쿠키 삭제 
```javascript
app.get('/', (req, res)=>{
    req.clearCookie('name', {
        httpOnly : true,
        path: '/',
    })
})
```
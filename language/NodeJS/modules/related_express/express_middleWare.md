# MiddleWare in Express

***

> Express 모듈을 사용할 떄 사용 되는 것으로 전체 API 에 공통적으로 사용 된다.  
> 다양한 미들웨어가 있으며 미들웨어의 순서가 중요하다.  
> 순서에 따라 생략할 수 도 있고 불필요한 자원이 생길 수 도 있으니 주의 하여야 한다.

<br>
<br>
<br>


## 기본 사용법  
***


#### 일반 서버 코드

```javascript
const express = require('NodeJS/modules/related_express/express')
const app = express()

app.set('port', 3000)


// use 를 이용해서 미들웨어 등록
app.use((req, res, next) => {
    console.log('this is MiddleWare!!! ')
    // next() 를 사용하지 않으면 해당 미들웨어에서 끝이나서 
    // 다음 라우터 를 탐색하지 않는다.
    // 따라서 next를 꼭 사용을 해야한다.
    // 또는 의도적으로 next를 하지 않아 라우터 접근을 못하게 하는 방법도 있다. 
    next();
})

// Router

app.get('/', (req, res) => {
    res.send('hello')
})

app.get('/aobut', (req, res) => {
    res.send('this is about')
})

app.get('/next', (req, res) => {
    res.send('this is next page')
})


// Error 핸들러로 사용된 미들웨어
// 에러가 터지면 이리로 온다!!
app.use((err, req, res, next) => {
    console.log(err)
    res.status(500).send(err.message);
})


app.listen('3000', () => {
    console.log('Server is Run!!')
})


```


<br>
<br>


## 예제
***

### 상황 
> 많은 Router 가 있고 모든 Router 시작 시간을 표시하고 싶다!

### 방법 1. 모든 API 에 코드를 넣는다?
```javascript
// server.js

app.get('/', (req, res)=>{
    console.log(new Data())
    res.send('hello')
})

app.get('/aobut', (req, res)=>{
    console.log(new Data())
    res.send('this is about')
})

app.get('/next', (req, res)=>{
    console.log(new Data())
    res.send('this is nextpage')
})

```

> 일일이 넣어 주어야 하므로 개발자 사망 예정

<br>

### 방법 2. MiddleWare 사용

```javascript

app.use((req, res, next)=>{
    console.log(new Date())
    next()
})

app.get('/', (req, res)=>{
    res.send('hello')
})

app.get('/aobut', (req, res)=>{
    res.send('this is about')
})

app.get('/next', (req, res)=>{
    res.send('this is nextpage')
})

```

> 미들 웨어 한 줄이면 끝
> express router 는 위에서 아래로 진행되기 때문에 use 가 제일 먼저 호출된다. 
> next 없으면 멈추니 주의!!
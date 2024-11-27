# bodyParser Module

***

<br>

> 해당 모듈은 express에서 쉽게 사용하게끔 대체 되었다.   
> express.json 을 사용하면 된다. 

<br> 
<br> 
<br> 

## 사용법
***

### import
```javascript
const express = require('express')
const app = express()

// JSON 데이터 
app.use(express.json())

// Form - data 
app.use(express.urlencoded({extened: true}))
```
* `urlencoded` : `Form-data` 보낼떄 
  * `extended` 
    * `true` : `qs` 사용 -> 성능이 더 좋으니 웬만 하면 `true` 로 넣기 
    * `false` : `querystring` 사용 

<br>

### JSON, Form-data 데이터 꺼내기
```javascript
apt.get('/', (req, res)=>{
    // req.body : JSON 데이터 
    req.body.name
})
```
* req.body == JSON 이다. 
* #### [주의] form-data 의 경우 이미지, 파일을 읽을 수가 없다!! 
  * `multer`, `busboy` 를 이용

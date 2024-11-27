## .ENV

> 프로젝트 코드에 시크릿 값을 그대로 넣으면 안되기 때문에 ( 보안 및 악용 이유 )  
> Key 와 같이 중요한 변수들은 .env 파일로 분리를 해준다. 



## 사용법 
### `.env`
```shell
//.env 파일 생성
키=값
키=값

// 이런식으로 작성을 한다. 
ex) 
COOKIE_SECRET=aadfjlejaf
```

### `app.js`
```javascript
const dotenv = require('dotenv')

dotenv.config()

app.use(cookieParser(process.env.COOKIE_SECRET))
// app.use(cookieParser(aadfjlejaf))
```
* `.env` 파일 안에있는 키값이 value로 변경이 된다. 
* `.env` 파일에 없는 value로 넣는다면 에러!
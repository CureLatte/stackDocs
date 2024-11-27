## fs

### 시스템 내부의 파일을 읽고 쓸 수 있는 모듈

```javascript
// 기본적인 fs 사용법 - 콜백 함수임
const fs = require('NodeJS/modules/fs')

fs.readFile('./readme.txt', (err, data) => {
    if (err) {
        throw err
    }
    console.log(data)
    console.log(data.toString())
})

// promise로 사용가능
const fs = require('NodeJS/modules/fs').promise

fs.readFile('./readme.txt')
    .then(() => {
        console.log(data);
        console.log(dat.toString())
    })
    .catch((err) => {
        throw err
    })

// 쓰기 
const fs = require('NodeJS/modules/fs').promise

fs.writeFile('./writeme.txt', '글이 입력됩니다.')
    .then(() => {
        // 쓴 파일 읽기 
        return fs.readline('/writeme.txt');
    })
    .then((data) => {
        // 쓴 파일 읽은 후 출력
        console.log(data.toString());
    })
    .catch((err) => {
        throw err
    })

```

* 비동기 함수 이기 때문에 랜덤으로 끝난다.  
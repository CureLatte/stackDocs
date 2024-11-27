## OS

### 컴퓨터에 대한 정보를 얻을 수 있는 모듈로 이미 export 되어 있으니 바로 사용하면된다. 

```javascript
const os = require('os')

// cpus의 갯수를 알려주는 함수 os.cpus()
console.log(os.cpus());
```


### 그 외에 자주 쓰는 메소드들 

* `os.arch()` : `process.arch` 와 동일 
* `os.platform()` : `process.platform` 과 동일 
* `os.type()` : 운영 체제의 종류 
* `os.uptime() `: 운영 체제 부팅 이후 흐른 시간을 보여줌
  * `process.uptime() `은 실행 시간
* `os.hostname()` : 컴퓨터 이름
* `os.release()` : 운영 체제의 버전 
* `os.homedir()` : 홈 디렉터리 경로 보여 주기
* `os.tmpdir()` : 임시 파일 저장 경로 보여 주기
* `os.cpus()` : 컴퓨터 코어 정보 
* `os.freemem()` : 사용 가능한 메모리 
* `os.totalmem()` : 전체 메모리 용량




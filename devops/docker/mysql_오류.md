## Docker MYSQL 사용시 오류 발생

### 상황
* 예제 파일 실습하다 mysql를 이미지로 빌드를 해야하는데 되질 않음 

### 실행 코드 
```shell
docker pull mysql 
# 또는 
docker run mysql
```

### 에러 코드 
```shell
no matching manifest for linux/arm64/v8 in the manifest list entries
```

### 원인 (예상) 
* 리눅스 버전이 아니라 서 그런것 같다.


### 해결
* 명령어 중간에 `--platform linux/amd64` 를 붙여 준다. 
```shell
docker pull --platform linux/amd64 mysql 
```

* dockerfile 에 `platform` 을 적어 준다. 
```shell
# dockerfile
version: '3.8'

services:
  mysql:
    image: mysql 
    # platform 작성
    platform : linux/amd64
    .
    .
    .
```
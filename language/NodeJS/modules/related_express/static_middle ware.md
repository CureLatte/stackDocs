# Static 파일 미들웨어
***

> `express` 에서 제공 하는 미들 웨어로 정적인 파일 즉 static 파일을 제공 해주는 것


<br>
<br>

## 사용법
***
### 요청 경로 마다 생성
```javascript
// static 미들웨어 사용
app.use('요청 경로', exress.static('실제 경로'))
```

### EXpress

## Console 

### 알아 두면 유용한 Console Method

* console.time, console.timeEnd : 시간 로깅
```javascript
console.time('hello')

// 작업내역

console.timeEnd('hello')

// 작업 내용에 까지의 시간이 출력 
```

* console.log : 평범한 로그 
```javascript
console.log('hellow!')

// 콘솔창 //
// hellow!
```


* console.error : 에러 로깅
* console.dir : 객체 로깅

```javascript
const obj = {
    a : 'hello',
    b : 'hellow 2'
}

console.dir(obj)
// 콘솔 창 // 
// [a: 'hello', b: 'hellow 2']
```
* console.trace : 호출 스택 로깅
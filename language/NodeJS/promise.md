## 프로미스

* 내용이 실행은 되었지만 결과를 아직 받환하지 않은 객체 
* 프로미스는 기본적으로 동기지만 .then 으로 가면 동기화 


```javascript

const condition = true;
const promise = new Promise((resolve, reject)=> {
    if(condition){
        resolve('성공')
    } else {
        reject('실패')
    }
});

// 다른 코드 삽입 

promise
    .then((message) => {
        console.log(message);
    })
    .catch((error) => {
        console.log(error)
})
// 성공할 경우 .then 으로 
// 실패할 경우 .catch 로 




const promise = setTimeoutPromise(3000)

console.log('딴짓')
console.log('딴짓')
console.log('딴짓')
console.log('딴짓')
console.log('딴짓')
console.log('딴짓')
console.log('딴짓')
console.log('딴짓')
console.log('딴짓')

// 난 지금 실행할꺼야!!
promise.then(promise)


```

* `Then` -> 결과를 반환함 
* 성공 했을 때 `Resolve` -> `Then` 으로 연결
* 실패 했을 때 `Reject` -> `Catch` 로 연결
* `Finally` 는 무조건 실행

* 이를 확장한 것이 async/ await 임으로 Promise 와 똑같이 사용 가능
* 하지만 Reject 할 경우를 처리를 못하기 때문에 
* `try - catch` 로 처리

```javascript
async
```
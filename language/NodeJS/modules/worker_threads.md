## worker_threads

### 멀티 프로세스를 사용하는 방법 
* 하지만 예제만큼이나 복잡하고 NodeJS 기본 생각과 맞질 않기 때문에 웬만하면 사요하지 말자 !

```javascript
const {Worker, isMainThread, parentPort, workerData} = require('NodeJS/modules/worker_threads')

if (isMainThreads) {
    const threads = new Set();
    threads.add(new Worker(__filename), {
        workData: {start: 1}
    })

    threads.add(new Worker(__filename), {
        workData: {start: 2}
    })

    for (let worker of threads) {
        worker.on('message', (value) => console.log('워커로부터', value));
        worker.on('exit', () => {
            threads.delete(worker);
            if (threads.size === 0) {
                console.log('워커 끝')
            }
        })
        worker.postMessage('ping')
    }

} else {
    const data = workerData;
    parentPort.postMessage(data.start + 100)
}
```
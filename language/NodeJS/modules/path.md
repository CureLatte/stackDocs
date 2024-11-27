## path

```javascript
const path = require('NodeJS/modules/path');

path.join(__dirname, 'var.js');

// 운영체제에 따라 다르게 경로를 지정해줌
// mac : ~\dirname\var.js 
// window : ~/dirname/var.js

path.resolve(__dirname, '..', '/var.js');
// resolve에 절대 경로 가 있다면 앞부분을 무시 
// join 은 절대경로가 있어도 상대경로로 진행

path.normalize('C://users\hellow\hello')
// normalize : 해당 경로를 정리를 해준다.


```
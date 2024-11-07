# Routing 
*** 
`Nest JS` 에서는 `NODE` 의 방식과는 다르게 `Routing` 이 된다.


`JAVA Spring` 에서 `Bean Container` 처럼 등록을 시켜줘야한다.

<br>

### 기본 작성법
*** 

우선 `Routing` 할 `Controller` 를 `class` 로 작성한다.


``` typescript
class TestController{
    

}

export default TestController
```



여기에 `@Controller` 라는 `Annotation` 을 달아주면 `Routing` 역할을 할 수 있는 
`Controller` 가 된다.


``` typescript

import { Controller} from '@nestjs/common';

@Controller()
class TestController{
    

}

export default TestController
```

`Import` 는 `@nestjs/common` 으로 한다.

이 때 한가지 `Java` 와 다른점이 있다면 함수 호출을 해야한다는 점이다.


또한  `Url PreFix` 를 하려면 해당 함수에 인자로 `URL` 명을 입력한다.


즉 `https://localhost:3000/user` 에 대항하려면 

``` typescript

import { Controller } from '@nestjs/common';

@Controller('user') // <- /user 라고 작성해도 동일 함
class TestController{
    

}

export default TestController
```

라고 해야한다.

마지막으로 `AppModules` 에 등록을 시켜야하는데 

`JAVA` 에서는 자동으로 `@Component` 에 해당하는 `class` 를 탐색하지만  
`NestJS` 에서는 해당 과정이 없어서 `app.modules.ts` 라는 파일에 등록을 시켜야한다.

`app.modules.ts` 파일은 프로젝트 생성될 때 같이 생성되는 파일이다.

```typescript
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import TestController from './TestController';

@Module({
  imports: [],
  controllers: [AppController, TestController], // 여기에 넣어주면 됨
  providers: [AppService],
})
export class AppModule {}


```


<br>

### Method 분류
*** 

`Method` 는 해당 함수마다 `Annotation` 으로 구분한다.


``` typescript

import { Controller, Post, Get, Put, Delete} from '@nestjs/common';

@Controller('user') // <- /user 라고 작성해도 동일 함
class TestController{
    
    @Get() // GET 요청
    public getFunctionName(){}
    @Post() // POST 요청
    public postFunctionName(){}
    @Put() // PUT 요청
    public putFunctionName(){}
    @Delete() // DELETE 요청
    public deleteFuntionName(){}
}

export default TestController
```

<br>

### `Request`, `Response` 제어
*** 

우선 범용적으로 사용하는 `Request` 는 `@Req` 를 이용하여 해당 함수의 인자로 등록하며   

`DTO` 를 사용할 경우엔 `@Body` 라는 `Annotation` 을 사용한다.  

`Request` 는 `@Res` 로 감싸서 진행한다.  

이때 `Interface` 호출을 `express` 에서 해야 `Node` 에서 사용한 `status` 를 지정하고 내려줄 수 있다.


``` typescript
// 테스트를 위한 Request Dto
export default class TestDto{
    firstParams: string;
    secondParams: number;
}

```


``` typescript

import { Controller, Post, Put, Req, Res, HttpStatus} from '@nestjs/common';
import { Response, Request } from 'express'
import TestDto from 'TestDto'

@Controller('user')
class TestController{
    
    @Post()
    public postFunctionName(@Req() req: Request, @Res() res: Response){
        // HTTPSTATUS 상태 코드도 존재함
        return res.status(HttpStatus.Ok).json({
            ok: true
        })
    }
    
    
    @Put() 
    public putFunctionName(@Body() testDto: TestDto, @Res() res: response){
        return res.status(HttpStatus.Ok).json({
                ok: true
            }) 
    }
}

export default TestController
```

<br>

### Params/ Query 구분 
***

`Controller` 에서 `Routing` 분기로 자주 사용하는   
`Params` 와 `Query` 는 `@Params`,  `@Query` 으로 구분한다.  
`Params` 의 경우 `Method` 에 `:` 으로 시작하여 변수명을 지정해주면 된다.  
`Query` 의 경우 사용하는 `key` 값을 함수에 넣어주거나 `DTO` 를 사용하면 된다.  



``` typescript

import { Controller, Get, Req, Res, Param, Query, HttpStatus} from '@nestjs/common';
import { Response, Request } from 'express'
import TestDto from 'TestDto';

@Controller('user')
class TestController{
    
    @Get()
    public queryFunctionName(@Query('testKey') query: string, @Res() res: Response){
        return res.status(HttpStatus.Ok).json({
            ok: true
        })
    }
    
    @Get()
    public queryDtoFunctionName(@Query() testDto: TestDto, @Res() res: Response){
        return res.status(HttpStatus.Ok).json({
            ok: true
        })
    }
    
    
    @Get(':id') 
    public paramsFunctionName(@Param() id: String, @Res() res: response){
        return res.status(HttpStatus.Ok).json({
                ok: true
            }) 
    }
}

export default TestController
```

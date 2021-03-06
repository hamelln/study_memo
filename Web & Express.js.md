## 동적 웹의 구현법

1. CSR (Client-Side-Rendering)

```txt
프론트엔드에서 동적인 부분을 처리하는 방식.
프론트엔드에서 거의 다 하고, 백엔드하고는 API를 통해 데이터만 주고 받는 정도.
API 호출이 완료된 이후에 내용이 보이지만 빠르다.
복잡, 큰 프로젝트할 때 하기 좋다.
```

2. SSR (Server-Side-Rendering)

```txt
백엔드 서버에서 페이지 영역을 처리한 다음 프론트엔드로 보내는 방식.
프론트엔드는 HTTP 응답으로 표시만 하고, 백엔드가 다 한다.
백엔드에서 HTML을 처리하고, CSR보다 간단하다.
상대적으로 느려보이고 페이지를 이동할 때마다 리로드하기 때문에 깜빡인다.
```

## 웹 프레임워크

```txt
웹을 구현할 때 일일이 만들면 낭비가 심하다.
웹 프레임워크는 정형화된 부분을 빠르게 구현하도록 도와준다.
ex) HTTP 요청(Request), 응답(Response) 처리, Routing, HTML Templating 등...

Node.js의 프레임워크로 유명한 건 Express.js가 있다.
```

## Express.js

- 모든 동작이 명시적.
- 필요한 기능 간단하게 추가.
- 유연한 구조 설정
- 웹 프레임워크 동작 방식의 이해 용이.


```txt
$ npm init
$ npm i express
```

```javascript
const express = require('express');

const app = express();

app.get('/', (req, res) => {
    res.send("Hello, express");
});

app.listen(3000, () => {
    console.log("SERVER STARTED");
})
```

```txt
$ npm start 

이러면 localhost:3000으로 서버가 시작된다.
```


```txt
$ npm i -g express-generator

$ express '프로젝트 명'

$ cd '프로젝트 명'

$ npm i

$ npm start

이렇게 해도 localhost:3000으로 서버가 시작된다.
```

### express.js 프로젝트 구조에 대해

```txt
app.js : 메인이 되는 파일
public : 코드와 무관한, 직접 제공하려는 파일 디렉토리
package.json : 의존성, 스크립트 정의
routes : 라우팅 파일 디렉토리
views : HTML Template 디렉토리
bin / www : Express.js 실행 담당
```

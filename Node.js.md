# 1. Node.js란?

```
 옛날 WEB 1.0 시절에 유튜브나 SNS같은 게 없던 시절, 사용자는 웹에서 정보를 보기만 했다.

 WEB 2.0로 접어들면서 게시판, 블로그, 댓글 등으로 사용자가 컨텐츠를 생산하기 시작했다.
이를 처리하려면 좋은 js 실행기가 필요했고 구글의 V8(js 엔진)이 등장했다.

 V8 엔진은 구글에서 만들었기에 구글 크롬 브라우저, 안드로이드 브라우저에 탑재돼있다.
개발자는 어느 환경에서나 이 V8 엔진처럼 js를 돌리고 싶었다.

 그리고 Node.js가 등장했다. Node.js는 어디서나 js를 돌릴 수 있는 실행기다. 
브라우저에 국한되지 않아 자유로운 개발이 가능다.
```

## 2. Node.js로 할 수 있는 것
    React.js, Express.js, React-Native, Brain.js, Electron...

## 3. Node.js의 특징

- ### 싱글 스레드

```txt
장점 : 동기화 문제 등을 신경 쓰지 않아도 된다.
단점 : 멀티 스레드가 필요한 작업에는 비효율적이다.
```
        
- ### 비동기
    
```txt
싱글 스레드를 보완하기 위해 비동기 동작을 더했다.

싱글 스레드 : 한 번에 한 가지 동작만 하고, 한 가지 동작이 끝날 때까지 기다린다.
비동기 : 동작을 실행하고, 완료가 되기까지 기다리지 않고 다음 동작을 실행한다.
```
    
- ### 이벤트 기반

```txt
비동기를 사용할 경우 동작이 끝난 뒤의 행동을 미리 함수로 등록해둔다.
이를 이벤트 등록이라고 한다.
```

## 4. 이벤트 루프

    이벤트를 처리하는 반복 동작
    
Node.js가 비동기 이벤트 동작을 처리하는 일련의 loop로서 구성요소는 다음과 같다.

- Call Stack

```txt
함수를 넣는 스택.
이벤트 루프는 콜스택이 빌 때까지 스택에 있는 함수들을 실행한다.
```

- Message Queue

```txt
setTimeout같은 지연 함수를 넣는 큐.
1. 메세지 큐에 등록했다가,
2. 지정한 시간이 지나고,
3. 콜스택이 비워지면!
4. 그제야 내부 함수는 메시지 큐 -> 콜스택으로 이동 후 실행.
```

![image](https://user-images.githubusercontent.com/39308313/144356805-87e7041c-7ca9-41ed-9cf5-5af3c9bf1c52.png)

```javascript
function a() {
  console.log('a');
}

function b() {
  console.log('b');
}

function c() {
    setTimeout(b, 0);
    a();
    console.log('c');
}

c();
```

```txt
위와 같은 코드를 돌렸을 때 아래와 같은 상태가 된다.
Call Stack: [c, a]
Message Queue : [ b ]
따라서 a -> c를 실행해서 콜스택을 비운 뒤에 메시지 큐에 있는 b가 콜스택으로 이동한 뒤 출력된다.
```

![image](https://user-images.githubusercontent.com/39308313/144221789-50c7f629-7fa5-4ec8-90b1-6ab53ed34199.png)

- Job Queue

```txt
Promise에 등록된 Callback을 넣는 큐.
자기의 상위 함수가 '종료되기 전'에 함수를 콜스택으로 옮긴다.
메세지 큐와 달리 콜스택이 안 비어도 된다.
```

## 5. 모듈

    프로젝트는 큰데 한 파일에 코드를 다 집어넣으면?
    
```txt
당연히 위험하다. 따라서 코드를 분리해야 한다.
모듈은 코드를 분리하기 위한 방법이다.
npm을 하면서 패키지를 설치하는데, 패키지는 여러 모듈의 모음이다. 이름부터 node_modules다.

모듈의 예로는 console, process, fs, HTTP, url, path 등이 있다.
```

### ES Module, commonjs 

```txt
ES Module은 export, import를 쓴다.
commonjs는 module.exports, require를 쓴다.
```

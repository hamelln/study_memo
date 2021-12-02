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
setTimeout은 V8 소스 코드에 없다.
브라우저에서 제공하는, js가 실행되는 런타임 환경에 있는 API이다.
1. stack에 setTimeout이 올라간다.
2. 내부 함수는 WepAPIs로 이동한 뒤, 카운트 다운을 한다.
3. 그동안 콜 스택은 함수들 실행하며 자기 할 일 한다.
4. 카운트 다운이 끝나면 task queue, 혹은 message queue로 함수가 이동한다.
5. 콜 스택이 다 비면 그제야 콜스택으로 이동 후 실행한다.

※ 구글엔 message queue vs task queue라는 주제가 있다.
둘이 다른 모양인데, 검색해서 알아보면 좋을 듯하다.
```

![image](https://user-images.githubusercontent.com/39308313/144356805-87e7041c-7ca9-41ed-9cf5-5af3c9bf1c52.png)

![image](https://user-images.githubusercontent.com/39308313/144360100-d6a69889-18f0-4e8e-a8c7-e835ed323bbb.png)

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

![image](https://user-images.githubusercontent.com/39308313/144221789-50c7f629-7fa5-4ec8-90b1-6ab53ed34199.png)

```txt
Call Stack: [c, a]
Message Queue : [ b ]
따라서 a -> c를 실행해서 콜스택을 비운 뒤에 메시지 큐에 있는 b가 콜스택으로 이동한 뒤 출력된다.

Q) 만약 아래처럼 코드를 짜면 어떻게 될까?
```

```javascript
function c() {
    setTimeout(b, 100);
    setTimeout(a, 0);
    console.log('c');
}
```

```txt
Call Stack : [c]
Message Queue : [a , b]
가 된다.
b는 100ms 뒤에 Call Stack으로 가는 게 아니라, 100ms 뒤에 Message Queue로 간다.
따라서 a가 먼저 메시지 큐에 들어갔기 때문에 a -> b 순으로 콜스택에 들어간다.
```

## 그래서 이거 왜 쓰는데?

![image](https://user-images.githubusercontent.com/39308313/144360746-b051a3da-561b-45f2-9efc-78e823293359.png)

```txt
setTimeout은 예시이다. setTimeout만 저렇게 돌아가는 게 아니다.
HTML에서 onClick()이벤트 처리 등도 이런 식으로 적용이 된다.
```

![image](https://user-images.githubusercontent.com/39308313/144361895-85407884-7049-4d0e-bb6d-c122ea7140db.png)

```txt
위 코드에서 그냥 forEach를 돌리면 각 index마다 console.log()를 동기적으로 돌린다. 

async로 돌릴 경우는 아래와 같이 된다.
```

![image](https://user-images.githubusercontent.com/39308313/144361671-f3a8b498-dc4b-4772-bb56-e68ed2823b09.png)

```txt
각 index마다 바로 콜스택을 비우는 게 아니라 큐에 집어넣는다.
```

### 왜 이렇게?

    콜스택을 비우기 전까진 다른 작업을 못한다!

```txt
몇 개 console.log 찍는 건 금방이니까 괜찮지만 시간이 오래 걸리는 작업이면?
콜스택 비우는 거에 시간을 너무 소모한다.

브라우저는 매 16.6ms마다 (60fps) 화면을 repaint한다.
render도 콜백처럼 작동하며 큐에 들어간다.
(단, 우리가 작성한 콜백보다 더 우선된다.)

그런데 스택에 코드가 있으면? 
스택에 못 들어가기 때문에 redering을 못한다.

렌더를 못하면?
텍스트 선택, 클릭 등 이벤트 작동도 다 막힌다.

이를 테면 마우스 스크롤 이벤트를 동기적으로 작동하면?
엄청 많은 함수들이 발생해서 스택에 쌓일 것이고,
스크롤을 내리는 동안 다른 짓을 못한다.

따라서 필요에 따라 비동기로 작동시키는 것이다.
```





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

# 비동기를 쓰는 방법에 대하여

## 1. 무슨 방법들이 있을까?
1. callback
2. Promise
3. async & await

### 2. callback

```javascript
function findUser(id, callback){
  const user = {...};
  callback(user);
  }
```

```txt
그러나 callback은 callback 지옥에 빠질 수 있기 때문에 Promise가 나왔다.
```

### 3. Promise

```javascript
  Data.getPromise()
    .then(res => res.json)
    .then(result => ...)
    .catch(...);
```

```txt
Promise를 쓰면 위와 같이 가독성이 좋게 쓸 수 있다.
getPromise로 Promise객체를 받아오는데, 
resolve(정상 작동)일 땐 then을 돌리고, reject(반려)되면 catch를 돌린다.
```

### callback 기반을 Promise로 바꿔보자.

```javascript
function getPromise(params) {
  return new Promise((resolve, reject) => {
    findUser(params, (error, user) => {
      if(error) {
        reject(error);
        return;
      }
      resolve(user);
    });
  });
}
```

### 4. async & await

    ※ async, await는 Promise와 다른 문법이지 '완전 상위호환 문법'은 아니다.

```javascript
async function test() => {
  const inner = await func();
  const inner2 = await func2(inner);
  ...
}
```

```txt
inner2는 inner가 끝날 때까지 기다린다.(await)
```

    ※ async 함수는 기본적으로 Promise를 리턴한다.
    
```javascript
//아래 세 코드는 동일한 뜻이다.

async function foo() { return 1 }

const foo = async() => 1;

function foo() { return Promise.resolve(1) }

//아래 네 코드는 동일한 뜻이다.

function foo() {
    const apple = "apple"
    return Promise
            .resolve(apple)
            .then(result => console.log(result));
}

function foo() {
    const apple = "apple"
    return Promise
            .resolve(apple)
            .then(console.log);
}

async function foo() {
    const apple = await "apple";
    console.log(apple);
}

const foo = async() => {
    const apple = await "apple";
    console.log(apple);
}
```

### async, await는 Promise와 오류 캐치 문법이 다르다.

```javascript
// 아래와 같이 try - catch 구문을 쓴다.

async function test(param) {
  try{
    const inner = await func();
    ...
  } catch(e) {
    e => console.log(e);
  }
}
```

### async를 잘 쓰는 방법.

```javascript
// bad()를 돌리면 r1에서 1초, r2에서 2초가 걸려 총 3초가 지난 뒤에 log를 찍는다.

async function bad() {
    const r1 = await resolveAfter1Seconds();
    const r2 = await resolveAfter2Seconds();
    console.log(r1,r2);
}


// good()을 돌리면 r1,r2를 동시에 돌리기 때문에 2초 뒤에 log를 찍는다.

async function good() {
    const [r1, r2] = await Promise.all([
        resolveAfter1Seconds(),
        resolveAfter2Seconds(),
    ]);
    console.log(r1,r2);
}

```

# ECMAScript 6에 대하여

## 1. ES6란?
    JavaScript의 표준 문법이다.
    
```txt
2015년에 나왔고, 이후로도 많은 문법이 추가됐다.
```

## 2. 왜 쓸까?

    생산성 향상에 도움을 준다.
    
```txt
옛날 js는 var를 써서 hoisting 문제가 있지만
ES6이후로 let, const를 권장하며 이 문제들이 다소 해결됐다.
이외에도 화살표 함수, class, destructing 등 여러 편리한 문법이 추가됐다.
```

```javascript
// 옛날 문법
var name = "HY";
var str = "my name is " + name + "!";

// 최신 문법
const name = "HY";
let str = `my name is ${name}!`;
```

## 3. 어떻게 쓰지?

    Node.js로 쓴다.
    
```txt
Node.js는 ES6의 '모든' 문법은 지원 안 하지만 많은, 최신 문법을 지원한다.
```

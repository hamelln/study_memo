## Typescript

  ES2015부터 '모듈'스펙을 제공하기 시작한다.
  트랜스파일러(Babel, Typescript 등) 등장.
  npm, 번들러(Webpack) 등장.
  
Typescript는 javascript의 슈퍼셋.
js의 모든 기능 + 추가 기능 제공
Type(유형) + script => 명시적인 데이터에 대한 유형이 설명 가능

```javascript
let age = 10;
let age = '10'
let age = true;
let weight = 75;
```

```typescript
let weight: number = 80;

type age = number;
let num: age = 10;

type myColor = 'red' | 'orange';
let color: myColor = 'black';
(error!)
let color: myColor = 'red';
(good)
```

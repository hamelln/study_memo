# NPM이란?

    Node Package Manager
    
```txt
Node.js 프로젝트를 관리한다.
온라인 저장소 : 오픈소스 라이브러리, 도구들이 업로드된다.
커맨드라인 툴 : 프로젝트 관리를 위한 명령어를 제공한다.
- 저장소에서 라이브러리, 도구 설치
- 프로젝트 설정 및 관리
- 프로젝트 의존성 관리
```

## 예시

```
$ npm init

Node.js 프로젝트를 생성하는 명령어다. 실행하면 프로젝트에 package.json이 생긴다.

$ npm i eslint

eslint를 설치하겠다는 명령어다. npm install eslint와 똑같은 말이다.
이런 식으로 라이브러리(혹은 패키지)를 설치하는 등의 행동을 의존성(dependencies) 관리라고 부른다.
설치를 하면 package.json의 dependencies, node_modules에 추가된다.

$ npm i eslint --save-dev

--save-dev는 개발용 의존성에 쓰는 명령어다.
배포할 때는 쓸 일 없는 라이브러리를 설치할 때 쓴다.
개발용 의존성은 package.json의 devDependencies에 추가된다.
```

![image](https://user-images.githubusercontent.com/39308313/144236491-60173ccb-a1a1-484e-8c6f-830af7e9d512.png)

![image](https://user-images.githubusercontent.com/39308313/144236436-64a386ea-67fc-492e-8a38-ee3ee178c226.png)

## node_modules 폴더는 따로 업로드를 하지 않는 대상이다.


```txt
1. 의존성이 늘어날수록 라이브러리가 차지하는 용량이 커질 것이고,
2. 운영체제마다 실행하는 코드가 제각각이 될 것이기 때문.

$ npm install

이것만 쓰면 package.json에 적힌 의존성들을 알아서 필요한 만큼 node_modules에 내려받는다.

$ npm install --production

개발용 의존성을 제외하고 내려받겠다는 뜻이다.

$ npm remove eslint

eslint 의존성을 제거하겠다는 얘기다.
```

## package-lock.json

```txt
원래는 의존성을 그냥 추가하면 자동으로 최신 버전이 깔린다.
진행하던 프로젝트에 쓰던 의존성을 그대로 쓰려면 그 버전을 따로 써야한다는 얘기.
package-lock.json은 설치된 버전을 고정한다.
```

## local package, global package

```txt
로컬 패키지는 해당 프로젝트의 package.json에 적혀있고, node_modules에 있는 패키지다.
전역 패키지는 npm install -g || npm install -global로 설치한, 전역 패키지 저장소에 저장된 패키지다.

프로젝트에 쓸 패키지는 가급적 전역 패키지보단 로컬 패키지를 활용하자.
```

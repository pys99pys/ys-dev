# Babel vs Polyfill

## Babel

최신 JavaScript 코드를 구버전에서도 동작하도록 변환(트랜스파일링, Transpiling)하는 도구(ex: ES6+ -> ES5 문법으로 변환)

### Babel이 하는 일 예시

- 화살표 함수 (=>) -> 일반 함수로 변환
- const, let -> var로 변환
- 클래스 (class) -> 함수 기반 코드로 변환
- 전개 연산자(...) -> Object.assign() 등으로 변환
- 옵셔널 체이닝 (?.) -> && 연산자로 변환

### Babel 변환 전 후 비교

**ES6 코드 (Babel 변환 전)**

```
const sayHello = (name) => console.log(`Hello, ${name}!`);
sayHello("Alice");
```

**Babel 변환 후 (ES5 코드)**

```
"use strict";

var sayHello = function sayHello(name) {
  console.log("Hello, " + name + "!");
};
sayHello("Alice");
```

## Polyfill

브라우저에서 지원하지 않는 최신 기능을 추가하는 코드 또는 라이브러리(ex: Promise, fetch, Object.assign() 같은 기능이 없는 구버전 브라우저에서도 동작 하도록 추가)

### Polyfill이 필요한 경우

- Array.prototype.includes() -> 오래된 브라우저에서 없음
- fetch() -> IE에서는 기본적으로 지원되지 않음
- Promise -> ES6 이전에는 존재하지 않음

### Polyfill 추가 후 코드

**Array.prototype.includes()가 없는 브라우저에서 Polyfill 사용**

```
if (!Array.prototype.includes) {
  Array.prototype.includes = function (searchElement) {
    return this.indexOf(searchElement) !== -1;
  };
}
```

## 차이점 정리

|  | **Babel** | **Polyfill** |
|---|---|---|
| **목적** | 최신 JS 문법을 구문 변환(트랜스파일) | 최신 JS 기능을 지원하지 않는 브라우저에서 사용 가능하게 함 |
| **변환 대상** | `const`, `class`, `()=>`, `...` 같은 문법 | `fetch()`, `Promise`, `Object.assign()` 같은 기능 |
| **실행 방식** | 트랜스파일링 (컴파일 단계에서 변환) | 런타임(실행 시점)에서 기능 추가 |
| **필요한 브라우저** | 구버전 브라우저에서도 최신 문법을 사용 가능 | 브라우저에서 기능이 없을 경우 추가 |

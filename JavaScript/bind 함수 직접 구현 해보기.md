# bind 함수 직접 구현 해보기

## 코드

```
Function.prototype.myBind = function (thisArg, ...args) {
  const fn = this; // 원본 함수 참조

  return function (...newArgs) {
    return fn.apply(thisArg, [...args, ...newArgs]);
  };
};
```

## 동작

- thisArg: this로 사용할 객체
- args: 미리 고정할 인자들
- newArgs:	바인딩된 함수가 호출될 때 전달될 인자들
- apply 사용 이유: this와 인자를 함께 설정하기 위함

## 예제 코드

```
function greet(greeting, name) {
  console.log(`${greeting}, ${name}! My name is ${this.name}.`);
}

const person = { name: 'ys' };
const greet = greet.myBind(person, 'Hello');

greet('wj'); // 출력: Hello, wj! My name is ys.
```

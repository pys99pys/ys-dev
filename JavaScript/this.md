# this

함수가 호출되는 방식에 따라 참조하는 객체가 동적으로 결정되는 특별한 키워드

## 기본 문맥에서의 this

- 브라우저 환경에서는 전역 객체인 `window`, Node.js 환경에서는 전역 객체 `global`
- 엄격 모드에서는 `undefined`

## 일반 함수 호출에서의 this

- 기본적으로 전역 객체(`window` 또는 `global`)
- 엄격 모드에서는 `undefined`

## 화살표 함수에서의 this

- 화살표 함수는 자신만의 this를 가지지 않음
- 선언된 위치의 상위 스코프의 this를 그대로 사용

```
const person = {
  name: "Alice",
  sayHello: () => {
    console.log(this.name); // 상위 스코프인 전역 객체 참조
  },
};

person.sayHello(); // undefined (브라우저에서는 window.name)
```

## 생성자 함수에서의 this

- 생성자 함수에서의 this는 새로 생성된 객체를 참조

```
function Person(name) {
  this.name = name;
}

const alice = new Person("Alice");
console.log(alice.name); // "Alice"
```

## 메서드 호출에서의 this

### 객체의 메서드

- 메서드를 호출한 객체를 참조

```
const person = {
  name: "Alice",
  sayHello: function () {
    console.log(this.name);
  },
};

person.sayHello(); // "Alice"
```

### 객체 참조가 끊긴 경우

- 호출 당시의 컨텍스트에 따라 달라짐

```
const person = {
  name: "Alice",
  sayHello: function () {
    console.log(this.name);
  },
};

const hello = person.sayHello;
hello(); // undefined(브라우저에서는 window.name)
```

## 클래스에서의 this

- 클래스의 메서드에서 this는 인스턴스를 참조

```
class Person {
  constructor(name) {
    this.name = name;
  }

  sayHello() {
    console.log(this.name);
  }
}

const alice = new Person("Alice");
alice.sayHello(); // "Alice"
```

##명시적으로 this를 바인딩

### call / apply

- 함수 호출 시 this를 명시적으로 설정 가능

```
function greet(greeting) {
  console.log(`${greeting}, ${this.name}`);
}

const person = { name: "Alice" };

greet.call(person, "Hello"); // "Hello, Alice"
greet.apply(person, ["Hi"]); // "Hi, Alice"
```

### bind

- 함수의 this를 고정한 새 함수를 반환

```
const boundGreet = greet.bind(person);
boundGreet("Hello"); // "Hello, Alice"
```

## 이벤트 핸들러에서의 this

## 기본

- 이벤트를 바인딩한 요소를 참조

```
const button = document.querySelector("button");
button.addEventListener("click", function () {
  console.log(this); // 클릭된 버튼 요소
});
```

## 화살표 함수

- 상위 스코프의 this를 참조

```
button.addEventListener("click", () => {
  console.log(this); // 상위 스코프의 this (전역 객체)
});
```

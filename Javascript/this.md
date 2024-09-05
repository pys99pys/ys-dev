## 전역

전역 객체 참조
```
// 웹 브라우저에서는 window 객체가 전역 객체
console.log(this === window); // true

a = 37;
console.log(window.a); // 37

this.b = "MDN";
console.log(window.b); // "MDN"
console.log(b); // "MDN"
```

## 함수

일반 모드에서는 window 참조
```
function f1() {
  return this;
}

// 브라우저
f1() === window; // true

// Node.js
f1() === global; // true
```

strict 모드에서는 undefined
```
function f2() {
  "use strict"; // 엄격 모드 참고
  return this;
}

f2() === undefined; // true
```

## call, apply

첫번째 인자로 전달 받은 객체 참조
```
function add(c, d) {
  return this.a + this.b + c + d;
}

var o = { a: 1, b: 3 };

// 첫 번째 인자는 'this'로 사용할 객체이고,
// 이어지는 인자들은 함수 호출에서 인수로 전달된다.
add.call(o, 5, 7); // 16

// 첫 번째 인자는 'this'로 사용할 객체이고,
// 두 번째 인자는 함수 호출에서 인수로 사용될 멤버들이 위치한 배열이다.
add.apply(o, [10, 20]); // 34
```

## bind

첫번째 인자로 전달 받은 객체 참조
```
function f() {
  return this.a;
}

var g = f.bind({ a: "azerty" });
console.log(g()); // azerty

var h = g.bind({ a: "yoo" }); // bind는 한 번만 동작함!
console.log(h()); // azerty

var o = { a: 37, f: f, g: g, h: h };
console.log(o.a, o.f(), o.g(), o.h()); // 37, 37, azerty, azerty
```

## 화살표 함수

자신의 상위 스코프
```
// 객체로서 메서드 호출
var obj = { func: foo };
console.log(obj.func() === globalObject); // true

// call을 사용한 this 설정 시도
console.log(foo.call(obj) === globalObject); // true

// bind를 사용한 this 설정 시도
foo = foo.bind(obj);
console.log(foo() === globalObject); // true
```

## 객체의 메서드

객체를 참조
```
var o = {
  prop: 37,
  f: function () {
    return this.prop;
  },
};

console.log(o.f()); // 37

function independent() {
  return this.prop;
}

o.b = { g: independent, prop: 42 };
console.log(o.b.g()); // logs 42
```

## 생성자

함수가 생성한 객체를 참조
```

function C() {
  this.a = 37;
}

var o = new C();
console.log(o.a); // 37

function C2() {
  this.a = 37;
  return { a: 38 };
}

o = new C2();
console.log(o.a); // 38
```

## DOM

이벤트를 생성한 요소을 참조
```
// 처리기로 호출하면 관련 객체를 파랗게 만듦
function bluify(e) {
  // 언제나 true
  console.log(this === e.currentTarget);
  // currentTarget과 target이 같은 객체면 true
  console.log(this === e.target);
  this.style.backgroundColor = "#A5D9F3";
}

// 문서 내 모든 요소의 목록
var elements = document.getElementsByTagName("*");

// 어떤 요소를 클릭하면 파랗게 변하도록
// bluify를 클릭 처리기로 등록
for (var i = 0; i < elements.length; i++) {
  elements[i].addEventListener("click", bluify, false);
}
```

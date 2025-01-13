# Iterable & Iterator Protocol

자바스크립트에서 객체가 반복(iteration) 가능한 객체로 작동하게 만드는 개념

## 이터러블 프로토콜(Iterable Protocol)

이터러블 프로토콜은 객체가 반복(iteration) 가능한 객체가 될 수 있도록 정의하는 규칙입니다

이 규칙은 객체에 `Symbol.iterator` 메서드를 구현하는 것이며, 이 메서드는 이터레이터(Iterator) 객체를 반환해야 함

### 프로토콜

- `Symbol.iterator`: 이 메서드는 객체가 이터러블인지 결정하며, 이터레이터 객체를 반환해야 함
- 이터러블 객체는 for...of 루프, Array.from(), spread 연산자(...)와 같은 반복 기능에서 사용할 수 있음

### 할 수 있는것

- `for...of` 루프 사용
- 스프레드 연산자(...) 사용
- `Array.from()` 사용
- `Promise.all()` 및 `Promise.race()` 사용
- 구조 분해 할당

### 예제 코드

```
const myIterable = {
  data: [10, 20, 30],
  [Symbol.iterator]: function() {
    let index = 0;
    const data = this.data;
    
    return {
      next: function() {
        if (index < data.length) {
          return { value: data[index++], done: false };
        } else {
          return { done: true };
        }
      }
    };
  }
};

for (let value of myIterable) {
  console.log(value);  // 10, 20, 30
}
```

## 이터레이터 프로토콜(Iterator Protocol)

이터레이터 프로토콜은 이터러블 객체의 `Symbol.iterator` 메서드가 반환해야 하는 이터레이터 객체에 대한 규칙을 정의

이 규칙은 `next()` 메서드를 통해 반복 가능한 값을 반환하는 동작을 담당

### 프로토콜

- `next()`: 반복할 값이 있으면 `value`와 `done` 속성을 포함하는 객체를 반환
- `value`: 현재 값(반복될 값)
- `done`: 반복이 끝났는지 여부(true/false)

### 예제 코드

```
const myIterator = {
  current: 0,
  data: [10, 20, 30],
  next: function() {
    if (this.current < this.data.length) {
      return { value: this.data[this.current++], done: false };
    } else {
      return { done: true };
    }
  }
};

console.log(myIterator.next());  // { value: 10, done: false }
console.log(myIterator.next());  // { value: 20, done: false }
console.log(myIterator.next());  // { value: 30, done: false }
console.log(myIterator.next());  // { done: true }
```

## 이터러블 프로토콜과 이터레이터 프로토콜의 관계

이터러블 프로토콜은 객체가 반복 가능한 객체가 될 수 있도록 하는 규칙이고, 이터레이터 프로토콜은 그 반복 동작을 처리하는 규칙

### 이터러블 객체는 Symbol.iterator를 정의

- `Symbol.iterator`는 이터러블 객체가 이터레이터 객체를 반환할 수 있도록 해야 함
- 이 메서드가 반환하는 이터레이터 객체는 next() 메서드를 가지고 있어야 함

### 이터레이터는 next() 메서드를 정의

- 이 메서드는 `value`와 `done을` 반환
- `done`이 `true`일 때, 이터레이션이 종료되었음을 나타냄

## 내장된 이터러블 객체

- 배열(Array)
- 문자열(String)
- Set
- Map

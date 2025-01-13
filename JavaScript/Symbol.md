# Symbol

ES6(ECMAScript 2015)에서 도입된 새로운 원시 데이터 타입 중 하나로 고유하고 변경할 수 없는 값을 만들 수 있음

Symbol은 주로 객체의 고유한 프로퍼티 키를 생성할 때 유용하게 사용됨

## 기본 개념

### 1. 고유한 값

- Symbol은 고유한 식별자를 생성할 때 사용됨
- 두 개의 Symbol이 동일한 값을 가지지 않기 때문에 같은 값을 가진 두 Symbol 객체가 절대 같지 않다는 특징이 있음

### 2. 변경 불가능

- Symbol은 한번 생성되면 값을 변경할 수 없음, 즉 그 자체로 불변성을 갖고 있음

### 3. 객체의 고유 프로퍼티 키로 사용

- Symbol은 객체의 프로퍼티 키로 사용할 수 있으며 이 키는 다른 코드에서 접근하거나 충돌을 일으킬 염려가 적음

## Symbol 생성

Symbol을 생성하려면 Symbol() 함수를 사용함

이 함수는 선택적인 설명을 받으며, 이 설명은 디버깅 시에만 유용하고, 실제 값에 영향을 미치지 않음

```
const symbol1 = Symbol();
const symbol2 = Symbol('description');

console.log(symbol1);  // Symbol()
console.log(symbol2);  // Symbol(description)
```

- Symbol()은 고유한 심볼 값을 생성
- Symbol('description')처럼 설명을 넣을 수 있으나, 이는 디버깅 목적일 뿐 값에는 영향을 미치지 않음

## Symbol의 고유성

두 개의 Symbol은 같은 설명을 가질지라도 절대로 동일하지 않음

```
const symbol1 = Symbol('unique');
const symbol2 = Symbol('unique');

console.log(symbol1 === symbol2);  // false
```

## Symbol을 객체의 프로퍼티 키로 사용

Symbol은 객체의 키로 사용할 때 유용함

Symbol을 사용하면 해당 프로퍼티가 고유하고 충돌할 가능성이 없음

```
const mySymbol = Symbol('id');
const obj = {
  [mySymbol]: 'value'
};

console.log(obj[mySymbol]);  // 'value'
```

## Symbol.for()와 Symbol.keyFor()

### Symbol.for(key)

전역 심볼 레지스트리에서 주어진 key에 해당하는 심볼을 찾거나, 없으면 새로 생성하여 반환

```
const globalSymbol = Symbol.for('shared');
const anotherSymbol = Symbol.for('shared');

console.log(globalSymbol === anotherSymbol);  // true
```

### Symbol.keyFor(symbol)

전역 심볼 레지스트리에서 해당 Symbol에 해당하는 key를 반환

```
const globalSymbol = Symbol.for('shared');
console.log(Symbol.keyFor(globalSymbol));  // 'shared'
```

## 예시: 고유 프로퍼티 및 숨겨진 데이터

Symbol을 사용하면 객체의 프로퍼티를 외부에서 쉽게 접근하지 못하게 숨길 수 있음

```
const secret = Symbol('secret');
const obj = {
  [secret]: 'hidden data',
  name: 'John'
};

console.log(obj.name);       // 'John'
console.log(obj[secret]);    // 'hidden data'
```

## Symbol과 ES6의 Object.getOwnPropertySymbols()

`Object.getOwnPropertySymbols()` 메서드는 객체의 심볼 프로퍼티만 반환, 일반적인 문자열 키는 포함되지 않음

```
const sym1 = Symbol('one');
const sym2 = Symbol('two');
const obj = {
  [sym1]: 'value1',
  [sym2]: 'value2',
  name: 'example'
};

const symbols = Object.getOwnPropertySymbols(obj);
console.log(symbols);  // [ Symbol(one), Symbol(two) ]
```

## Symbol을 사용한 반복

Symbol.iterator를 사용하면 객체나 배열을 반복 가능한 객체로 만들 수 있음

이는 커스텀 반복자를 정의하는 데 유용함

```
const myIterable = {
  [Symbol.iterator]: function() {
    let i = 0;
    const values = [10, 20, 30];
    return {
      next: function() {
        return i < values.length
          ? { value: values[i++], done: false }
          : { done: true };
      }
    };
  }
};

for (let value of myIterable) {
  console.log(value);  // 10, 20, 30
}
```

## 활용 예

1. 고유 프로퍼티 키: 객체에 충돌할 가능성이 적은 고유한 키를 사용하고자 할 때 유용
2. 상태 관리 및 메타 데이터: 객체의 숨겨진 정보나 메타 데이터를 안전하게 저장할 때
3. 반복자 및 이터러블: Symbol.iterator를 사용하여 커스텀 반복자를 정의하고, 객체나 배열을 반복할 수 있게 만듦


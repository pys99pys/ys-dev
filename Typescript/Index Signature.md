## Javascript의 객체 참조 문자열

Javascript Object의 key에 객체를 사용하면 key가 사용될 때마다 `.toString`가 호출된다.

```javascript
let obj = {
  toString() {
    console.log("toString called");
    return "Hello";
  },
};

let foo: any = {};
foo[obj] = "World"; // toString called
console.log(foo[obj]); // toString called, World
console.log(foo["Hello"]); // World
```

## Typescript의 Index Signature

Javascript Object의 key에 사용된 객체에 대해 자동으로 `.toString`을 호출하기 때문에 발생하는 문제를 방지하기 위해 Typescript에서 사용하지 못하도록 오류를 발생시킨다.

```javascript
let obj = {
  toString() {
    return "Hello";
  },
};

let foo: any = {};

// Error: Index Signature는 string, number 여야 함...
foo[obj] = "World";

// FIX: TypeScript는 명시적으로 호출하게 강제함
foo[obj.toString()] = "World";
```

객체의 기본 `.toString` 구현이 엉망이기 때문에 사용자가 명시적으로 처리하게 한다. 예를 들어, v8은 항상 `[object Object]`를 반환한다.

```javascript
let obj = { message: "Hello" };
let foo: any = {};

// Error: Index Signature는 string, number 여야 함...
foo[obj] = "World";

// 실제 저장 위치가 이렇게 됨!
console.log(foo["[object Object]"]); // World
```

따라서 Typescript의 Index Signature는 반드시 string 혹은 number여야 한다.

## Index Signature 선언

Index Signature를 명시적으로 지정할 수 있다.

```javascript
let foo: { [index: string]: { message: string } } = {};

/**
 * 정의된 구조에 맞는 것들만 저장
 */

// Ok
foo["a"] = { message: "some message" };

// Error: 타입이 string인 `message`가 있어야 함. `message` 부분에 오타 존재
foo["a"] = { messages: "some message" };

/**
 * 내용을 읽을 때도 타입 검사가 이루어짐
 */

// Ok
foo["a"].message;

// Error: messages는 존재하지 않음. `message` 부분에 오타 존재
foo["a"].messages;
```

> `{ [index: string]: { message: string } }`에서 index는 아무 의미 없이 가독성을 위해 넣는 코드이다. > `{ [username: string]: { message: string } }`으로 사용해도 아무 문제 없다.

## 문자열 리터럴 집합 사용

타입 매핑(Mapped Type)을 사용하여 Index Signature의 Index 문자열이 유니온의 구성원이 되게끔 지정할 수 있다.

```javascript
type Index = 'a' | 'b' | 'c'
type FromIndex = { [k in Index]?: number }

// OK
const good: FromIndex = { b:1, c:2 }

// Error:
// 타입 '{ b: number; c: number; d: number; }'은 타입 'FromIndex'에 할당 불가능.
// 객체 리터럴은 알려진 속성만 지정할 수 있고 'd'는 'FromIndex' 타입에 존재하지 않음.
const bad: FromIndex = { b:1, c:2, d:3 };
```

## Index로 string, number 둘 다 사용

일반적은 사용법은 아니지만 Typescript에서는 Index로 string, number 둘 다 사용하는 것도 가능하다. 하지만 string Index가 number Index보다 더 구체적이어야 한다는 제약이 있다.

```javascript
interface ArrStr {
  [key: string]: string | number; // string Index는 더 구체적(string | number)

  [index: number]: string; // number Index는 더 제한적(string)

  // 그냥 예제 멤버
  length: number;
}
```

## 디자인 패턴: 중첩 Index Signature

매우 빈번하게 JS 커뮤니티에서 문자열 인덱서를 남용하는 API들을 볼 수 있다. 예를 들어, JS 라이브러리에서 CSS를 다루는 흔한 패턴이다.

```javascript
interface NestedCSS {
  color?: string;
  [selector: string]: string | NestedCSS | undefined;
}

const example: NestedCSS = {
  color: "red",
  ".subclass": {
    color: "blue",
  },
};
```

이런 식으로 문자열 인덱서와 유효한 값을 섞어서 쓰면 오타가 발생해도 검출이 되지 않는다.

```javascript
const failsSilently: NestedCSS = {
  colour: "red", // `colour`는 유효한 문자열 인덱서이므로 오류 아님
};
```

대신 중첩된 내용을 nest(아니면 children 아니면 subnodes 등)같은 별도 이름 속성으로 분리하는 것이 좋다.

```javascript
interface NestedCSS {
  color?: string;
  nest?: {
    [selector: string]: NestedCSS,
  };
}

const example: NestedCSS = {
  color: "red",
  nest: {
    ".subclass": {
      color: "blue",
    },
  },
};

const failsSilently: NestedCSS = {
  colour: "red", // TS 오류: 정의되지 않은 속성 `colour`
};
```

## Index Signature에서 특정 속성 제외시키기

때로는 여러 속성을 한 인덱스 서명으로 합쳐야 할 수 있다.

```javascript
type FieldState = {
  value: string,
};

type FormState = {
  isValid: boolean, // 오류: 인덱스 서명을 준수하지 않음
};
```

교차 타입으로 문제를 해결할 수 있다.

```javascript
type FieldState = {
  value: string,
};

type FormState = { isValid: boolean } & { [fieldName: string]: FieldState };
```

이렇게 해서 기존 JavaScript 모델을 선언할 수는 있지만 이런 객체를 TypeScript로 생성할 수는 없다.

```javascript
type FieldState = {
  value: string
}

type FormState =
  { isValid: boolean }
  & { [fieldName: string]: FieldState }


// 다른데서 넘어오는 JavaScript 객체 용으로 사용
declare const foo:FormState;

const isValidBool = foo.isValid;
const somethingFieldState = foo['something'];

// 이것으로 TypeScript 객체를 생성하는 것은 안됨
const bar: FormState = { // 오류 `isValid`는 `FieldState`에 할당할 수 없음
  isValid: false
}
```

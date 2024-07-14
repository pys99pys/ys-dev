## unknown

- unknown 은 타입스크립트의 Top-Type
- 타입스크립트에 존재하는 모든 타입을 할당 할 수 있음
- 따라서 모든 타입의 공통적인 연산밖에 할 수 없음

```
let foo: unknown = 'bar';

foo = 10; // ok
foo = ['hello', 'world']; // ok

// 공통된 연산 외에는 할 수 없다. 

foo[0]; // Error 
foo(); // Error 
foo.bar // Error 

// 타입이 지정된 변수에 할당 할 수 없다. 

let bar: boolean = foo; // Error !! 
// foo 변수의 타입이 unknown 이기 때문에 boolean 타입의 변수에 할당 할 수 없다.

// 할당하기 위해서는 아래와 같이 타입을 명시해줘야 한다.
let bar: boolean = (foo as boolean);
```

## never

- 모든 타입의 하위 타입
- 따라서 그 어떤 값도 Never 타입에 할당 할 수 없음

```
let foo : never = 'bar'; // Error
let bar : never = 10; // Error 
```

### 사용처

함수가 아무것도 반환하지 않을 때 -> never 를 반환타입으로 지정하여 타입추론 예외를 제거

```
function throwError(errorMsg: string): never { 
  throw new Error(errorMsg); 
} 
```

### 특정 타입 값을 할당받지 못하게 할 때

```
type NonString<T> = T extends string ? never : T;
```

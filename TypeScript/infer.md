# infer

조건부 타입(Conditional Types) 문법에서 사용되는 키워드로, 타입 추론(type inference)을 가능하게 해주는 문법

## 기본 문법

```
T extends SomeType<infer U> ? U : DefaultType
```

- `T`가 `SomeType<infer U>`에 할당될 수 있으면 `U` 타입을 추론해서 사용
- 그렇지 않으면 `DefaultType`을 사용

## 예제

### 예제 1: 배열 요소 타입 추출

```
type ElementType<T> = T extends (infer U)[] ? U : never;

type A = ElementType<string[]>; // string
type B = ElementType<number[]>; // number
type C = ElementType<boolean>;  // never
```

- `infer U`를 사용해서 배열 안에 어떤 타입이 있는지 추출

## 예제 2: 함수의 리턴 타입 추출

```
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : never;

type Func = () => number;
type R = ReturnType<Func>; // number
```

- `infer R`로 함수의 리턴 타입을 추론

## 용도

- 타입 추론: 특정 타입 구조 안에서 부분 타입을 추출
- 조건부 타입과 함께 사용: extends 구문에서 infer 사용 가능

## 추가 대안

- typeof와 keyof, indexed access types로 직접 타입 탐색
- utility types(예: ReturnType, Parameters, Awaited 등) 사용

컨디셔널 타입에서 타입스크립트의 추론에 맡기고 싶을 때 사용

반드시 컨디셔널 타입의 참 부분에 들어가야 함

## 기본 사용법

```
type Element<T>=T extends (infer U)[] ? U : T; // success
type Element<T>=T extends (infer U)[] ? T : U; // error

// 배열 요소 타입 얻기
type Elem<T>=T extends (infer U)[] ? U : T;
 
type A=Elem<string[]>; // string
 
// 함수 파라미터 타입 얻기
type Param<T>=T extends (...args: infer P) => any ? P : never;
 
type B=Param<(a: string, b: number) => void>; // [string, number]

// 여러개의 infer 사용
type ParamAndReturn<T>=T extends (...args: infer P) => infer R ? [P, R] : never;
```

## 예시

리액트 컴포넌트 타입 추론(> TS 4.1.0)

```
type InferProps<T> = T extends React.ComponentType<infer P> ? P : never;

type MyProps = InferProps<typeof LibComponent>;
```

재귀적 타입 추론

```
// 배열 T를 flat한 배열의 타입을 나타낸다
type Flatten<T extends readonly unknown[]> = T extends unknown[] ? _Flatten<T>[] : readonly _Flatten<T>[];
// T 타입을 flat 하기 위한 보조 타입. T가 배열이 아니라면 T를 리턴하고 배열이면 배열의 요소를 리턴한다.
// 즉 배열의 요소들을 모두 평탄화해 유니언한 타입을 리턴한다.
type _Flatten<T> = T extends readonly (infer U)[] ? _Flatten<U> : T;
 
// T를 평탄화한 배열의 타입 Flatten<T> 타입을 리턴한다
function flatRecurisve<T extends readonly unknown[]>(xs: T): Flatten<T> {
  const result: unknown[] = [];
 
  function flattenArray(arr: readonly unknown[]) {
    for (const item of arr) {
      if (Array.isArray(item)) {
        flattenArray(item);
      } else {
        result.push(item);
      }
    }
  }
 
  flattenArray(xs);
 
  return result as Flatten<T>;
}
 
const t1 = flatRecurisve(['apple', ['orange', 100], [[4, [true]]]] as const);
```

Promise return 타입

```
type PromiseReturnType<T> = T extends Promise<infer Return> ? Return : T
 
type t = PromiseReturnType<Promise<string>> // string 
```

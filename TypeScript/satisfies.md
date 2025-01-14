# satisfies

TypeScript 4.9에 도입된 기능, 타입 검증을 실행할 때 더 구체적인 제약을 설정하고 코드에서 타입 안전성을 강화하는 데 사용됨

## 요약

- 객체 리터럴이 특정 타입 조건을 충족하는지 검증하지만, 변수의 타입 자체를 제한하지 않음
- 기존의 타입 단언(as)과 달리 런타임 시 발생할 수 있는 오류를 줄여줌
- 주로 객체가 특정 타입을 만족하면서도 더 많은 속성을 가질 수 있는 경우에 유용함

## 사용법

```
const variable = {
  key1: "value1",
  key2: 123,
} satisfies MyType;
```

## 예제

### 타입 검증의 강화를 위한 경우

```
type User = {
  name: string;
  age: number;
};

const user = {
  name: "Alice",
  age: 25,
} satisfies User; // OK! User 타입을 정확히 만족

const invalidUser = {
  name: "Bob",
} satisfies User; // 오류 발생! `age` 속성이 누락됨
```

### 문제 해결

### 문제

```
type Colors = "red" | "green" | "blue";
type RGB = [red: number, green: number, blue: number];

const palette1: Record<Colors, string | RGB> = {
  red: [255, 0, 0],
  green: "#00ff00",
  blue: [0, 0, 255],
};

palette1.red.map(0); // ❌ Error(ts2339): 타입이 배열로 확정되지 않음. (string 가능성)
palette1.green.toUpperCase(); // ❌ Error(ts2339): 타입이 string으로 확정되지 않음 (배열 가능성)
```

- 타이핑에 따르면 모든 key의 값은 튜플 | string 타입
- 따라서 해당 값에서 배열이나 string 메소드를 쓰려면 타입을 좁혀야 함

### 해결

```
const palette2 = {
  red: [255, 0, 0],
  green: "#00ff00",
  blue: [0, 0, 255],
} satisfies Record<Colors, string | RGB>;

palette2.green.toUpperCase(); // ✅ OK: green은 string 타입으로 다운캐스팅 됐으므로 가능.
palette2.red = "#00ff00"; // ❌ Error(ts2322): red은 [number, number, number] 타입으로 다운캐스팅돼서 불가능.
```

- satisfies는 명시한 타입을 만족할 경우 자동으로 다운 캐스팅
- red는 이미 튜플 타입으로 좁혀졌기 때문에 string 재할당이 불가능

## satisfies vs as

as와 satisfies는 비슷해 보이지만 동작은 다름

### as

- 강제로 타입을 지정, 타입 강제 단언으로 런타임 오류 위험 증가
- 타입 검증을 무시

```
const value = "text" as number; // 컴파일러는 이를 허용하지만, 잘못된 단언.
```

## satisfies

- 타입 조건을 만족해야 하며, 강제 단언 없이 타입 안정성 확보

```
const value = {
  name: "Alice",
  age: 25,
} satisfies { name: string; age: number };

// 오류: 타입 조건을 만족하지 않으면 컴파일 실패.
```

## 장점

- 타입 안전성 강화
  - 불필요한 속성을 허용하면서도 타입 조건을 만족하는지 검사 가능
- 가독성 향상
  - 특정 타입 조건을 명확히 하여 코드 이해가 쉬워짐
- 오류 방지
  - as처럼 강제로 단언하지 않고, 타입 조건을 컴파일 시 확실히 검증

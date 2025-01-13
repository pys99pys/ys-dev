## unknown

### 특징

- 가장 넓은 범위를 가지는 타입(unknown은 모든 타입의 슈퍼 타입)
- 모든 값이 할당 가능하지만 unknown으로 선언된 값을 사용할 때는 타입 검증이 필요함

### 예시

```
let value: unknown;

// 어떤 값이든 할당 가능
value = 42;
value = "hello";
value = { key: "value" };

// 사용하려면 타입 검증이 필요
if (typeof value === "string") {
  console.log(value.toUpperCase()); // "HELLO"
}

### 정리
- 안전한 타입으로 타입을 좁히기 전까지는 사용 불가
- 런타임에서 타입이 결정되는 상황에 적합
```

## never

### 특징

- 가장 좁은 범위를 가지는 타입(never는 모든 타입의 서브 타입)
- 절대 값이 존재하지 않는 타입으로,절대 실행되지 않거나 반환되지 않는 코드를 표현할 때 사용

### 예시

**절대 반환되지 않는 함수**

```
function throwError(message: string): never {
  throw new Error(message);
}
```

**끝없는 루프**

```
function infiniteLoop(): never {
  while (true) {}
}
```

**타입 가드에서 불가능한 상태**

```
type Shape = "circle" | "square";

function getArea(shape: Shape) {
  if (shape === "circle") {
    return Math.PI * 2;
  } else if (shape === "square") {
    return 4;
  }

  // shape가 "circle" 또는 "square"가 아니면 이 코드는 실행되지 않음
  const _exhaustiveCheck: never = shape; 
}
```

### 정리

- 실행되지 않는 코드 경로나 반환하지 않는 함수에서 사용
- 타입 체크에서 논리적으로 불가능한 상태를 명시하는 데 유용

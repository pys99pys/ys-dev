# parseInt vs Number

## parseInt

### 특징

- 문자열에서 숫자를 앞부분만 추출해서 정수로 변환
- 기본 10진수로 동작하지만, 원하는 진수를 지정할 수 있음
- 문자열의 앞부분이 숫자가 아닐 경우 NaN 반환

### 예시

```
console.log(parseInt("42"));        // 42
console.log(parseInt("42px"));      // 42 (앞부분만 변환)
console.log(parseInt("abc42"));     // NaN (앞부분이 숫자가 아님)

console.log(parseInt("1010", 2));   // 10 (2진수로 해석)
console.log(parseInt("FF", 16));    // 255 (16진수로 해석)
```

### 주의

- 공백은 무시되지만 문자열이 숫자로 시작하지 않으면 NaN이 반환됨
- 소수점(.)이 있는 경우 정수 부분만 변환됨

## Number

### 특징

- 문자열 전체를 실수 또는 정수로 변환
- 변환할 문자열이 유효하지 않으면 NaN을 반환
- 진수 지정 기능은 없음

### 예시

```
console.log(Number("42"));          // 42
console.log(Number("3.14"));        // 3.14
console.log(Number("42px"));        // NaN (전체가 숫자가 아님)
console.log(Number("abc42"));       // NaN (전체가 숫자가 아님)

console.log(Number("   42  "));     // 42 (공백 무시)
```

## 사용 예제

### parseInt

- 정수 변환이 필요한 경우
- 특정 진수(2진수, 16진수 등)를 처리해야 할 때

### Number

- 실수 변환이 필요한 경우
- 전체 문자열이 숫자 형태인지 확인하고 변환해야 할 때

# 자바스크립트의 숫자 데이터

JavaScript에서 숫자 데이터 처리는 다른 언어와 비교했을 때 몇 가지 독특한 특징이 있음, 특히 JavaScript는 기본적으로 단일 숫자 타입(number)만 제공하며 IEEE 754 표준을 따르는 부동소수점 숫자를 사용한다는 점에서 차별화됨

## 1. 숫자 타입의 단일성

- JavaScript: 숫자는 모두 number 타입으로 처리됨
  - 정수와 부동소수점 모두 같은 타입(number)에 포함
  - ES6 이후, 정수 전용 타입인 BigInt가 추가됨
- 다른 언어: 정수와 실수를 구분하여 다양한 숫자 타입 제공
  - 예: int, float, double, long 등 (C, Java, Python 등)
 
```
console.log(typeof 42);       // "number"
console.log(typeof 3.14);     // "number"
console.log(typeof 9007199254740991n); // "bigint" (ES6+)
```

## 2. 부동소수점 연산

- JavaScript: 64비트 부동소수점 숫자(IEEE 754)로 표현되기 때문에 정밀도 문제가 발생할 수 있음
  - 부동소수점 연산 문제 해결을 위해 toFixed() 또는 Math 라이브러리 사용
- 다른 언어:
  -  Python: decimal 모듈을 이용해 정밀한 연산 가능
  -  Java: BigDecimal을 사용해 정밀도를 유지

```
console.log(0.1 + 0.2); // 0.30000000000000004
```

## 3. 암묵적 변환

- JavaScript: 숫자와 문자열 간에 암묵적 변환을 수행할 수 있음
- 다른 언어: 대부분의 언어는 명시적 타입 변환이 필요함
  - 예: Python에서는 int("5") + 3이 필요
 
```
console.log("5" - 3);   // 2 (문자열이 숫자로 변환됨)
console.log("5" + 3);   // "53" (문자열 결합으로 처리)
```

## 4. 안전하지 않은 정수 범위

- JavaScript: number 타입은 정밀한 정수를 표현할 수 있는 범위가 제한됨
  - 안전 정수 범위: -(2^53 - 1) ~ 2^53 - 1 (약 ±9천조)
  - 이를 넘어서는 값은 정확히 표현할 수 없음
- 다른 언어:
  - Python: 정수 크기에 제한 없음
  - Java: long으로 큰 정수 표현 가능, 더 큰 수는 BigInteger 사용
 
```
console.log(9007199254740991 + 1); // 9007199254740992 (정확)
console.log(9007199254740991 + 2); // 9007199254740992 (오류 발생)

// ES6에서 BigInt 타입이 도입되어 큰 정수를 안전하게 처리 가능
const bigNumber = 9007199254740991n + 2n;
console.log(bigNumber); // 9007199254740993n
```

## 5. NaN(Not-a-Number)

- JavaScript: 숫자 연산이 실패하면 NaN을 반환
  - NaN은 특이하게도 자기 자신과 같지 않음
- 다른 언어:
  - Python: float('nan')을 통해 비슷한 값을 표현
  - Java: Double.NaN 사용

```
console.log(NaN === NaN); // false
console.log(isNaN(NaN));  // true
```

## 6. Infinity

- JavaScript: 무한대를 나타내는 Infinity와 -Infinity를 지원
  - 숫자가 너무 크거나 0으로 나누는 경우 발생
- 다른 언어: 대부분의 언어에서 무한대를 지원하지만, 명시적 예외 처리를 요구하는 경우도 있음

```
console.log(1 / 0);        // Infinity
console.log(-1 / 0);       // -Infinity
console.log(Infinity > 1); // true
```

## 7. 동적 타입 시스템

- JavaScript: 동적 타입 언어로 변수의 타입이 런타임에 결정됨
- 다른 언어: Java, C++: 정적 타입 언어로 컴파일 타임에 타입이 결정됨

```
let x = 42;    // x는 number
x = "hello";   // x는 string
```

## 8. 내장 Math 객체

- JavaScript: Math 객체를 통해 다양한 수학 연산과 상수를 제공
  - 대표적인 메서드: Math.abs(), Math.sqrt(), Math.pow(), Math.random().
  - 상수: Math.PI, Math.E
- 다른 언어: 대부분의 언어에서 비슷한 기능의 수학 라이브러리를 제공

```
console.log(Math.PI);          // 3.141592653589793
console.log(Math.sqrt(16));    // 4
console.log(Math.random());    // 0 ~ 1 사이의 난수
```

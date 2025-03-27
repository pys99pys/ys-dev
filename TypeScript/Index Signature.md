# Index Signature

객체에서 정해지지 않은 동적 키를 정의하고 싶을 때 사용하는 기능

어떤 키가 올지 모르지만 모든 키의 타입과 값의 타입을 명확히 지정하고 싶을 때 사용

## 예시

**기본**

```
{
  [key: string]: valueType;
}
```

- key: 객체의 속성 이름(string 또는 number만 가능)
- valueType: 해당 키에 대응하는 값의 타입

**문자열 키, 숫자 값**

```
type ScoreMap = {
  [studentName: string]: number;
};

const scores: ScoreMap = {
  Sam: 95,
  Jack: 100,
  Brown: 88
};
```

**숫자 키, 문자열 값**

```
type NumMap = {
  [id: number]: string;
};

const arrLike: NumMap = {
  0: 'zero',
  1: 'one'
};
```

- number 인덱스를 지정하면 string 인덱스도 암묵적으로 허용됨, JavaScript에서 객체 키는 결국 string이기 때문

## Index Signature vs Record

## 🧩 Record vs Index Signature 핵심 비교

| 항목               | `Record<K, V>`                              | Index Signature (`{ [key: string]: V }`)     |
|--------------------|----------------------------------------------|----------------------------------------------|
| 키 제한 가능 여부   | ✅ 가능 (`K`를 유니온 타입으로 지정 가능)     | ❌ 불가능 (모든 string 또는 number 허용)     |
| 키 타입 지정        | 명확한 키 집합 (`'a' | 'b'`)                | 넓은 범위의 키 (`string`, `number`)          |
| 오타 방지          | ✅ 키 오타 시 컴파일 에러 발생               | ❌ 오타 입력해도 정상 동작                   |
| 타입 안전성        | 높음 (정적 구조)                            | 낮음 (동적 구조)                             |
| 주요 사용처        | 정해진 키의 객체 (예: i18n, 설정값)          | 동적 키 객체 (예: 서버 응답, 캐시 맵 등)     |
| 타입 유추          | 구체적으로 유추 가능                         | 일반적으로 느슨함                            |

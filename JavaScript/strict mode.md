# strict mode

"use strict" 지시어를 써서 자바스크립트 코드의 실행을 더 엄격한 규칙 아래에서 수행하게 만드는 모드

## 예시

```
"use strict"; // 이 줄이 핵심!

x = 10; // ❌ ReferenceError: x is not defined
```

- 일반 모드에서는 그냥 x가 전역 변수로 만들어지는데, strict 모드에서는 명시적 선언 없으면 에러 발생

## 사용법

### 전체 스크립트에 적용

```
"use strict";

function test() {
  // strict 모드 적용됨
}
```

### 함수 단위로 적용

```
function strictFunction() {
  "use strict";
  // 여기만 strict
}
```

### 모듈

모듈(type="module")은 자동으로 strict 모드 적용됨

## 달라지는 점

| 특징 | 설명 |
|------|------|
| 전역 변수 선언 없이 사용 불가 | `x = 1` → ReferenceError |
| 중복 파라미터 금지 | `function (x, x) {}` → SyntaxError |
| this 바인딩 안전 | 일반 함수 내 `this`는 undefined |
| 안전한 eval | `eval`로 만든 변수는 외부에 안 보임 |
| 에러 조기 발생 | 조용히 무시되던 문제를 강제 에러로 |

## 사용 이유

- 무분별한 전역 변수 생성 방지
- this 바인딩 혼란 방지
- 버그 조기 발견
- 코드 최적화에 도움

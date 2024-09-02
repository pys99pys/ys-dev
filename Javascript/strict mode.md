자바스크립트를 엄격하게 사용하기 위해 ES5에 추가된 문법

## 선언

### 문서 전체에서 선언

```
"use strict"

var x = 'someone';
```

### 함수내에서 선언

```
function fn() {
  "use strict"
}
```

### 모듈에 적용

모듈은 별도 선언 없이 자동으로 strict mode 적용

## strict mode 적용시 변화

실수로 글로벌 변수를 생성하는 것을 방지
```
"use strict";

x = 17; // error
```

잘못된 할당 방지
```
// 쓸 수 없는 프로퍼티에 할당
var undefined = 5; // TypeError
var Infinity = 5; // TypeError

// 쓸 수 없는 프로퍼티에 할당
var obj1 = {};
Object.defineProperty(obj1, "x", { value: 999, writable: false });
obj1.x = 99; // TypeError

// getter-only 프로퍼티에 할당
var obj2 = {
  get x() {
    return 999;
  },
};
obj2.x = 99; // TypeError

// 확장 불가 객체에 새 프로퍼티 할당
var fixed = {};
Object.preventExtensions(fixed);
fixed.newProp = "ohai"; // TypeError
```

삭제할 수 없는 프로퍼티 삭제 방지
```
"use strict";

delete Object.prototype; // TypeError
```

함수 파라미터 변수명 중복 방지
```
function sum(a, a, c) {
  "use strict";
  // error
}
```

8진 구문을 금지(앞에 0)
```
"use strict";
var sum =
  015 + // error
  197 +
  142;
```

primitive 값에 프로퍼티 생성 금지
```
"use strict";

false.true = ""; // TypeError
(14).sailing = "home"; // TypeError
"with".you = "far away"; // TypeError
```

with문 사용 금지, eval 사용 제한

일반 변수 삭제 금지
```
var x;
delete x; // error
```

일반 함수내에서 this가 window를 참조하지 않음

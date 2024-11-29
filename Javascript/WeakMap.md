# 특징

- key는 반드시 객체여야 함
  - string, number 등 타입을 key로 사용할 수 없음
- 키와 값의 약한 참조
  - 가비지 컬렉터가 객체를 메모리에서 정리할 때, WeakMap에 의해 참조되고 있는 키/값 쌍이 있어도 삭제 대상이 될 수 있음
  - 장점: 메모리 누수 방지
- 열거 불가능
  - 약한 참조의 특성 때문에, 내부에 저장된 객체가 언제 사라질지 알 수 없기 때문
  - 제공되는 메서드만 사용해서 접근 가능.
 
# 사용법

## 지원되는 메서드

- set(key, value): 키와 값을 추가
- get(key): 키에 해당하는 값을 반환
- delete(key): 키/값 쌍을 제거
- has(key): 키가 존재하는지 확인

## 예제

```
// WeakMap 생성
const weakMap = new WeakMap();

let obj1 = { name: "Alice" };
let obj2 = { name: "Bob" };

// WeakMap에 객체를 키로 추가
weakMap.set(obj1, "Data for Alice");
weakMap.set(obj2, "Data for Bob");

console.log(weakMap.get(obj1)); // "Data for Alice"
console.log(weakMap.has(obj2)); // true

// 객체 참조를 제거
obj1 = null; // obj1이 가비지 컬렉션 대상이 됨

// obj1은 이제 WeakMap에서 자동으로 제거됨 (명시적으로 확인은 불가능)
```

# Map과 WeakMap의 차이

| **특징**              | **Map**                               | **WeakMap**                              |
|-----------------------|---------------------------------------|-----------------------------------------|
| **키**               | 모든 값 사용 가능                      | 반드시 객체만 키로 사용 가능              |
| **참조 방식**         | 강한 참조                              | 약한 참조                                |
| **가비지 컬렉션 영향** | 키가 참조되고 있는 한 값이 유지됨       | 키가 가비지 컬렉션 대상이 되면 값도 삭제됨 |
| **열거 가능 여부**     | `keys()`, `values()`, `entries()` 지원 | 열거 불가능 

# 사용 사례

## 1. DOM 요소와 관련된 데이터 저장

DOM 요소를 키로 사용해 관련 데이터를 저장하면서, DOM 요소가 제거되면 자동으로 데이터도 정리

```
const elementData = new WeakMap();

const element = document.querySelector("#myElement");
elementData.set(element, { clicked: false });

// 이벤트 처리
element.addEventListener("click", () => {
  const data = elementData.get(element);
  data.clicked = true;
  console.log(data);
});

// DOM 요소 제거
element.remove(); // element가 메모리에서 정리되면 WeakMap 항목도 자동 삭제
```

## 2. 메모리 누수 방지

객체와 관련된 데이터를 저장하되, 객체가 더 이상 필요 없을 때 메모리 정리를 자동으로 수행하도록 설정.

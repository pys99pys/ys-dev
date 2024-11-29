# 강함 참조(Strong Reference)

## 정의

- 객체를 참조할 때, 기본적으로 사용하는 참조 방식.
- 강한 참조가 있는 한 객체는 가비지 컬렉션의 대상이 되지 않음.
- JavaScript에서 변수를 통해 생성된 객체나 데이터는 기본적으로 강한 참조를 사용.

## 특징

- 객체가 메모리에 남아 있음.
- 강한 참조가 제거되지 않으면 메모리 누수가 발생할 수 있음.

## 예제

```
let obj = { name: "Alice" }; // obj는 강한 참조
console.log(obj.name); // "Alice"

// obj가 메모리를 계속 점유
obj = null; // 강한 참조가 제거됨 -> 객체는 가비지 컬렉션의 대상이 됨
```

# 약한 참조(Weak Reference)

## 정의

- 객체를 참조하지만, 가비지 컬렉션 대상이 되는 것을 막지 않는 참조 방식.
- WeakMap, WeakSet 같은 구조에서 주로 사용됨.

## 특징
- 객체가 더 이상 다른 강한 참조에 의해 참조되지 않을 경우, 자동으로 메모리에서 제거됨.
- 가비지 컬렉션이 일어나면 약한 참조도 함께 사라짐.

## 예제

```
let weakMap = new WeakMap();
let obj = { name: "Alice" }; // 강한 참조

// WeakMap에 객체를 추가 (약한 참조)
weakMap.set(obj, "Data for Alice");

// 강한 참조 제거
obj = null; // 객체는 더 이상 강하게 참조되지 않음 -> 가비지 컬렉션으로 제거됨
// weakMap도 자동으로 해당 키를 제거
```

# 차이점

## 강한 참조

- GC의 대상이 되기 전까지 객체는 반드시 "명시적"으로 참조를 제거해야 메모리에서 해제될 수 있음
- 예를 들어, 강한 참조로 객체를 Map에 추가하면, 객체가 가비지 컬렉션의 대상이 되지 않고 계속 메모리에 남아 있음.

```
let map = new Map();
let obj = { name: "Alice" };

// 강한 참조로 추가
map.set(obj, "Data");

// obj = null로 참조를 끊어도 map은 obj를 강하게 참조 중
obj = null;
console.log(map.has(obj)); // false (obj는 직접 참조하지 않지만 내부적으로 여전히 유지됨)

// 객체는 GC 대상이 되지 않음
console.log([...map.keys()]); // [{ name: "Alice" }]

// 결과: Map이 obj를 강하게 참조하므로, obj는 메모리에서 제거되지 않음.
```

## 약한 참조

- WeakMap은 객체를 약하게 참조하기 때문에, 객체가 더 이상 강하게 참조되지 않으면 자동으로 메모리에서 제거됨.
- WeakMap 내부에 남아 있던 데이터도 함께 삭제됨.

```
let weakMap = new WeakMap();
let obj = { name: "Alice" };

// 약한 참조로 추가
weakMap.set(obj, "Data");

// obj = null로 참조를 끊으면 GC 대상이 됨
obj = null;
// WeakMap 내부 데이터도 사라짐
console.log(weakMap.has(obj)); // false

// 결과: WeakMap은 객체에 대한 약한 참조만 가지고 있으므로, 객체가 GC 대상이 되어 제거됨.
```

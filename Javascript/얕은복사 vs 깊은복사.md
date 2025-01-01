얕은 복사(Shallow Copy)**와 **깊은 복사(Deep Copy)**는 객체를 복사하는 방식에 대한 개념

## 얕은 복사(Shallow Copy)

객체의 최상위 속성만 복사하고 객체 내부의 참조가 여전히 원본 객체를 가리키는 방식

즉, 객체의 속성이 다른 객체를 참조하는 경우 복사된 객체는 여전히 원본 객체의 속성값을 참조하게 됨

### 특징

- 복사된 객체는 원본 객체와 동일한 참조를 공유
- 객체 내부의 중첩된 값은 복사되지 않고 참조만 복사
- 원본 객체나 복사된 객체의 속성이 변경되면 다른 객체에도 영향을 미칠 수 있음

### 예시

```
const original = { name: 'Alice', age: 25, address: { city: 'Seoul' } };

// 얕은 복사: Object.assign() 사용
const shallowCopy = Object.assign({}, original);

shallowCopy.name = 'Bob';
shallowCopy.address.city = 'Busan'; // 원본 객체와 공유된 참조가 변경됨

console.log(original.name); // 'Alice' (변경되지 않음)
console.log(original.address.city); // 'Busan' (변경됨, 주소 변경됨)

console.log(shallowCopy.name); // 'Bob' (이름만 변경됨)
console.log(shallowCopy.address.city); // 'Busan' (주소 변경됨)
```

### 얕은 복사 메서드

- Object.assign()
- 스프레드 연산자 ({ ...obj })

## 깊은 복사 (Deep Copy)

객체의 모든 속성을 재귀적으로 복사하여 새로운 객체를 생성하는 방식

이 방식은 객체 내부의 참조 값까지 모두 새로운 값으로 복사하여 원본 객체와 복사된 객체가 완전히 독립적인 상태가 됨

### 특징

- 객체 내부의 모든 속성이 새로운 메모리 공간에 복사
- 원본 객체와 복사된 객체가 독립적, 따라서 한 객체를 변경해도 다른 객체에 영향을 주지 않음
- 성능 측면에서 비효율적일 수 있음

### 예시

```
const original = { name: 'Alice', age: 25, address: { city: 'Seoul' } };

// 깊은 복사: JSON 방법 사용
const deepCopy = JSON.parse(JSON.stringify(original));

deepCopy.name = 'Bob';
deepCopy.address.city = 'Busan'; // 원본 객체와 독립적으로 복사됨

console.log(original.name); // 'Alice' (변경되지 않음)
console.log(original.address.city); // 'Seoul' (변경되지 않음)

console.log(deepCopy.name); // 'Bob' (이름만 변경됨)
console.log(deepCopy.address.city); // 'Busan' (주소 변경됨)
```

## 깊은 복사 방법

- JSON.parse(JSON.stringify(obj))
- 재귀적 복사 함수 작성
- 라이브러리 사용 (예: lodash.cloneDeep)

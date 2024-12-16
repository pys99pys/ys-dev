## 유사배열(array-like)

배열처럼 동작할 수 있지만 실제 배열이 아닌 객체

배열과 비슷하게 인덱싱을 통해 요소에 접근할 수 있고, length 속성을 가지지만 배열의 메서드(push, map, forEach 등)를 직접 사용할 수는 없음

## 특징

### 1. 인덱싱을 통한 요소 접근 가능
배열처럼 obj[0], obj[1] 형태로 요소를 읽거나 쓸 수 있음

### 2. length 속성 존재
객체에 몇 개의 요소가 포함되어 있는지를 나타내는 length 속성이 있음

### 3. 배열 메서드 미지원
Array.prototype 메서드(map, filter, reduce 등)를 직접 호출할 수 없음

### 4. 일반 객체와 다른 구조
일반 객체와는 달리 숫자 인덱스를 키로 사용하고 이를 기반으로 동작

## 대표적인 유사 배열

### 1. arguments 객체

```
function example() {
  console.log(arguments[0]); // 첫 번째 인자 출력
  console.log(arguments.length); // 인자의 개수 출력

  // arguments.map(x => x * 2); // 오류! arguments는 배열이 아님
}

example(1, 2, 3);
```

### 2. DOM의 NodeList

```
const divs = document.querySelectorAll("div");

console.log(divs[0]); // 첫 번째 div 요소
console.log(divs.length); // div 요소의 개수

// divs.map(div => div.textContent); // 오류! NodeList는 배열이 아님
```

## 유사 배열을 배열로 변환하는 방법

### 1. Array.from()

```
const divs = document.querySelectorAll("div");
const divArray = Array.from(divs);

console.log(divArray.map(div => div.textContent)); // 배열 메서드 사용 가능
```

### 2. 스프레드 연산자 (...)

```
const divArray = [...document.querySelectorAll("div")];
console.log(divArray.map(div => div.textContent)); // 배열 메서드 사용 가능
```

### 3. Array.prototype.slice

```
function example() {
  const argsArray = Array.prototype.slice.call(arguments);
  console.log(argsArray.map(x => x * 2)); // 배열 메서드 사용 가능
}

example(1, 2, 3);
```

## 유사 배열을 사용하는 이유

- 메모리 효율성을 높이기 위해 사용, 배열 메서드가 없어도 필요한 동작만을 수행할 수 있는 경우 더 가볍게 사용할 수 있음
- DOM API나 함수 인자를 간단히 다루기 위해 설계된 구조이기도 함

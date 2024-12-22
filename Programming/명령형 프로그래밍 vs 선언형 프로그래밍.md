## 명령형 프로그래밍 (Imperative Programming)

### 요약

- 프로그램이 "어떻게(how)" 동작해야 하는지를 명시적으로 지시하는 방식
- 순차적으로 프로그램의 상태를 변경하며, 절차를 중요하게 여김
- 보통 루프, 조건문, 변수 등을 사용해 상태를 관리하고 결과를 만듦
- 전통적인 C, Java, Python 같은 언어에서 자주 사용됨

### 특징

- 상태(state)를 명시적으로 다룸
- 코드 흐름을 세밀하게 제어
- 보통 복잡한 로직이나 알고리즘에 적합

### 예제

```
const numbers = [1, 2, 3, 4, 5];
let sum = 0;

for (let i = 0; i < numbers.length; i++) {
  sum += numbers[i]; // 상태를 명시적으로 변경
}

console.log(sum); // 15
```

## 선언형 프로그래밍 (Declarative Programming)

### 요약

- 무엇을(what) 해야 하는지를 표현하는 방식
- 결과에 초점을 맞추며, "어떻게" 수행될지는 숨겨져 있음
- 코드가 더 간결하고 읽기 쉬운 경우가 많음
- SQL, HTML, 함수형 프로그래밍(JavaScript의 map, filter 등)에서 흔히 사용됨

### 특징

- 상태를 명시적으로 관리하지 않음
- 무엇을 원하는지 표현에 집중
- 복잡한 작업을 추상화해 가독성이 높음

### 예제

```
const numbers = [1, 2, 3, 4, 5];
const sum = numbers.reduce((acc, curr) => acc + curr, 0);

console.log(sum); // 15
```

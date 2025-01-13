## Attribute 

- HTML 문서에 정의된 속성
- 요소의 초기 상태를 나타냄
- HTML에서 태그에 직접 작성하는 속성을 의미
- 예: <input type="text" value="Hello">에서 type과 value는 attributes

## Property

- DOM 객체의 속성
- JavaScript에서 해당 요소를 나타내는 객체의 상태
- Property는 요소의 현재 상태를 나타냄. JavaScript로 변경 가능

## 예제

```
**HTML**

```
<input id="myInput" type="text" value="Hello">
```

**JavaScript**

```
const input = document.getElementById("myInput");

// Attribute 접근
console.log(input.getAttribute("value")); // "Hello"

// Property 접근
console.log(input.value); // "Hello"

// Property를 변경
input.value = "Hi";

// 변경 후 확인
console.log(input.getAttribute("value")); // "Hello" (초기값 유지)
console.log(input.value); // "Hi" (현재 상태)
```

- getAttribute("value")는 HTML에서 정의된 초기 속성 값을 가져옴
- .value는 현재 DOM 요소의 상태를 반영

## 동기화

- 일부 Attribute와 Property는 동기화됨
  - 예: value, checked, src 등
  - HTML에서 속성을 정의하면 Property에 반영되고, 초기 Property 값은 Attribute를 기반으로 설정
- 동기화는 한 방향으로만 이루어짐
  - HTML Attribute -> DOM Property: 초기값 동기화
  - DOM Property → HTML Attribute: 반영되지 않을 수 있음
 
## 동기화 예외

- 일부 속성은 동기화되지 않음
  - class (Attribute) ↔ className (Property): 초기값은 동기화되지만 변경 시 동작 방식이 다를 수 있음
  - style: getAttribute("style")은 스타일 문자열을 반환하지만 style Property는 CSS 스타일 객체를 반환

## 동기화 예시

**HTML**

```
<div id="myDiv" class="test"></div>
```

**JavaScript**

```
const div = document.getElementById("myDiv");

// Attribute 변경
div.setAttribute("class", "new-class");
console.log(div.className); // "new-class"

// Property 변경
div.className = "another-class";
console.log(div.getAttribute("class")); // "another-class"
```

## 사용 예제

### Attribute 사용

- HTML의 초기 속성 값을 확인하거나 변경할 때
- HTML과 관련된 속성을 다룰 때

```
element.getAttribute("attributeName");
element.setAttribute("attributeName", "value");
```

### Property 사용

- DOM의 현재 상태를 확인하거나 변경할 때
- JavaScript로 동적으로 요소를 제어할 때

```
element.propertyName = "value";
```

## 결론

- Attribute: HTML 문서의 초기값(고정적)
- Property: DOM 객체의 동적 상태(변화 가능)

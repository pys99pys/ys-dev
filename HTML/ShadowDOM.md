# ShadowDOM

웹 컴포넌트 기술의 핵심 요소로 DOM의 특정 부분을 독립적으로 관리하고 스타일과 기능을 캡슐화할 수 있는 기술

Shadow DOM을 사용하면 요소 내부의 구현 세부사항이 외부 DOM 트리와 분리되므로 스타일 충돌이나 의도치 않은 변경을 방지할 수 있음

## 주요 특징

### 캡슐화된 DOM 트리

- Shadow DOM은 독립적인 DOM 트리를 생성하며, 외부 DOM과 분리됨
- 내부 스타일과 스크립트는 외부 DOM에 영향을 받지 않으며 외부에도 영향을 주지 않음

### 스타일 격리

- Shadow DOM 내부에서 정의된 스타일은 Shadow DOM 내부 요소에만 적용
- 외부에서 Shadow DOM 내부 요소를 직접 스타일링할 수 없음

### 스코프가 분리된 DOM

- Shadow DOM은 스코프를 제공하여 외부 DOM 트리와 독립적으로 작동

## Shadow DOM의 생성

Shadow DOM은 일반 DOM 요소에 attachShadow() 메서드를 사용하여 생성할 수 있음

```
<div id="host"></div>
<script>
  // 호스트 요소 선택
  const host = document.getElementById("host");

  // Shadow DOM 생성
  const shadowRoot = host.attachShadow({ mode: "open" });

  // Shadow DOM 내부 콘텐츠 추가
  shadowRoot.innerHTML = `
    <style>
      p {
        color: blue;
        font-weight: bold;
      }
    </style>
    <p>이 내용은 Shadow DOM 안에 있습니다.</p>
  `;
</script>
```

## Shadow DOM 모드

### Open Mode

- Shadow DOM은 생성된 Shadow Root에 대해 직접적으로 접근할 수 있음

```
const shadowRoot = host.attachShadow({ mode: "open" });
console.log(host.shadowRoot); // ShadowRoot에 접근 가능
```

### Closed Mode

- Shadow DOM은 외부에서 접근할 수 없음

```
const shadowRoot = host.attachShadow({ mode: "closed" });
console.log(host.shadowRoot); // null
```

## 사용 사례

### 웹 컴포넌트 제작

- 스타일과 기능을 캡슐화하기 때문에 재사용 가능한 웹 컴포넌트 제작에 적합

### 스타일 충돌 방지

- 외부 스타일과의 충돌을 방지하므로, 복잡한 애플리케이션에서 안전하게 사용할 수 있음

### 플러그인 및 위젯 개발

- 독립된 스코프를 제공하여 플러그인이나 위젯이 기존 사이트의 레이아웃이나 스타일에 영향을 주지 않도록 보장함

## Shadow DOM과 Custom Elements

Shadow DOM은 Custom Elements와 함께 사용되며 재사용 가능한 캡슐화된 컴포넌트를 만드는 데 도움 줌

```
// javascript
class MyComponent extends HTMLElement {
  constructor() {
    super();
    const shadow = this.attachShadow({ mode: "open" });
    shadow.innerHTML = `
      <style>
        h1 { color: green; }
      </style>
      <h1>Shadow DOM 컴포넌트</h1>
    `;
  }
}

customElements.define("my-component", MyComponent);

// HTML
<my-component></my-component>
```

## 한계

### SEO

- Shadow DOM 내부 콘텐츠는 기본적으로 검색 엔진이 접근하기 어려울 수 있음

### 디버깅 어려움

- Shadow DOM 내부의 스타일과 DOM은 디버깅 툴에서 별도로 확인해야 함

### 브라우저 지원

- 대부분의 최신 브라우저에서 지원되지만, 구형 브라우저에서는 폴리필이 필요할 수 있음

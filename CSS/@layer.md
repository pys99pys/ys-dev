# @layer

CSS의 레이어(Layer) 우선순위를 제어할 수 있게 해주는 CSS 규칙, 주로 Tailwind CSS 같은 유틸리티 프레임워크나 컴포넌트 기반 스타일 구성에서 자주 사용됨

## 기본 개념

```
@layer base, components, utilities;
```

- @layer를 선언하면 각각의 CSS를 논리적인 그룹으로 나눌 수 있음
- 이 레이어들끼리는 우선순위가 정해짐
  - base < components < utilities
 
## 레이어 선언 방법

```
@layer base {
  h1 {
    font-size: 2rem;
  }
}

@layer components {
  .btn {
    background-color: blue;
  }
}

@layer utilities {
  .mt-4 {
    margin-top: 1rem;
  }
}
```

- utilities 안에 있는 스타일이 다른 스타일보다 우선해서 적용됨

## 필요한 이유

- 전통적인 CSS에서는 선언 순서가 곧 우선순위였음
- @layer는 순서와 상관없이 우선순위를 구조적으로 제어할 수 있음

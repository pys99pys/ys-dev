# script 태그의 defer, async 속성

## 비교

### 기본 script

```
<script src="main.js"></script>
```

- HTML 파싱 중단
- 스크립트 다운로드 + 실행
- 끝나야 HTML 계속 파싱

-> 성능에 좋지 않음

### async

```
<script src="analytics.js" async></script>
```

- HTML 파싱과 동시에 다운로드
- 다운로드 끝나면 즉시 실행
- 파싱 중단됨
- 여러 개면 실행 순서 보장 안 됨

-> 파싱과 실행 순서 꼬일 수 있음

### defer

```
<script src="bundle.js" defer></script>
```

- HTML 파싱과 동시에 다운로드
- 파싱 끝난 후, 순서대로 실행
- 실행은 DOMContentLoaded 직전

-> 모듈 번들, 페이지 로직 스크립트에 가장 안정적

## 사용처

- 메인 앱 번들(JS 로직, DOM 조작 등): defer
- 외부 분석기, 광고, 독립적인 기능: async
- inline script 없이 빠르게 렌더링하고 싶을 때: defer
- 여러 script 간 순서 상관 없을 때: async

## 모듈 스크립트

```
<script type="module" src="app.js"></script>
```

- 기본적으로 defer처럼 동작
- 따로 defer 안 써도 됨
- 하지만 async는 명시적으로 지정 가능

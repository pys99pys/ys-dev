브라우저에서 DOM 생성중 script 태그를 만나면 DOM 생성을 잠시 중단하고 제어권을 렌더링 엔진에서 자바스크립트 엔진으로 넘겨 자바스크립트를 실행함

이 문제는 몇가지 이슈를 발생시킴

1. DOM 생성이 중단되었으므로 script 아래에 있는 DOM에 접근할 수 없음
2. 스크립트가 무거운 경우 다운받고 실행되는동안 렌더링이 되지 않아 흰화면을 보게될 수 있음

## defer

defer 속성이 있는 스크립트는 백그라운드에서 다운됨

따라서 script 다운로드중에도 HTML 파싱을 멈추지 않음

defer 스크립트 실행은 페이지 구성이 끝날때까지 지연됨

```
<p>...스크립트 앞 콘텐츠...</p>

<script>
  document.addEventListener('DOMContentLoaded', () => alert("`defer` 스크립트가 실행된 후, DOM이 준비되었습니다!"));
</script>

<script defer src="https://javascript.info/article/script-async-defer/long.js?speed=1"></script>

<p>...스크립트 뒤 콘텐츠...</p>
```

- 페이지 콘텐츠는 바로 출력
- DOMContentLoaded 이벤트는 지연 스크립트 실행을 기다림
- 따라서 얼럿창은 DOM 트리가 완성되고 지연 스크립트가 실행된 후에 노출

defer 속성은 외부 스크립트에만 유효하며 src 속성이 없는 경우 무시됨

## async

페이지와 완전히 독립적으로 동작

defer 속성과 마찬가지로 백그라운드에서 다운로드 되지만 페이지 구성과 상관 없이 다운로드 완료된 시점에 바로 실행됨

```
<p>...스크립트 앞 콘텐츠...</p>

<script>
  document.addEventListener('DOMContentLoaded', () => alert("DOM이 준비 되었습니다!"));
</script>

<script async src="https://javascript.info/article/script-async-defer/long.js"></script>
<script async src="https://javascript.info/article/script-async-defer/small.js"></script>

<p>...스크립트 뒤 콘텐츠...</p>
```

- 페이지 콘텐츠는 바로 출력
- DOMContentLoaded 이벤트는 스크립트 다운로드 여부와 상관 없이 콘텐츠 출력 완료된 시점에 실행
- small.js는 위치상 long.js 보다 아래지만 먼저 다운로드 될 경우 먼저 실행됨

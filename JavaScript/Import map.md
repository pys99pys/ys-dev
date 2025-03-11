# import map

자바스크립트에서 사용하는 모듈 임포트(import) 방식을 브라우저에서 직접 커스터마이징할 수 있게 해주는 기능

## 주요 기능

- 모듈 경로 별칭 지정: 모듈 경로에 별칭(alias)을 설정해 쉽게 불러오기 가능
- CDN 활용 용이: CDN에서 직접 라이브러리를 불러오는 방식도 쉬워짐
- 번들링 생략: 간단한 프로젝트에선 번들러(Webpack, Vite 등) 없이도 ES모듈을 효과적으로 관리 가능

## 사용 예시

### 기본 문법

```
<script type="importmap">
{
  "imports": {
    "lodash": "https://cdn.jsdelivr.net/npm/lodash-es@4.17.21/lodash.min.js",
    "react": "https://esm.sh/react@18.2.0"
  }
}
</script>

<script type="module">
  import { isEmpty } from "lodash";
  import React from "react";

  console.log(isEmpty({})); // true
  console.log(React.version); // "18.2.0"
</script>
```

- lodash나 react라는 별칭(alias)을 설정해서 URL을 직접 쓰지 않고 모듈 사용

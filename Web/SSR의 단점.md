# SSR의 단점

## 서버 부하 증가

- 모든 요청마다 HTML을 서버에서 렌더링해야 하므로, 트래픽이 많아질수록 서버 리소스 소모가 커짐
- 정적 페이지보다 서버 비용이 높아질 수 있음

### => 해결 방법

**캐싱 전략 도입**

- 페이지 수준 캐싱(예: getServerSideProps + Cache-Control 헤더)
- Reverse Proxy 캐싱(CDN): Cloudflare, Fastly 등을 통해 서버 응답 캐싱

**부분적인 SSR(Hybrid Rendering)**

- 빈번히 바뀌지 않는 부분은 SSG, 자주 바뀌는 부분만 SSR

## 응답 속도 변동

- 서버가 응답을 준비하는 데 시간이 걸려, **TTFB(Time To First Byte)가 늘어날 수 있음
- 특히, 데이터 fetching 시간이 길 경우 사용자가 콘텐츠를 늦게 보게 됨

### => 해결 방법

**데이터 프리패칭 및 캐싱**

- 백엔드 API의 응답을 Redis, Edge cache 등에 캐싱

**스트리밍 SSR(React 18의 pipeToNodeWritable)**

- 일부 HTML부터 빠르게 전송해서 TTFB 단축(점진적 렌더링)

## 복잡한 코드 구조

- 클라이언트와 서버 모두에서 실행되는 코드를 관리해야 하므로 코드가 복잡해짐
- window, document 같은 브라우저 API는 서버에서 사용할 수 없기 때문에 조건 분기가 필요함

### => 해결 방법

**isomorphic(동일한) 유틸리티 패턴 사용**

- 환경 감지 유틸 작성

**Next.js 같은 프레임워크 활용**

- 환경별 코드 분리를 체계적으로 지원
- useEffect는 CSR만 동작 등

## 초기 로딩 이후 느린 인터랙션

- 클라이언트에서 하이드레이션(hydration) 과정이 필요하여, 인터랙티브 요소가 늦게 활성화됨
- 하이드레이션 전까지 버튼 클릭 등의 UI 반응이 작동하지 않을 수 있음

### => 해결 방법

**React 18의 useTransition, Suspense + streaming SSR**

- 비동기 컴포넌트를 우선순위에 따라 나눠 하이드레이션

**부분적 CSR 도입**

- 인터랙션이 많은 컴포넌트는 `dynamic(import, { ssr: false })`로 CSR 처리

## 빌드/배포 환경 복잡도

- SSR을 사용하는 프레임워크(예: Next.js)의 경우, 정적/동적 라우팅 처리나 캐싱 전략 설정이 더 복잡함
- CDN 캐싱이 제한적일 수 있음(서버에서 실시간 HTML을 생성하므로)

### => 해결 방법

**Vercel / Netlify 같은 SSR 지원 플랫폼 사용**

- 자동 배포, 빌드 최적화, SSR endpoint 관리 등을 지원

**서버리스 SSR 도입(예: AWS Lambda + Next.js middleware)**

- 동적 페이지도 자동 확장되도록 구성 가능

## 초기화 문제

클라이언트와 서버의 상태 불일치로 인해 hydration mismatch 오류 발생 가능성 있음

### => 해결 방법

**서버와 클라이언트 상태 동기화 주의**

- useEffect에서만 클라이언트 상태 변경
- Math.random, Date.now() 같은 값은 서버와 클라이언트에서 일치시켜야 함

**SSR-safe 컴포넌트 설계**

- mounted 체크 로직(useHasMounted 훅)으로 클라이언트만 렌더링

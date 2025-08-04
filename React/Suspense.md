# Suspense

비동기 데이터 로딩 상태를 관리하고, 컴포넌트가 렌더링되기 전에 대체 UI를 표시할 수 있게 해주는 React의 내장 컴포넌트

## 특징

- 비동기 UI 상태 관리: 데이터를 가져오거나, 동적으로 컴포넌트를 로드하는 동안 대체 UI를 표시함으로써 사용자가 로딩 상태를 시각적으로 인지할 수 있음
- 로딩 화면 표시: 로딩 중에 표시할 UI를 fallback 속성으로 지정해 사용할 수 있음
- 비동기 데이터와의 통합: 서버 사이드 렌더링(SSR), 클라이언트 사이드 데이터 패칭, use 훅과 함께 비동기 데이터 처리를 간소화

## 동작 원리

**핵심 개념 -> Promise Throwing**

```
function MyComponent() {
  if (!data) {
    throw fetchData(); // 아직 데이터 없음 → Promise를 던짐
  }

  return <div>{data.text}</div>;
}
```

- MyComponent가 렌더링될 때 data가 아직 없으면 fetchData()가 반환하는 Promise를 throw
- React는 이 Promise를 감지하고 렌더링을 중단
- 부모 Suspense에서 지정한 fallback 컴포넌트를 렌더
- Promise가 해결되면 다시 렌더를 시도 -> 이번엔 data가 있음 -> 정상 렌더

## React.lazy와의 조합

```
const MyComponent = React.lazy(() => import('./MyComponent'));

<Suspense fallback={<div>로딩중...</div>}>
  <MyComponent />
</Suspense>
```

- React.lazy는 내부적으로 import()가 반환하는 Promise를 throw
- Suspense는 이걸 잡고 fallback UI를 보여줌

## 사용법

**기본 사용법**

```
import React, { Suspense } from 'react';

const LazyComponent = React.lazy(() => import('./MyComponent'));

function App() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <LazyComponent />
    </Suspense>
  );
}

export default App;
```

- `React.lazy`: 컴포넌트를 동적으로 로드
- `fallback`: 컴포넌트가 로드될 때까지 표시할 로딩 UI

**비동기 데이터 로딩과 함께 사용**

```
import React, { Suspense } from 'react';

// 비동기 데이터 패칭 함수
async function fetchData() {
  const response = await fetch('https://jsonplaceholder.typicode.com/posts/1');
  return response.json();
}

// 비동기 데이터를 Suspense로 처리
function DataComponent() {
  const data = use(fetchData());

  return (
    <div>
      <h1>{data.title}</h1>
      <p>{data.body}</p>
    </div>
  );
}

function App() {
  return (
    <Suspense fallback={<div>Loading data...</div>}>
      <DataComponent />
    </Suspense>
  );
}

export default App;
```

- use(fetchData())를 사용해 데이터를 패칭하며, 데이터 로드가 끝날 때까지 Suspense가 로딩 UI를 표시

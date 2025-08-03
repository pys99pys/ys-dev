# Fiber

Fiber는 React 16부터 도입된 내부 자료구조이자 알고리즘

## 도입 목적

- 기존 React는 동기적(재귀적) 렌더링 방식
- 컴포넌트 트리가 깊거나 복잡할 경우, 이 방식은 브라우저의 메인 스레드를 장시간 점유
- 그 결과 스크롤, 입력, 애니메이션 같은 사용자 인터랙션을 막거나, 큰 앱에서는 렌더링 버벅임이 발생
- React는 이를 해결하기 위해 렌더링을 작업 단위로 쪼개고, 중단 가능한 구조로 전환 -> Fiber

## 핵심 개념

- Fiber Node: 각 React 엘리먼트(컴포넌트)를 나타내는 객체, 트리 형태로 연결됨
- Work Unit: Fiber Node 하나하나가 작업 단위로 처리됨
- Interruptible Rendering: 렌더링 중간에 멈췄다가 이어서 할 수 있음
- Prioritization: 작업마다 우선순위를 정해서 중요한 것부터 처리
- Concurrency: 여러 렌더링 작업을 병렬처럼 다루기 위한 기반, React 18의 Concurrent 기능이 이 위에서 작동함

## Fiber Node 구조

Fiber Node는 각 React 엘리먼트(혹은 컴포넌트)를 표현하는 객체

```
type FiberNode = {
  tag: WorkTag;                     // 어떤 종류의 컴포넌트인지 (함수형, 클래스형 등)
  key: null | string;              // 리스트 렌더링 시 key prop
  elementType: any;                // JSX의 type (ex. 'div', MyComponent)
  type: any;                       // 최종 처리될 타입 (HOC 처리 후 등)
  stateNode: any;                  // 실제 DOM 노드 or 클래스 인스턴스

  // 트리 구조
  return: FiberNode | null;        // 부모 노드
  child: FiberNode | null;         // 첫 번째 자식
  sibling: FiberNode | null;       // 다음 형제
  index: number;                   // 형제 중 위치

  // 더블 버퍼링을 위한 구조
  alternate: FiberNode | null;     // 이전 렌더링의 FiberNode

  // props / state 관련
  pendingProps: any;               // 새로 전달된 props
  memoizedProps: any;              // 렌더링 완료된 props
  memoizedState: any;              // 렌더링 완료된 state
  updateQueue: any;                // 업데이트가 쌓이는 큐

  // side effect 관련
  flags: Flags;                    // 어떤 작업이 필요한지 (ex. Placement, Update)
  subtreeFlags: Flags;            // 자식까지 포함한 effect 정보
  deletions: FiberNode[] | null;  // 삭제될 노드들
};
```

## 렌더링 단계

React는 Fiber 구조를 통해 렌더링을 2단계로 나눠서 처리

### 1. Render Phase (비동기 가능)

- Fiber 트리를 순회하면서 어떤 변경이 필요한지 계산
- performUnitOfWork() 단위로 작업을 쪼갬
- 시간이 부족하면 shouldYield()로 판단해 브라우저에게 제어권을 넘김
- 중단된 지점에서 다시 이어서 실행 가능

### 2. Commit Phase (동기 처리)

- 변경된 내용을 DOM에 실제 반영
- DOM 업데이트, ref 처리, lifecycle 실행
- 이 단계는 중단되지 않음

### Fiber 도입으로 해결된 것

| 문제                        | Fiber 도입 전       | Fiber 도입 후          |
| -------------------------- | ----------------- | --------------------- |
| 긴 렌더링 블로킹               | 전체 트리를 재귀 순회  | 작업을 쪼개서 중단/재개 가능 |
| 우선순위 없음                 | 모든 작업 동일 취급    | 중요한 작업을 먼저 처리     |
| UX 끊김                     | 애니메이션, 입력과 충돌 | 브라우저가 끼어들 수 있음   |
| Suspense / Concurrent Mode | 불가능              | 구현 가능               |

## Concurrent Rendering과의 연결

Fiber는 중단 가능한 구조이지만, 실제로 작동하게 하려면 다음 조건이 필요

### 1. ReactDOM.createRoot() 사용

```
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App />);
```

- 기존 ReactDOM.render()는 동기 방식, 중단 불가
- createRoot()를 써야 React의 Scheduler가 작동

### 2. startTransition()으로 우선순위 낮추기

```
import { startTransition } from 'react';

startTransition(() => {
  setState('검색어 업데이트');
});
```

- 이 안에서 발생하는 렌더링은 낮은 우선순위로 처리됨
- 사용자 입력 같은 높은 우선순위 작업을 먼저 처리할 수 있음


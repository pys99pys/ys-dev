# Prioritized Task Scheduling API

브라우저가 실행할 작업의 **우선순위(priority)**를 지정할 수 있도록 해주는 API, 기존의 setTimeout()이나 requestIdleCallback() 같은 방식보다 더 세밀하게 작업의 중요도를 조정할 수 있음

## 핵심 개념

### scheduler.postTask() 메서드

이 메서드를 사용하면 특정 작업을 브라우저의 **태스크 큐(task queue)**에 추가하면서, 실행될 때의 우선순위를 지정할 수 있음

### 작업 우선순위(Priority)

postTask()를 호출할 때, 다음 중 하나의 우선순위를 설정할 수 있음

- "user-blocking": 사용자 입력과 관련된 가장 중요한 작업(최고 우선순위) -> 버튼 클릭 처리, 키 입력 이벤트
- "user-visible": 사용자가 볼 수 있는 UI 업데이트 관련 작업(기본값) -> DOM 업데이트, 애니메이션
- "background": 백그라운드에서 실행되며, 중요한 작업보다 후순위 -> 로그 전송, 데이터 분석

## 사용법

### 기본적인 postTask() 사용

```
scheduler.postTask(() => {
  console.log("이 작업이 실행됨!");
}, { priority: "user-visible" });
```

### 여러 개의 우선순위 작업 실행하기

```
scheduler.postTask(() => console.log("🟥 user-blocking"), { priority: "user-blocking" });
scheduler.postTask(() => console.log("🟦 user-visible"), { priority: "user-visible" });
scheduler.postTask(() => console.log("🟩 background"), { priority: "background" });
```

## 활용 사례

### 애니메이션 프레임과 함께 사용

```
function renderFrame() {
  scheduler.postTask(() => {
    console.log("🔵 프레임 렌더링");
  }, { priority: "user-visible" });
}

requestAnimationFrame(renderFrame);
```

- 애니메이션을 부드럽게 유지하면서 다른 작업을 백그라운드에서 실행할 수 있음

### 사용자 입력 이벤트 우선 처리

```
document.getElementById("btn").addEventListener("click", () => {
  scheduler.postTask(() => {
    console.log("🚀 버튼 클릭 처리");
  }, { priority: "user-blocking" });

  scheduler.postTask(() => {
    console.log("📊 로그 전송");
  }, { priority: "background" });
});
```

- 버튼 클릭 이벤트는 빠르게 처리하고, 로그 전송은 백그라운드에서 실행하도록 조정 가능

## 주의할 점


- 모든 브라우저에서 지원되지 않음
  - 현재 **Chrome 94+**에서만 지원됨(⚠️ Edge, Firefox, Safari 미지원)
  - MDN 공식 문서에서 최신 지원 상태 확인 필요
- 작업이 즉시 실행된다는 보장이 없음
  - postTask()는 브라우저의 내부 스케줄링 정책에 따라 실행됨
  - 즉, "user-blocking"이라고 해도 이벤트 루프 상황에 따라 지연될 수 있음

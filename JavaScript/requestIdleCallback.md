# requestIdleCallback

브라우저가 할 일이 없고 한가할 때(Idle Time) 콜백 함수를 실행하는 API

## 사용 목적

- 백그라운드에서 실행해야 하는 작업을 브라우저가 최적의 타이밍에 실행하도록 유도
- 사용자 인터랙션(클릭, 스크롤 등)을 방해하지 않음 -> UX 개선

## 기본 사용법

```
requestIdleCallback((idleDeadline) => {
  console.log("브라우저가 한가할 때 실행!");
});
```

위 코드가 실행되는 시점:

- 브라우저가 UI 렌더링, 애니메이션, 사용자 입력 처리 등 중요한 작업을 다 끝낸 후
- 남는 시간이 있을 때(idle time) 실행됨

## 활용

idleDeadline 객체는 현재 남은 한가한 시간(ms)을 제공

```
requestIdleCallback((idleDeadline) => {
  while (idleDeadline.timeRemaining() > 0) {
    console.log(`남은 시간: ${idleDeadline.timeRemaining()}ms 동안 작업 실행!`);
  }
});
```

- idleDeadline.timeRemaining()을 이용하면 지정된 시간 내에서만 작업 실행 가능
- timeRemaining()이 0이 되면 실행을 멈추고, 다음 requestIdleCallback()에서 이어서 실행

## 예제

```
function processTasks(deadline) {
  while (deadline.timeRemaining() > 0 && tasks.length > 0) {
    console.log("작업 실행:", tasks.shift());
  }
  
  if (tasks.length > 0) {
    requestIdleCallback(processTasks);
  }
}

const tasks = ["Task 1", "Task 2", "Task 3", "Task 4"];
requestIdleCallback(processTasks);
```

동작 방식:

- tasks 배열의 작업을 하나씩 처리
- requestIdleCallback()을 반복 호출하면서 브라우저가 한가할 때마다 실행

## setTimeout과 차이점

**실행 시점**
  - setTimeout: 이벤트 루프에서 실행
  - requestIdleCallback: 브라우저가 한가할 때 실행

**주요 사용처**
  - setTimeout: ASAP 실행 (하지만 UI 인터랙션 방해 가능)
  - requestIdleCallback: 백그라운드 데이터 처리, 성능 최적화

## timeout 옵션

브라우저가 계속 바쁘다면 requestIdleCallback()이 실행되지 않을 수도 있음 -> timeout을 설정해서 최대 대기 시간을 지정

```
requestIdleCallback(() => {
  console.log("최대 2초까지 기다렸다가 실행!");
}, { timeout: 2000 });
```

- 설정한 timeout이 지나면, 브라우저가 한가하지 않더라도 강제로 실행됨
- 즉, 중요한 작업은 timeout을 설정해서 보장할 수 있음

## 활용 사례

- 사용자 경험을 방해하지 않으면서, 추가적인 작업을 수행할 때
- 저사양 기기에서도 원활하게 실행되도록 최적화할 때
- 사용자가 직접 요청하지 않은 부가적인 데이터 로딩(예: 캐싱, 분석 데이터 수집)
- Lazy Loading(필요한 경우에만 데이터 가져오기)
- SEO 크롤러를 위한 추가 데이터 처리

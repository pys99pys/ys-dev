# 스케줄러 API(Scheduler API)

브라우저가 태스크 실행을 관리할 수 있도록 도와주는 API

## 대표적인 스케줄링 API

- setTimeout(), setInterval(): 일정 시간 후/주기적으로 실행
- requestAnimationFrame(): 화면 리페인트 전에 실행(애니메이션 최적화)
- requestIdleCallback(): 브라우저가 한가할 때 실행(백그라운드 작업)
- queueMicrotask(): 현재 실행 중인 코드가 끝난 직후 실행
- scheduler.postTask()(실험적): 우선순위 기반 작업 실행

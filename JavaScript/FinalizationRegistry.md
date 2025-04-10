# FinalizationRegistry

자바스크립트에서 객체가 GC 대상이 되었을 때, 감지해서 특정 동작을 실행할 수 있게 해주는 API

-> 객체가 메모리에서 해제될 때 호출될 콜백을 등록할 수 있는 기능

## 사용법

```
const registry = new FinalizationRegistry((heldValue) => {
  console.log(`GC됨: ${heldValue}`);
});

let obj = { name: "yoonseo" };

// 이 객체가 GC 대상이 되면 위 콜백이 호출됨
registry.register(obj, "yoonseo 객체");

// 나중에 참조 해제
obj = null;
```

## 특징

- 객체가 GC될 직후에 콜백 실행: 정확한 시점은 보장 X(비동기, 내부 타이밍에 따름)
- 비동기적으로 실행됨: 현재 코드 흐름과 별개로 나중에 실행됨
- 자주 쓰이는 용도: 캐시 정리, 리소스 클리어, 로깅 등
- 단점:	콜백 타이밍이 예측 불가 -> 로직에 의존하면 안 됨

## 예시

**캐시에서 자동 삭제 처리**

```
const cache = new Map();
const registry = new FinalizationRegistry((key) => {
  cache.delete(key);
});

function loadData(key, value) {
  let data = { value };
  cache.set(key, data);

  registry.register(data, key); // data가 GC되면 key로 cache에서 삭제
  return data;
}

let userData = loadData("user", "yoonseo");
userData = null; // 이제 data 객체는 GC 대상 → 자동으로 cache에서 제거됨
```

## 주의 사항

- FinalizationRegistry는 의존하지 말고 참고용으로만 사용해야 함
- GC 타이밍은 엔진이 결정하므로, 정확한 실행 순서를 보장하지 않음
- 보통 캐시나 리소스 정리 목적 외에는 잘 안 씀

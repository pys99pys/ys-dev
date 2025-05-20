# IntersectionObserver

브라우저에서 대상 요소가 뷰포트 또는 다른 요소와 교차(Intersection) 되는지를 비동기적으로 관찰할 수 있는 API

## 특징

- 비동기 관찰: 스크롤 이벤트를 직접 다루지 않고 효율적으로 관찰
- 퍼포먼스 향상: requestAnimationFrame이나 scroll 이벤트보다 효율적
- 옵션 설정 가능: 관찰 대상, 루트 요소, margin, threshold 조정 가능
- 여러 요소 동시 관찰 가능

## 예시

```
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      console.log("보임!", entry.target);
      // 예: 이미지 로딩, 애니메이션 시작 등
      observer.unobserve(entry.target); // 한 번만 관찰하려면
    }
  });
}, {
  root: null, // viewport
  rootMargin: "0px",
  threshold: 0.5 // 50% 이상 보여야 감지됨
});

// 관찰할 대상
const target = document.querySelector('.observe-me');
observer.observe(target);
```

## 장점

- 고성능: scroll 이벤트 대비 성능 우수
- 코드 간결: 이벤트 제거 등 수동 관리 필요 없음
- 다양한 설정 지원: threshold, root 등 유연성 있음
- SPA에서 유용: 컴포넌트 단위 lazy load에 적합

## 단점

- IE 미지원 (Polyfill 필요)
- 관찰 해제 안 하면 메모리 누수
- 애니메이션 세밀 제어가 어려울 수도 있음(단순 노출 감지에는 좋음)

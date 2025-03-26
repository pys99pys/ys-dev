# 버블링(Bubbling) vs 캡처링(Capturing)

DOM에서 이벤트가 발생하면, 그 이벤트는 부모 → 자식 → 목표 → 다시 부모로 올라가는 단계적 흐름을 거쳐서 전달되는 개념

## 흐름

1. 캡처링(Capturing) 단계
- window -> document -> … -> 이벤트 대상(element) 까지 내려감
2. 타겟(Target) 단계
- 실제 이벤트가 발생한 요소에서 실행
3. 버블링(Bubbling) 단계
- 이벤트 대상에서 다시 위로 올라감
- 부모 -> 조상 -> … -> document, window

## 예시

**HTML**
```
<div id="parent">
  <button id="child">클릭</button>
</div>
```

**JS**
```
document.getElementById("parent").addEventListener("click", () => {
  console.log("부모 클릭!");
});

document.getElementById("child").addEventListener("click", () => {
  console.log("자식 클릭!");
});
```

**출력**
```
자식 클릭!
부모 클릭!
```

## 캡처링 사용

기본은 버블링, 캡처링을 쓰려면 아래처럼 true 전달
```
document.getElementById("parent").addEventListener(
  "click",
  () => {
    console.log("캡처링 단계에서 부모 감지됨");
  },
  true // <- 캡처링 단계에서 실행
);
```

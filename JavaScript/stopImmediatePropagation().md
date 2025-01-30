# stopImmediatePropagation()

stopPropagation()과 비슷하지만, 같은 요소에서 실행되는 다른 이벤트 핸들러까지 차단한다는 차이가 있음

## stopPropagation()과의 차이

- stopPropagation(): 부모로 전파만 막음(같은 요소의 다른 이벤트 리스너는 실행됨)
- stopImmediatePropagation(): 부모로 전파도 막고, 같은 요소의 다른 이벤트 리스너도 실행 안 됨

## 예제

**HTML**

```
<button id="btn">클릭</button>
```

### stopPropagation()

```
document.getElementById("btn").addEventListener("click", function (event) {
  event.stopPropagation();
  console.log("첫 번째 핸들러 실행");
});

document.getElementById("btn").addEventListener("click", function () {
  console.log("두 번째 핸들러 실행");
});

// 버튼 클릭시
// 첫 번째 핸들러 실행
// 두 번째 핸들러 실행
```

### stopImmediatePropagation()

```
document.getElementById("btn").addEventListener("click", function (event) {
  event.stopImmediatePropagation();
  console.log("첫 번째 핸들러 실행 (stopImmediatePropagation)");
});

document.getElementById("btn").addEventListener("click", function () {
  console.log("두 번째 핸들러 실행");
});

// 버튼 클릭시
// 첫 번째 핸들러 실행
```

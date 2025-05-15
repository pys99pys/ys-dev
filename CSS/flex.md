# flex

일차원(1D) 레이아웃 시스템, 가로 또는 세로 한 방향으로 정렬할 때 사용

- 부모가: flex container
- 자식: flex item

## 기본 구조

```
<style>
.flex-container {
  display: flex;
}
</style>

<div class="flex-container">
  <div>1</div>
  <div>2</div>
  <div>3</div>
</div>
```

## flex 컨테이너 속성

| 속성                | 값                                                   | 설명            |
| ----------------- | --------------------------------------------------- | ------------- |
| `display`         | `flex`                                              | flex 컨테이너로 선언 |
| `flex-direction`  | `row` / `column` / `row-reverse` / `column-reverse` | 주축 방향 설정      |
| `flex-wrap`       | `nowrap` / `wrap` / `wrap-reverse`                  | 줄바꿈 여부        |
| `justify-content` | `flex-start` / `center` / `space-between` 등         | **주축 정렬**     |
| `align-items`     | `stretch` / `center` / `flex-start` 등               | **교차축 정렬**    |
| `align-content`   | 여러 줄일 때 교차축 정렬                                      | 여러 줄에만 적용됨    |

## flex 아이템 속성

| 속성            | 설명                                             |
| ------------- | ---------------------------------------------- |
| `flex-grow`   | 남는 공간을 얼마나 키워서 차지할지 (비율)                       |
| `flex-shrink` | 공간이 부족할 때 얼마나 줄일지 (비율)                         |
| `flex-basis`  | 기본 크기 설정 (`width`와 비슷하지만 우선순위 다름)              |
| `flex`        | `grow shrink basis`의 축약형 (예: `flex: 1 0 auto`) |
| `align-self`  | 아이템 개별 정렬 (`align-items`를 덮어씀)                 |
| `order`       | 아이템 순서 조정 (기본값 0, 낮을수록 먼저)                     |

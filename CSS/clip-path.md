# clip-path

요소의 보이는 영역(클리핑 영역)을 정의하는 CSS 속성 ->  특정한 형태로 요소를 잘라내서 보이게 할 수 있음

## 특징

- 요소를 특정 모양으로 자를 수 있음
- 보이지 않는 부분은 마우스 이벤트를 받지 않음
- overflow: hidden;과 비슷하지만 더 정교한 형태를 만들 수 있음
- 애니메이션과 함께 사용하면 다양한 효과를 만들 수 있음


## 기본 문법

```
selector {
  clip-path: shape(arguments);
}
```

- shape(arguments) 부분에 원하는 형태를 정의

## 사용 가능한 값

- circle(): clip-path: circle(50%) ->	원형
- ellipse():	clip-path: ellipse(50% 30% at 50% 50%); ->	타원형
- polygon():	clip-path: polygon(0% 0%, 100% 0%, 50% 100%) ->	다각형
- inset():	clip-path: inset(10% 20% 30% 40%); ->	박스 내부 자르기

## 중심점 -> at 키워드

**기본 (at 생략)**

```
.circle {
  clip-path: circle(50%);
}
```

- at을 생략하면 기본적으로 **at 50% 50% (가운데 정렬)**로 적용됨

**at을 사용하여 위치 변경**

```
.circle-top-left {
  clip-path: circle(50% at 0% 0%);
}
```

- **원의 중심이 요소의 왼쪽 상단 (0%, 0%)**으로 이동됨

```
.circle-bottom-right {
  clip-path: circle(50% at 100% 100%);
}
```

- **원의 중심이 요소의 오른쪽 하단 (100%, 100%)**으로 이동됨

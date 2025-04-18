# DAC(Divide and Conquer)

분할 정복 원칙에 기반하여 문제를 더 작고 관리하기 쉬운 단위로 나누고 각각의 단위를 독립적으로 해결한 뒤 이를 결합하여 전체 문제를 해결하는 방법

소프트웨어 설계뿐만 아니라 알고리즘, 시스템 설계, 프로젝트 관리 등 다양한 분야에서 사용됨

## 기본 개념

### 1. 분할(Divide)

- 문제를 더 작은 하위 문제로 분할
- 하위 문제는 원래 문제와 동일한 성질을 가지거나 더 간단한 형태가 되어야 함

### 정복(Conquer)

- 나눈 하위 문제를 개별적으로 해결
- 일반적으로 재귀적으로 해결하거나 특정 알고리즘을 사용

### 결합(Combine)

- 해결된 하위 문제를 조합하여 원래 문제의 답을 얻음

## 특징

- 재귀적 접근: 하위 문제를 더 작은 단위로 나누는 과정이 반복적으로 이루어짐
- 병렬성 가능: 하위 문제를 독립적으로 처리할 수 있어 병렬화에 적합
- 복잡도 관리: 복잡한 문제를 작게 나누어 단계적으로 접근

## 예제

문제를 절반으로 나누고 정렬한 뒤 합치는 알고리즘

```
function mergeSort(arr) {
  // Base case: 배열이 1개 이하이면 이미 정렬된 상태
  if (arr.length <= 1) return arr;

  // Divide: 배열을 절반으로 나눔
  const mid = Math.floor(arr.length / 2);
  const left = mergeSort(arr.slice(0, mid));
  const right = mergeSort(arr.slice(mid));

  // Conquer & Combine: 두 정렬된 배열을 병합
  return merge(left, right);
}

function merge(left, right) {
  let result = [];
  while (left.length && right.length) {
    if (left[0] < right[0]) {
      result.push(left.shift());
    } else {
      result.push(right.shift());
    }
  }
  return result.concat(left, right);
}

console.log(mergeSort([5, 3, 8, 4, 2])); // [2, 3, 4, 5, 8]
```

## DAC를 활용한 시스템 설계

문제: 대규모 파일을 처리해야 하는 시스템 설계

**1. Divide(분할)**
  - 큰 파일을 여러 작은 청크(chunk)로 나눔
  - 각 청크는 독립적으로 처리 가능
**2. Conquer (정복)**
  - 각 청크를 병렬로 처리 (데이터 분석, 변환 등)
  - 예: AWS Lambda, MapReduce, Spark 같은 도구 활용
**3. Combine (결합)**
  - 처리된 청크들을 다시 합쳐서 최종 결과를 생성

## 장점

### 1. 문제 해결이 체계적

- 복잡한 문제를 단계적으로 접근 가능
- 하위 문제 단위로 관리할 수 있어 디버깅이 쉬움

### 2. 병렬 처리에 적합

- 독립된 하위 문제들은 병렬로 처리할 수 있어 성능 향상

### 3. 확장성

- 문제를 작게 나눴기 때문에 새로운 요구사항이 추가될 때 적응하기 쉬움

## 단점

### 1. 오버헤드 발생

- 너무 많은 하위 문제로 나누면 관리 비용이 증가할 수 있음
- 특히 재귀 호출에서 스택 오버플로우 발생 가능

### 2. 조합의 복잡성

- 하위 문제의 결과를 결합하는 단계가 어려운 경우 설계가 복잡해질 수 있음

## 사례

1. 알고리즘 설계: 병합 정렬, 퀵 정렬, 이진 탐색 등
2. 분산 시스템: Hadoop, Spark 같은 데이터 처리 시스템은 DAC 원칙을 기반으로 동작
3. 웹 서비스: 백엔드의 마이크로서비스 아키텍처 설계, 각각의 마이크로서비스는 독립적인 하위 문제를 해결하고 API를 통해 통합
4. 게임 개발: 복잡한 게임 로직을 모듈화하여 설계

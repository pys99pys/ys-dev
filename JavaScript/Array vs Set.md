# Array vs Set

## 성능 비교

- 추가(add or push)
  - Array: O(1) (끝에 추가), O(n) (중간 삽입)
  - Set: O(1)
- 삭제(remove or splice)
  - Array: O(n) (탐색 후 삭제)
  - Set: O(1)
- 검색(includes or has)
  - Array: O(n)
  - Set: O(1)
- 반복문 처리(forEach, map)
  - Array: O(n)
  - Set: O(n)

## Set이 좋을 때

- 중복 없는 데이터를 저장하고 싶을 때
  - Set은 중복을 자동으로 제거해 주므로 Array.includes()로 중복 체크할 필요가 없음
- 빠른 검색이 필요할 때
  - Set.has(value)는 O(1)이라 Array.includes(value)의 O(n)보다 빠름.
- 삭제가 자주 발생할 때
  -  Set.delete(value)는 O(1), Array.splice()는 O(n)이라 차이가 큼

## Array가 좋을 때

- 순서가 중요한 경우
  - Set은 삽입 순서를 유지하지만, Array처럼 인덱스로 접근하는 기능이 부족
- 인덱스 기반 접근이 필요할 때
  - arr[i]처럼 특정 위치의 요소를 가져오는 게 Set에서는 불가능함
- 맵핑, 필터링, 리듀스 등의 배열 메서드를 자주 사용할 때
  - Array는 map(), filter(), reduce() 같은 고차 함수가 많지만, Set은 직접 지원하지 않음(필요하면 [...set]으로 변환해야 함)

## 결론

- 중복 제거 + 빠른 검색/삭제 -> Set
- 순서 유지 + 인덱스 접근 + 배열 메서드 사용 -> Array

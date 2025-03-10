# Object vs Map

## 성능 비교

- 추가(obj[key] = value, map.set(key, value))
  - Object: O(1)
  - Map: O(1)
- 삭제(delete obj[key], map.delete(key))
  - Object: O(1) (하지만 메모리 해제가 비효율적일 수 있음)
  - Map: O(1)
- 검색 (key in obj, map.has(key))
  - Object: O(1)
  - Map: O(1)
- 반복(for...in, Object.keys())
  - Object: O(n) (키를 배열로 변환해야 함)
  - Map: O(n) (반복 전용 메서드 제공)
- 키의 타입
  - Object: 문자열 또는 Symbol만 가능
  - Map: 모든 값 가능 (객체 포함)
- 순서 보장
  - 키 순서 보장 X
  - 키 삽입 순서 보장 O
- 메모리 사용량
  - 더 적음
  - 더 많음

## Map이 좋을 때

- 키로 문자열이 아닌 값을 사용하고 싶을 때
  - Map은 숫자, 객체, 함수 등을 키로 사용할 수 있음
- 키 순서를 유지해야 할 때
  - Map은 삽입 순서를 보장하지만, Object는 순서가 일정하지 않을 수도 있음
- 데이터의 크기가 크고 성능이 중요한 경우
  - Map은 내부적으로 최적화되어 있어서 큰 데이터셋에서 성능이 더 좋음
- 반복이 많을 때
  - Map은 .keys(), .values(), .entries() 같은 반복 전용 메서드 제공
 
## Object가 좋을 때

- JSON 데이터와 호환해야 할 때
  - JSON.parse()와 JSON.stringify()는 Object만 지원함
- 간단한 키-값 저장용으로 사용할 때
  - 작은 크기의 데이터를 저장하고, 키가 문자열이라면 Object로도 충분함
- 프로토타입을 활용해야 할 때
  - Object는 프로토타입 체인을 지원해 메서드 상속이 가능하지만, Map은 불가능

## 결론

- 키로 객체, 숫자 등 다양한 타입을 쓰고 싶다면 -> Map
- 데이터 크기가 크고 성능이 중요한 경우 -> Map
- JSON과 호환성이 필요하거나 간단한 키-값 저장용이면 -> Object

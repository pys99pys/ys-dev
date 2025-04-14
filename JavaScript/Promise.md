# Promise

비동기 작업의 완료(또는 실패)를 처리하기 위한 JavaScript 객체

## 필요한 이유

JavaScript는 기본적으로 싱글 스레드 언어
-> 오래 걸리는 작업(API 호출, 타이머 등)을 기다리면 전체 앱이 멈춰버림

그래서 비동기 처리 방식이 필요해짐
-> 기존에는 callback을 썼는데, 콜백 지옥(callback hell) 문제 발생
-> 그래서 나온 게 Promise

## 개념

- 객체: Promise는 new Promise()로 만든 객체
- 비동기: 시간이 걸리는 작업(예: API 요청)을 처리하는 데 사용
- 상태 관리: pending -> fulfilled or rejected의 상태를 가짐
- 체이닝: `.then()`, `.catch()`, `.finally()`로 후속 작업 처리 가능

## 상태 흐름

- 생성 -> pending -> resolve() -> fulfilled
- 생성 -> pending -> reject() ->  rejected

## 관련 메서드

- `.then()`: 성공했을 때 실행되는 함수 등록
- `.catch()`: 실패했을 때 실행되는 함수 등록
- `.finally()`: 성공/실패 관계없이 항상 실행
- `Promise.all()`: 여러 Promise를 동시에 처리, 모두 성공해야 fulfilled
- `Promise.race()`: 가장 먼저 끝난 Promise 기준으로 처리됨, 성공 or 실패
- `Promise.allSettled()`: 모두 끝날 때까지 기다리고 결과 배열로 반환
- `Promise.any()`: 하나라도 성공하면 fulfilled

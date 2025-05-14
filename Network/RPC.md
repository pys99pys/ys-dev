# RPC(Remote Procedure Call - 원격 프로시저 호출)

네트워크를 통해 다른 컴퓨터에 있는 함수를 로컬 함수처럼 호출할 수 있게 해주는 통신 방식

## 특징

- 직관적: 함수 호출처럼 보이지만, 실제론 네트워크 요청
- 추상화: 네트워크 처리(직렬화, 전송, 응답 등)를 숨김
- 양방향 통신 가능: 클라이언트가 서버 함수 호출 가능(반대도 가능)
- 다양한 프로토콜: HTTP, gRPC, WebSocket 등으로 구현 가능

## 구조 예시

- 클라이언트: getUser(1) 호출
- 실제로는 네트워크 요청 -> GET /user/1 전송
- 서버: 요청을 받아 getUser 함수 실행 후 결과 반환
- 클라이언트는 결과를 받아 사용

## 자바스크립트 예시

```
// 클라이언트 측
async function getUser(id) {
  const res = await fetch(`/api/getUser?id=${id}`);
  return await res.json();
}

// 사용
getUser(1).then((user) => console.log(user));
```

## gRPC

- Google의 고성능 RPC 프레임워크

### gRPC 특징

- protobuf 사용
- HTTP/2 기반
- 타입 안정성, 빠른 속도 제공

### gRPC 예시

```
// user.proto
service UserService {
  rpc GetUser(GetUserRequest) returns (UserResponse);
}
```

## 장점

- 직관적(함수 호출처럼 사용)	
- 코드 재사용성과 구조화에 좋음
- gRPC 등 사용 시 빠르고 타입 안정성 ↑

## 단점

- 네트워크 장애 시 디버깅 어려움
- 버전 관리/호환성 유지가 중요
- 브라우저 환경에선 제한적(ex: gRPC-web 필요)

## 사용 예시

- 마이크로서비스 간 통신 (ex: gRPC, Thrift)
- 브라우저 -> 서버 간 간단한 RPC 구현
- 백엔드 시스템 간 API 호출
- 게임 서버, IoT 기기 제어 등 실시간 처리

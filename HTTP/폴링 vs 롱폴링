# 폴링 vs 롱폴링(Polling vs Long Polling)

클라이언트와 서버 간의 데이터를 주기적으로 또는 지속적으로 교환하는 방법

## 폴링(Polling)

### 동작 방식

- 클라이언트가 주기적으로 서버에 요청을 보내 데이터가 있는지 확인
- 데이터가 있으면 응답으로 반환, 없으면 빈 응답을 보냄
- 일정한 간격으로 계속 요청을 보내므로 반복적인 통신 발생

### 장점

- 구현이 간단하고 HTTP 요청-응답 모델과 잘 맞음
- 서버가 별도의 상태를 유지할 필요가 없음

### 단점

- 비효율적: 데이터가 없는 경우에도 클라이언트가 요청을 보내므로 네트워크와 서버 자원 낭비
- 지연 시간: 새로운 데이터가 생겨도 다음 요청 전까지 클라이언트가 알 수 없음

## 예제

```
setInterval(async () => {
  const response = await fetch('/server-endpoint');
  const data = await response.json();
  console.log(data);
}, 5000); // 5초마다 요청
```

## 롱폴링(Long Polling)

### 동작 방식

- 클라이언트가 서버에 요청을 보내고, 서버는 새로운 데이터가 생길 때까지 응답을 지연
- 새로운 데이터가 생기면 즉시 응답하고, 클라이언트는 데이터를 받고 다시 요청을 보냄
- 데이터를 즉시 전달하면서 폴링의 자원 낭비를 줄임

### 장점

- 효율성: 데이터가 준비될 때까지 서버가 대기하므로 불필요한 요청 감소
- 실시간성 강화: 새로운 데이터가 생기면 즉시 클라이언트에게 전달

### 단점

- 구현이 상대적으로 복잡
- 서버 자원 소모: 대기 상태의 요청이 많아지면 서버에 부하가 걸릴 수 있음
- 네트워크 제한: 일부 프록시 서버나 방화벽에서 긴 대기 요청을 차단할 가능성

### 예제

```
const longPolling = async () => {
  try {
    const response = await fetch('/server-endpoint');
    const data = await response.json();
    console.log(data);
    // 새로운 데이터가 도착하면 즉시 처리 후 다시 요청
    longPolling();
  } catch (error) {
    console.error('Error:', error);
    setTimeout(longPolling, 5000); // 실패 시 5초 후 재시도
  }
};

longPolling();
```

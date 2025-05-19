# SSE(Server-Sent Events)

서버 → 클라이언트(브라우저)로의 단방향 통신을 위한 기술, 클라이언트가 연결을 하면 서버가 계속 데이터를 푸시(push)하는 구조

## 특징

- 단방향 스트리밍: 서버가 클라이언트로 지속적으로 데이터 전송
- HTTP 기반: 일반 HTTP 연결을 사용(WebSocket처럼 별도 프로토콜을 사용할 필요 없음)
- 브라우저에서 기본 지원: JavaScript의 EventSource 객체로 쉽게 사용 가능

## 예시

**서버(Express)**

```
app.get('/sse', (req, res) => {
  res.setHeader('Content-Type', 'text/event-stream');
  res.setHeader('Cache-Control', 'no-cache');
  res.setHeader('Connection', 'keep-alive');

  res.write(`data: 안녕하세요!\n\n`);

  const interval = setInterval(() => {
    res.write(`data: ${new Date().toISOString()}\n\n`);
  }, 2000);

  req.on('close', () => {
    clearInterval(interval);
  });
});
```

**클라이언트(브라우저)**

```
const eventSource = new EventSource('/sse');

eventSource.onmessage = (event) => {
  console.log('서버로부터 메시지:', event.data);
};
```

## 장점

- HTTP 기반이라 방화벽, 프록시 환경에서 잘 동작
- 간단한 구현
- 자동 재연결 기능 내장
- 텍스트 기반 스트리밍에 적합(ex. 로그, 알림)

## 단점

- 단방향(클라이언트 -> 서버로 메시지 전송은 불가능)
- 구형 브라우저 지원 X
- 바이너리 전송 불가(텍스트만 가능)

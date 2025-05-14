# Protocol Buffers

Google이 개발한 구조화된 데이터 직렬화 포맷, 데이터를 빠르고 작게, 언어와 플랫폼에 상관없이 주고받을 수 있게 해주는 기술

## 특징

- 빠름: JSON보다 훨씬 빠른 직렬화/역직렬화 속도
- 작음: JSON에 비해 전송 데이터 크기가 훨씬 작음(바이너리 포맷)
- 스키마 기반: .proto 파일에 데이터 구조를 명시
- 다양한 언어 지원: JS, Go, Python, Java, C++ 등
- 자동 코드 생성: .proto 파일 -> 각 언어별 클래스/인터페이스 자동 생성

## 예시

```
syntax = "proto3";

message User {
  int32 id = 1;
  string name = 2;
  string email = 3;
}
```

-> 컴파일 후

```
const user = new User();
user.setId(1);
user.setName("윤서");
user.setEmail("yoonseo@example.com");
```

## vs JSON

| 항목      | Protocol Buffers    | JSON     |
| ------- | ------------------- | -------- |
| **형식**  | 바이너리                | 텍스트      |
| **성능**  | 매우 빠름               | 상대적으로 느림 |
| **크기**  | 작음                  | 큼        |
| **스키마** | 필요 (`.proto` 필수)    | 없음       |
| **가독성** | 낮음 (바이너리라 사람이 못 읽음) | 높음       |

## 사용처

- gRPC와 함께 쓰는 것이 가장 대표적인 활용처
- 마이크로서비스 간 통신
- 대용량, 고속 데이터 처리
- 네트워크 비용이 중요한 모바일 환경

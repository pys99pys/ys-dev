# semver(Semantic Versioning, 의미론적 버전 관리)

소프트웨어의 버전 번호에 명확한 의미와 규칙을 부여하는 버전 관리 시스템

## 형식

```
MAJOR.MINOR.PATCH
```

- 예: 1.4.2 → Major: 1, Minor: 4, Patch: 2

## 의미

- MAJOR: 호환되지 않는 API 변경이 있을 때
- MINOR: 호환되는 기능 추가
- PATCH: 호환되는 버그 수정

## 범위 기회

- `^`: 최신 MINOR/PATCH 버전 허용(^1.2.3 → 1.x.x)
- `~`: 최신 PATCH만 허용(~1.2.3 → 1.2.x)
- `*`: 모든 버전 허용
- `>=`, `<`:	범위 조건 명시 가능

```
// 4.x.x까지 설치됨 (5.0.0은 설치 안 됨)

"dependencies": {
  "lodash": "^4.17.15"
}
```

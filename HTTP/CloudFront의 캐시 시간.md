오리진의 Cache-Control, Expires와 CloudFront의 TTL에 의한 캐시 시간

## Cache-Control 헤더와 TTL에 따른 캐싱

- 오리진에 Cache-Control: max-age 헤더가 있는 경우
  - 최소 TTL = 0
    - CloudFront: max-age, 최대 TTL 중 작은 값 만큼 캐싱
    - 브라우저: max-age 만큼 캐싱
  - 최소 TTL > 0
    - CloudFront
      - 최소 TTL < max-age < 최대 TTL인 경우: max-age 만큼 캐싱
      - max-age < 최소 TTL인 경우: 최소 TTL 만큼 캐싱
      - max-age > 최대 TTL인 경우: 최대 TTL 만큼 캐싱
    - 브라우저: max-age 만큼 캐싱
- 오리진에 Cache-Control: max-age 헤더가 없는 경우
  - 최소 TTL = 0
    - CloudFront: 기본 TTL 만큼 캐싱
    - 브라우저: 브라우저 정책을 따름
  - 최소 TTL > 0
    - CloudFront: 최소 TTL, 기본 TTL 중 큰 값 만큼 캐싱
    - 브라우저: 브라우저 정책을 따름
- 오리진에 Cache-Control: max-age 및 s-max-age 헤더가 있는 경우
  - 최소 TTL = 0
    - CloudFront: s-max-age, 최소 TTL 중 작은 값 만큼 캐싱
    - 브라우저: max-age 만큼 캐싱
  - 최소 TTL > 0
    - CloudFront
      - 최소 TTL < ㄴ-max-age < 최대 TTL인 경우: max-age 만큼 캐싱
      - s-max-age < 최소 TTL인 경우: 최소 TTL 만큼 캐싱
      - s-max-age > 최대 TTL인 경우: 최대 TTL 만큼 캐싱
    - 브라우저: max-age 만큼 캐싱
- 오리진에 Expires 헤더가 있는 경우
  - 최소 TTL = 0
    - CloudFront: Expires, 최대 TTL 중 더 빠른 날짜의 객체를 캐싱
    - 브라우저: Expires의 날짜까지 캐싱
  - 최소 TTL > 0
    - CloudFront
      - 최소 TTL < Expires < 최대 TTL인 경우: Expires 까지 캐싱
      - Expires < 최소 TTL인 경우: 최소 TTL 만큼 캐싱
      - Expires > 최대 TTL인 경우: 최대 TTL 만큼 캐싱
    - 브라우저: Expires의 날짜까지 캐싱

## 주의 사항

최소 TTL > 0 인 경우 ClodFront는 Cache-Control: no-cache, no-store 또는 private 지시문이 있더라도 최소 TTL을 사용

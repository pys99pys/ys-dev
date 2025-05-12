# SSR, SSG, ISG

## SSR(Server Side Rendering)

- 요청이 들어올 때마다 서버에서 HTML 생성
- SEO와 실시간 데이터에 유리

```
export async function getServerSideProps() {
  const res = await fetch('https://api.example.com/data');
  const data = await res.json();
  return { props: { data } };
}
```

### 장점

- 항상 최신 데이터
- SEO에 적합

### 단점

- 요청마다 렌더링 -> 느리고 서버 부하 큼

### 사례

- 대시보드
- 로그인 사용자 페이지

## SSG(Static Site Generation)

- 빌드 시 HTML 생성 후 업로드
- 정적 페이지에 적합

```
export async function getStaticProps() {
  const res = await fetch('https://api.example.com/data');
  const data = await res.json();
  return { props: { data } };
}
```

### 장점

- 가장 빠름
- 서버 부하 없음(CDN에서 처리)

### 단점

- 데이터가 바뀌면 재빌드 필요
- 실시간 반영 어려움

### 사례

- 블로그
- 소개 페이지

## ISR(Incremental Static Regeneration)

- SSG처럼 정적 생성하지만, revalidate 시간마다 백그라운드에서 페이지 재생성
- 최신성과 성능을 동시에 확보

```
export async function getStaticProps() {
  const res = await fetch('https://api.example.com/data');
  const data = await res.json();
  return {
    props: { data },
    revalidate: 60, // 60초마다 새로 렌더링
  };
}
```

### 장점

- CDN 기반 빠른 응답
- 실시간에 가까운 갱신

### 단점

- 초기 요청자는 낡은 데이터 볼 수 있음
- 미묘한 동기화 타이밍 문제 발생 가능

### 사례

- 상품 상세 페이지
- 뉴스 목록

# TanStack Query 데이터 상태

## 쿼리 상태

- idle: 쿼리가 아직 실행되지 않음
- loading: 쿼리가 처음 실행되거나 refetch 중
- success: 쿼리 성공적으로 완료됨
- error: 쿼리 실패

## 데이터 상태

- fresh:	데이터가 신선하고 최신, 재요청 불필요
- stale: 데이터가 오래됐다고 간주됨, 리패치 후보
- inactive: 사용 중이 아니고 캐시만 유지됨
- garbage collected: 캐시 시간이 지나 삭제됨(cacheTime 만료)

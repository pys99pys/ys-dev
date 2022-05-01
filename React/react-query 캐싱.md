## 캐시 상태

### stale

- 최신화가 필요한 상태
- 새로운 쿼리가 실행되거나
- 브라우저에 새로 focus 되거나 (refetchOnWindowFocus옵션 활성화시)
- 네트워크가 다시 연결되거나
- 등등 새로운 쿼리가 필요한 상태일때 refetch됨

### fresh

- 정상적으로 캐시된 상태
- refetch하지 않음
- 기본적으로 모든 query는 stale한 상태, 따라서 별도 옵션을 지정하지 않으면 캐시되지 않음

## use-uqery 캐시 옵션

- staleTime과 cacheTime으로 캐시를 조절
- staleTime(default 0): 캐시된 후 해당 시간동한 fresh 상태를 유지
- cacheTime(default 5분): 해당 시간만큼 캐시
- 따라서 cacheTime 옵션을 설정해도 기본 staleTime이 0이기 때문에 캐시되지 않으며, staleTime 을 줘야 캐시가 동작함
- queryClient.invalidateQueries() 로 캐시 초기화 가능

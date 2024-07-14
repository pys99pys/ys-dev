Promise를 제거한 타입

```
export type Providers = Awaited<ReturnType<typeof getProviders>>;
```

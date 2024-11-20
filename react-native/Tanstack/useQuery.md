## React Query의 `useQuery` 훅 사용 가이드

`useQuery` 훅은 서버에서 데이터를 가져오고, 상태를 관리하는 강력한 도구입니다. 이 글에서는 `useQuery`의 다양한 파라미터와 반환 값을 이해하고, 어떻게 사용하는지에 대해 자세히 설명하겠습니다. 특히 한국어로 설명하면서, 개발자들이 더 쉽게 접근할 수 있도록 하겠습니다.
```
const {
  data,
  dataUpdatedAt,
  error,
  errorUpdatedAt,
  failureCount,
  failureReason,
  fetchStatus,
  isError,
  isFetched,
  isFetchedAfterMount,
  isFetching,
  isInitialLoading,
  isLoading,
  isLoadingError,
  isPaused,
  isPending,
  isPlaceholderData,
  isRefetchError,
  isRefetching,
  isStale,
  isSuccess,
  promise,
  refetch,
  status,
} = useQuery(
  {
    queryKey,
    queryFn,
    gcTime,
    enabled,
    networkMode,
    initialData,
    initialDataUpdatedAt,
    meta,
    notifyOnChangeProps,
    placeholderData,
    queryKeyHashFn,
    refetchInterval,
    refetchIntervalInBackground,
    refetchOnMount,
    refetchOnReconnect,
    refetchOnWindowFocus,
    retry,
    retryOnMount,
    retryDelay,
    select,
    staleTime,
    structuralSharing,
    throwOnError,
  },
  queryClient,
)
```
### `useQuery` 파라미터 설명 (옵션)

#### 1. `**queryKey: unknown[]**` (필수)

- 이 쿼리에서 사용할 키입니다.
    
- `queryKey`는 안정적인 해시 값으로 변환되며, 키가 변경될 때 쿼리가 자동으로 업데이트됩니다 (단, `enabled`가 `false`로 설정되지 않은 경우).
    

#### 2. `**queryFn: (context: QueryFunctionContext) => Promise<TData>**` (필수, 기본 쿼리 함수가 정의되지 않은 경우)

- 데이터를 요청할 때 사용할 함수입니다.
    
- `QueryFunctionContext`를 인자로 받아야 하며, 데이터로 resolve하거나 오류를 throw하는 Promise를 반환해야 합니다.
    

#### 3. `**enabled: boolean | (query: Query) => boolean**`

- 이 쿼리가 자동으로 실행되지 않도록 하려면 `false`로 설정하세요.
    
- 의존성 쿼리를 사용할 때 유용합니다.
    

#### 4. `**networkMode: 'online' | 'always' | 'offlineFirst'**` (선택 사항, 기본값: `'online'`)

- 네트워크 모드를 설정합니다.
    

#### 5. `**retry: boolean | number | (failureCount: number, error: TError) => boolean**`

- 실패한 쿼리를 재시도하는 횟수를 설정합니다.
    
- `false`로 설정하면 재시도를 하지 않습니다. 숫자로 설정하면 해당 횟수만큼 재시도합니다.
    

#### 6. `**retryOnMount: boolean**` (기본값: `true`)

- 쿼리가 에러가 있는 상태에서 마운트될 때 재시도할지 여부를 설정합니다.
    

#### 7. `**retryDelay: number | (retryAttempt: number, error: TError) => number**`

- 재시도 사이의 지연 시간을 설정합니다. 지연 시간은 밀리초 단위입니다.
    

#### 8. `**staleTime: number | ((query: Query) => number)**` (선택 사항, 기본값: `0`)

- 데이터가 오래되었다고 간주되는 시간 (밀리초 단위)을 설정합니다.
    

#### 9. `**gcTime: number | Infinity**` (기본값: `5분`, SSR의 경우 `Infinity`)

- 사용되지 않거나 비활성화된 캐시 데이터를 메모리에서 유지할 시간 (밀리초 단위)을 설정합니다.
    

#### 10. `**queryKeyHashFn: (queryKey: QueryKey) => string**` (선택 사항)

- 지정된 경우, 이 함수는 `queryKey`를 문자열로 해시하는 데 사용됩니다.
    

#### 11. `**refetchInterval: number | false | ((query: Query) => number | false | undefined)**` (선택 사항)

- 모든 쿼리를 설정된 주기 (밀리초 단위)로 지속적으로 재요청합니다.
    

#### 12. `**refetchIntervalInBackground: boolean**` (선택 사항)

- 브라우저 탭/창이 백그라운드에 있는 동안에도 `refetchInterval`이 설정된 쿼리를 계속해서 재요청할지 설정합니다.
    

#### 13. `**refetchOnMount: boolean | "always" | ((query: Query) => boolean | "always")**` (선택 사항, 기본값: `true`)

- 마운트될 때 데이터가 오래된 경우 쿼리를 다시 요청할지 설정합니다.
    

#### 14. `**refetchOnWindowFocus: boolean | "always" | ((query: Query) => boolean | "always")**` (선택 사항, 기본값: `true`)

- 창이 포커스를 얻을 때 데이터가 오래된 경우 쿼리를 다시 요청할지 설정합니다.
    

#### 15. `**refetchOnReconnect: boolean | "always" | ((query: Query) => boolean | "always")**` (선택 사항, 기본값: `true`)

- 네트워크 연결이 복구될 때 데이터가 오래된 경우 쿼리를 다시 요청할지 설정합니다.
    

#### 16. `**notifyOnChangeProps: string[] | "all" | (() => string[] | "all" | undefined)**` (선택 사항)

- 컴포넌트가 리렌더링되는 조건을 설정합니다.
    

#### 17. `**select: (data: TData) => unknown**` (선택 사항)

- 반환된 데이터의 일부만 선택하거나 변환하는 함수입니다.
    

#### 18. `**initialData: TData | () => TData**` (선택 사항)

- 쿼리 캐시에 초기 데이터로 사용할 값을 설정합니다.
    

#### 19. `**initialDataUpdatedAt: number | (() => number | undefined)**` (선택 사항)

- `initialData`가 마지막으로 업데이트된 시간을 설정합니다.
    

#### 20. `**placeholderData: TData | (previousValue: TData | undefined, previousQuery: Query | undefined) => TData**` (선택 사항)

- 쿼리가 대기 상태일 때 표시할 데이터를 설정합니다.
    

#### 21. `**structuralSharing: boolean | (oldData: unknown | undefined, newData: unknown) => unknown)**` (선택 사항, 기본값: `true`)

- 쿼리 결과 간의 구조적 공유를 설정합니다.
    

#### 22.
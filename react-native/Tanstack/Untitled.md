## React Query의 `useMutation` 훅 사용 가이드

`useMutation` 훅은 서버에 데이터를 보내거나 상태를 변경하는 작업을 비동기로 수행하는 데 매우 유용한 도구입니다. 이 글에서는 `useMutation`의 다양한 파라미터와 반환 값을 이해하고, 어떻게 사용하는지에 대해 자세히 설명하겠습니다.

### `useMutation` 파라미터 설명 (옵션)

#### 1. `**mutationFn: (variables: TVariables) => Promise<TData>**` (필수, 기본 뮤테이션 함수가 정의되지 않은 경우)

- 비동기 작업을 수행하는 함수로, Promise를 반환해야 합니다.
    
- `variables` 객체는 `mutate` 함수가 `mutationFn`에 전달할 변수들을 의미합니다.
    

#### 2. `**gcTime: number | Infinity**`

- 사용되지 않거나 비활성화된 캐시 데이터를 메모리에서 유지할 시간 (밀리초 단위)을 설정합니다.
    
- `Infinity`로 설정하면 캐시 수집이 비활성화됩니다.
    

#### 3. `**mutationKey: unknown[]**` (선택 사항)

- 뮤테이션 키를 설정하여 `queryClient.setMutationDefaults`로 설정된 기본값을 상속받을 수 있습니다.
    

#### 4. `**networkMode: 'online' | 'always' | 'offlineFirst'**` (선택 사항, 기본값: `'online'`)

- 네트워크 모드를 설정합니다.
    

#### 5. `**onMutate: (variables: TVariables) => Promise<TContext | void> | TContext | void**` (선택 사항)

- 뮤테이션 함수가 실행되기 전에 실행되는 함수입니다. 뮤테이션 함수가 받을 변수와 동일한 변수를 받습니다.
    
- 낙관적 업데이트를 수행하거나 실패 시 롤백하기 위한 컨텍스트를 반환하는 데 유용합니다.
    

#### 6. `**onSuccess: (data: TData, variables: TVariables, context: TContext) => Promise<unknown> | unknown**` (선택 사항)

- 뮤테이션이 성공했을 때 실행되는 함수입니다.
    
- 뮤테이션 결과를 인자로 받으며, Promise를 반환하면 해당 Promise가 완료될 때까지 대기합니다.
    

#### 7. `**onError: (err: TError, variables: TVariables, context?: TContext) => Promise<unknown> | unknown**` (선택 사항)

- 뮤테이션이 실패했을 때 실행되는 함수입니다.
    
- Promise를 반환하면 해당 Promise가 완료될 때까지 대기합니다.
    

#### 8. `**onSettled: (data: TData, error: TError, variables: TVariables, context?: TContext) => Promise<unknown> | unknown**` (선택 사항)

- 뮤테이션이 성공하거나 실패한 후에 실행되는 함수입니다.
    
- 성공 또는 실패 여부에 상관없이 실행됩니다.
    

#### 9. `**retry: boolean | number | (failureCount: number, error: TError) => boolean**` (기본값: `0`)

- 실패한 뮤테이션을 재시도할 횟수를 설정합니다.
    
- `false`로 설정하면 재시도하지 않으며, 숫자로 설정하면 해당 횟수만큼 재시도합니다.
    

#### 10. `**retryDelay: number | (retryAttempt: number, error: TError) => number**`

- 재시도 사이의 지연 시간을 설정합니다. 지연 시간은 밀리초 단위입니다.
    

#### 11. `**scope: { id: string }**` (선택 사항, 기본값: 고유 ID)

- 뮤테이션의 스코프를 설정합니다. 동일한 스코프 ID를 가진 뮤테이션은 직렬로 실행됩니다.
    

#### 12. `**throwOnError: undefined | boolean | (error: TError) => boolean**` (기본값: 전역 설정의 `throwOnError`)

- 뮤테이션 오류가 발생했을 때 오류를 렌더링 단계에서 throw하여 가장 가까운 오류 경계로 전파할지 설정합니다.
    

#### 13. `**meta: Record<string, unknown>**` (선택 사항)

- 뮤테이션 캐시 항목에 추가 정보를 저장합니다.
    

### `useMutation` 반환 값 설명

#### 1. `**mutate: (variables: TVariables, { onSuccess, onSettled, onError }) => void**`

- 뮤테이션을 수동으로 실행하는 함수입니다. `variables` 객체와 추가 콜백 옵션들을 전달할 수 있습니다.
    

#### 2. `**mutateAsync: (variables: TVariables, { onSuccess, onSettled, onError }) => Promise<TData>**`

- `mutate`와 비슷하지만 Promise를 반환하며, `await`할 수 있습니다.
    

#### 3. `**status: string**`

- 뮤테이션의 현재 상태 (`idle`, `pending`, `error`, `success`).
    

#### 4. `**isIdle**`**,** `**isPending**`**,** `**isSuccess**`**,** `**isError**` (boolean)

- `status`를 기준으로 파생된 여러 상태 값입니다.
    

#### 5. `**isPaused: boolean**`

- 뮤테이션이 일시 중단된 경우 `true`.
    

#### 6. `**data: undefined | unknown**`

- 마지막으로 성공적으로 해결된 뮤테이션 데이터입니다.
    

#### 7. `**error: null | TError**`

- 뮤테이션에서 발생한 오류 객체입니다.
    

#### 8. `**reset: () => void**`

- 뮤테이션 내부 상태를 초기 상태로 리셋하는 함수입니다.
    

#### 9. `**failureCount: number**`

- 뮤테이션 실패 횟수입니다. 뮤테이션이 실패할 때마다 증가하며, 성공 시 `0`으로 리셋됩니다.
    

#### 10. `**failureReason: null | TError**`

- 뮤테이션 재시도의 실패 이유입니다. 성공 시 `null`로 리셋됩니다.
    

#### 11. `**submittedAt: number**`

- 뮤테이션이 제출된 타임스탬프입니다.
    

#### 12. `**variables: undefined | TVariables**`

- `mutationFn`에 전달된 변수 객체입니다.
    

### 결론

`useMutation` 훅은 비동기 작업을 관리하고 서버에 데이터를 전송하는 작업을 간단하게 만들어주는 매우 유용한 도구입니다. 이 글에서는 `useMutation`의 다양한 옵션과 반환 값에 대해 설명했으며, 이를 통해 여러분이 뮤테이션을 더 잘 활용하고, 서버 상태를 쉽게 관리할 수 있기를 바랍니다.

React Query의 강력한 기능을 활용하여 보다 효율적이고 사용자 친화적인 애플리케이션을 개발해 보세요!
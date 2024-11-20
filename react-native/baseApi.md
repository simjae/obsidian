`baseApi`의 타입 정의와 제너릭(Generic)을 사용하는 이유를 자세히 설명하겠습니다. 이는 코드의 **유연성**과 **타입 안정성**을 동시에 확보하기 위해 사용된 설계입니다.

---

## **1. 주요 타입 정의**

### **제너릭 타입 정의**

typescript

코드 복사

`export async function baseApi<T, B = Record<string, unknown>>(   endpointOrUrl: string,   options: {     method: 'GET' | 'POST' | 'PATCH' | 'DELETE';     body?: B;     headers?: Record<string, string>;     queryParams?: Record<string, string | number | boolean>;     requireAuth?: boolean;     fullUrl?: boolean;     apiType?: 'default' | 'simulator' | 'file';   }, ): Promise<T>;`

- `T`: **응답(Response) 데이터 타입**
    - API의 응답 데이터를 타입 안정성 있게 처리하기 위해 사용됩니다.
    - 호출하는 시점에서 반환되는 데이터의 타입을 결정합니다.
- `B`: **요청(Request) 본문(body) 데이터 타입**
    - API 호출 시 서버로 전송하는 데이터의 타입을 정의합니다.
    - 기본값은 `Record<string, unknown>`로 설정되어 있으며, 호출하는 곳에서 타입을 오버라이드할 수 있습니다.

---

## **2. 타입 정의의 이유**

### **a. 제너릭으로 응답 데이터 타입 지정**

typescript

코드 복사

`const response = await baseApi<IUser[]>('/v1/users', {   method: 'GET', });`

- **문제점**: 응답 데이터가 항상 다릅니다.
    - 일부 API는 객체(`{ id: number, name: string }`), 다른 API는 배열(`[ { id: number, name: string } ]`)로 반환될 수 있습니다.
- **해결책**: 제너릭 `T`를 사용하면, 호출 시점에서 반환 타입을 명확히 지정할 수 있습니다.
    - 위 예제에서 `IUser[]` 타입을 지정했기 때문에, `response`의 타입은 `IUser[]`로 추론됩니다.

---

### **b. 제너릭으로 요청 데이터 타입 지정**

typescript

코드 복사

`const response = await baseApi<ICreateUserResponse, ICreateUserParams>(   '/v1/users',   {     method: 'POST',     body: { name: 'John Doe', email: 'john@example.com' },   }, );`

- **문제점**: 요청 본문 데이터(`body`)의 타입은 API마다 다릅니다.
    - 어떤 API는 `name`과 `email`, 또 다른 API는 `id`와 `status`를 필요로 할 수 있습니다.
- **해결책**: 제너릭 `B`를 사용하면, 호출 시점에서 요청 데이터의 타입을 지정할 수 있습니다.
    - 위 예제에서 `ICreateUserParams` 타입을 지정했기 때문에, `body`의 타입도 강제됩니다.

---

### **c. 기본값과 유연성**

#### `B` 기본값: `Record<string, unknown>`

typescript

코드 복사

`export async function baseApi<T, B = Record<string, unknown>>(   ... ): Promise<T>;`

- 기본값을 설정한 이유:
    - 요청 본문(`body`)가 항상 필요한 것은 아닙니다. 예를 들어, `GET` 요청에서는 `body`가 필요하지 않습니다.
    - `Record<string, unknown>`은 객체 형태로 동작하며, 특정 API에서 사용자가 `body` 타입을 명시하지 않더라도 유연하게 동작합니다.
    - 하지만, 특정 API의 `body`를 명확히 지정하고 싶을 때는 오버라이드할 수 있습니다.

#### 사용 예시

- `body`가 필요 없는 경우:

typescript

코드 복사

`const response = await baseApi<IUser[]>('/v1/users', {   method: 'GET', });`

- `body`가 필요한 경우:

typescript

코드 복사

`const response = await baseApi<ICreateUserResponse, ICreateUserParams>(   '/v1/users',   {     method: 'POST',     body: { name: 'John Doe', email: 'john@example.com' },   }, );`

---

### **d. 옵션 속성의 타입 정의**

#### `headers`와 `queryParams`

typescript

코드 복사

`headers?: Record<string, string>; queryParams?: Record<string, string | number | boolean>;`

- `headers`: 추가적인 HTTP 헤더를 정의할 때 사용합니다.
    - 예를 들어, `Content-Type`이나 `Authorization` 헤더를 명시적으로 추가 가능.
- `queryParams`: URL에 포함될 쿼리 문자열을 정의할 때 사용합니다.
    - `Record<string, string | number | boolean>`을 사용해 문자열, 숫자, 또는 부울 값으로 제한.
    - 예시: `queryParams: { page: 1, search: 'React' }` -> `?page=1&search=React`

---

### **e. 타입 안정성의 중요성**

- **안정성 확보**:
    - `baseApi` 호출 시 잘못된 데이터 구조를 전달하면 컴파일 시점에 오류를 잡아줍니다.
- **유지보수성 증가**:
    - API 스펙이 변경되었을 때, 관련된 타입만 업데이트하면 모든 호출부에서 오류를 검출할 수 있습니다.

---

## **3. 제너릭 설계의 장점**

1. **재사용성**:  
    하나의 `baseApi` 함수로 다양한 API 호출을 처리할 수 있습니다.
    
2. **타입 추론**:  
    호출부에서 반환되는 데이터의 타입과 요청 데이터의 타입을 명시적으로 지정 가능.
    
3. **유연성**:  
    기본값(`Record<string, unknown>`)을 활용해 필요하지 않은 경우에도 유연하게 동작.
    
4. **타입 안정성**:  
    요청 데이터와 응답 데이터를 컴파일 시점에 체크하여 런타임 오류를 최소화.
    

---

## **4. 예제**

### **a. GET 요청**

typescript

코드 복사

`const response = await baseApi<IUser[]>('/v1/users', {   method: 'GET', });`

- 응답 데이터가 `IUser[]`로 타입이 지정됩니다.

---

### **b. POST 요청**

typescript

코드 복사

`interface ICreateUserParams {   name: string;   email: string; }  interface ICreateUserResponse {   id: number;   name: string;   email: string; }  const response = await baseApi<ICreateUserResponse, ICreateUserParams>(   '/v1/users',   {     method: 'POST',     body: { name: 'John Doe', email: 'john@example.com' },   }, );`

- 요청 본문은 `ICreateUserParams` 타입으로 제한되며, 응답 데이터는 `ICreateUserResponse`로 타입이 지정됩니다.

---

### **c. 쿼리 매개변수 사용**

typescript

코드 복사

`const response = await baseApi<IUser[]>('/v1/users/search', {   method: 'GET',   queryParams: { q: 'React' }, });`

- 쿼리 매개변수로 `q=React`가 URL에 추가됩니다.

---

### **결론**

`baseApi`의 타입 설계는 유연성과 타입 안정성을 모두 고려한 디자인입니다. 제너릭을 통해 호출부에서 요청 데이터와 응답 데이터를 명확히 지정할 수 있으며, 타입 추론을 활용하여 코드의 가독성과 유지보수성을 크게 향상시킵니다. 이러한 설계는 대규모 프로젝트에서 특히 유용하며, 변경된 API 스펙에 대응하기 쉽습니다.
# http method DELETE에 body 담아보내기
- id를 이용해 여러 건 삭제
- Query string으로 보낼 수도 있지만 url이 지저분해지고 많이 길어질 수 있음.
- 서버에서 `@RequestBody`로 받기로 한다.
- `Axios`를 사용한다.

## 🔎 방법 찾기
- axios.delete()는 두번째 파라미터로 config를 받는다.
```typescript
delete<T = any, R = AxiosResponse<T>>(url: string, config?: AxiosRequestConfig): Promise<R>;
```
- 그리고 `interface AxiosRequestConfig`에는 `data`가 있음.
- 여기에 request body를 설정할 수 있다.
```typescript
export interface AxiosRequestConfig {
    url?: string;
    method?: Method;
    baseURL?: string;
    transformRequest?: AxiosTransformer | AxiosTransformer[];
    transformResponse?: AxiosTransformer | AxiosTransformer[];
    headers?: any;
    params?: any;
    paramsSerializer?: (params: any) => string;
    data?: any;
    // ...
}
```

## 🤹‍♀️ 예제
```jsx
export const Axios = axios.create();

const payload = {
	"ids": [1, 2, 3]
}

// 기존 query string으로 보내는 방식
function remove(url, payload) {
    return Axios.delete(url, { params: payload });
}

// body 보내기
function multiRemove(url, payload) {
    return Axios.delete(url, { data: payload });
}
```

## ❓ 나의 문제 상황
- 그런데 `data`가 계속 `undefined`로 보내짐.
- 코드를 살피니 `axios.interceptors`가 사용되고 있었음.
```jsx
Axios.interceptors.request.use(
    (config) => {
        config.headers['Authorization'] = `Bearer ${token}`;
	    
        return config;
    }
);
```
- `axios.interceptors`는 요청 전 혹은 응답 후 가로채서 처리를 할 수 있게 해준다.
- `config.data`가 세팅되지 않고 있었음. 세팅함.

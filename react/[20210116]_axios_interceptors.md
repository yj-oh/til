# axios.interceptors
- `then`, `catch` 처리 전 요청, 응답을 가로챌 수 있음.
- 공통적인 header 세팅이나 request, response, error 공통 처리 등에 사용하면 좋을 듯.

## 추가
```jsx
// 요청 인터셉터
axios.interceptors.request.use(
    function (config) {
        // 요청을 보내기 전 수행할 것
        // ...
        return config;
    },
    function (error) {
        // 오류 요청을 보내기 전 수행할 것
        // ...
        return Promise.reject(error);
    }
);

// 응답 인터셉터
axios.interceptors.response.use(
    function (response) {
        // 응답 데이터를 가공
        // http status가 200일 때 응답 직전 수행할 것
        // .then()으로 이어짐
        // ...
        return response;
    },
    function (error) {
        // 오류 응답을 처리
        // .catch()로 이어짐
        // ...
        return Promise.reject(error);
    }
);
```

## 제거
```jsx
const myInterceptor = axios.interceptors.request.use(function () { /*...*/ });
axios.interceptors.request.eject(myInterceptor);
```

## Custom axios instance에 적용
```jsx
const instance = axios.create();
instance.interceptors.request.use(function () { /*...*/ });
```

##### * Reference : [Axios 러닝 가이드 - 인터셉터](https://xn--xy1bk56a.run/axios/guide/interceptors.html)

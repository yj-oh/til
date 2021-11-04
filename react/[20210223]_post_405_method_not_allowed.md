# 배포하며 겪었던 문제 - POST 405 (Method Not Allowed)

## 상황
- `create-react-app`으로 생성한 리액트 프로젝트
- API domain : https://api.com/
- Front domain : https://web.com/
- 서버쪽 CORS 설정하지 않고 간편하게 도메인 문제를 해결하기 위해 `package.json`에 [프록시 설정함](https://react.vlpt.us/redux-middleware/09-cors-and-proxy.html).
    ```json
    {
      "proxy": "https://api.com/"
    }
    ```
- 로컬에서 문제없이 동작.
- 자동 배포 세팅되어있다.
- 빌드 잘 되고 배포 잘 되었다.
- 사이트 들어가서 post 요청 보내 로그인 하려고 하니.

## POST https://web.com/login 405 (Method Not Allowed)
- [nginx post 405 not allow 문제](https://www.dummy.pe.kr/1739)
- [stackoverflow - POST request not allowed - 405 Not Allowed - nginx, even with headers included](https://stackoverflow.com/questions/24415376/post-request-not-allowed-405-not-allowed-nginx-even-with-headers-included)
- static 페이지에서 post 요청이 안 돼? 외않되?
- 아무튼 위 링크들을 보고 nginx conf에 `error_page 405 = $uri;`를 추가함.
```
server {
    listen          80;
    server_name     web.com;

    location / {
        root   /home/ec2-user/project/build;
        index  index.html;
    }

    # To allow POST on static pages
    error_page 405 = $uri;
}
```
- 정상적으로 로그인이 되고 메인 페이지로 넘어간다.
- 하지만 뭔가 야매로 처리한 느낌을 지울 수 없음.
- 그리고 가장 중요한 문제는 AWS는 위와 같은 방법으로 해결했지만 Azure는 nginx 설정 등이 없다고 함.
- 다른 방법을 찾아야 했음.

## proxy 설정을 버리자
- `package.json`의 proxy 설정을 삭제하고 axios.create() 할 때 baseURL 설정함.
```jsx
import axios from 'axios';

export const Axios = axios.create({
    baseURL: 'https://api.com/',
});
```
- 그리고 드디어 만난 CORS error
```text
🚨 Access to fetch at 'https://api.com' from origin 'https://web.com' 
has been blocked by CORS policy: No 'Access-Control-Allow-Origin' 
header is present on the requested resource. If an opaque response 
serves your needs, set the request's mode to 'no-cors' to fetch 
the resource with CORS disabled.
```

## 결국 CORS 설정
- Origin, preflight... what?
- 열공
  - [CORS에 대한 이해](../web/[20210221]_cors.md)
  - [Spring Boot - CORS 설정하기](../spring/[20210222]_spring_boot_cors.md)
- 처음에 Origin이 뭔지 CORS 관련 설정을 어디에 해야하는지 헷갈렸다.
  - Origin은 https://web.com
  - 브라우저가 알아서 보내주므로 따로 값을 세팅하거나 할 필요 없다.
  - 서버측에 허용할 Origin - https://web.com 설정.
  - 서버가 허용할 Origin 정보를 response header `Access-Control-Allow-Origin`에 담아
    보내주면 브라우저가 둘을 비교해 CORS 정책 적합성 여부를 판단한다.
- 겁 먹었는데 공부, 정리하고 보니 생각만큼 복잡하지는 않았음. 설정 코드도 간단하고.
- 겁 먹지 말자.

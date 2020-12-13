# Create React App 환경변수
- `TIL` \[20201105\] : [API Key 숨기기]([20201105]_hide_api_key.md)
- 위에서 환경변수에 대해 살짝 맛봤는데 조금 더 자세히 정리.

---

## 환경변수
- `process.env`에 정의됨.
- build time에 세팅됨.
- 사용자 환경변수 선언 시 변수 앞에 `REACT_APP_`
- 기본 환경 변수 `NODE_ENV`에 환경에 대한 값이 담겨있음.
    - 각각의 환경별로 다른 변수를 선언할 수 있음.
        - `development`
        - `test`
        - `production`
- 변경하면 서버 재시작 해야 함

## 선언
- root 폴더 아래에 `.env` 파일 생성
```text
REACT_APP_VALUE = 'value'
```

### `.env` 외에 사용할 수 있는 파일
| 사용할 수 있는 파일명 | 설명 |
| --- | --- |
`.env` | Default
`.env.local` | Local overrides. This file is loaded for all environments except test.
`.env.development`, `.env.test`, `.env.production` | Environment-specific settings.
`.env.development.local`, `.env.test.local`, `.env.production.local` | Local overrides of environment-specific settings.

### 각 파일 별 우선 순위
| 명령어 | 파일 우선 순위 |
| --- | --- |
| npm start | `.env.development.local` > `.env.local` > `.env.development` > `.env`
| npm run build | `.env.production.local` > `.env.local` > `.env.production` > `.env`
| npm test | `.env.test.local` > `.env.test` > `.env` (note `.env.local` is missing)

## 사용
#### JSX
```jsx
<div>{process.env.REACT_APP_VALUE}</div>
```
#### HTML
```html
<div>%REACT_APP_VALUE%</div>
```
#### JS
```javascript
const baseURL = process.env.NODE_ENV === 'production' ? '/api' : '';
```

##### * Reference : https://create-react-app.dev/docs/adding-custom-environment-variables/

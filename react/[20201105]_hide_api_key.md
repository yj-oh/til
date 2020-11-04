# API Key 숨기기
- root 경로 (src, package.json 등이 있는)에 `.env` 생성

### .env 파일 생성
- 키 이름 앞에 `REACT_APP_` 추가
   - `REACT_APP_` : create-react-app이 변수를 식별하는 데에 사용
```ignore
REACT_APP_KAKAO_REST_API_KEY={키값}
```

### .gitignore에 .env 추가
```ignore
# api key
.env
```

### 접근
```javascript
const KAKAO_API_KEY = process.env.REACT_APP_KAKAO_REST_API_KEY;
```

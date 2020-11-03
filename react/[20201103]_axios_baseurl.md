# axios baseURL
- API 요청시 중복되는 패스를 기본 URL로 설정하여 사용할 수 있음

### 예제
#### package.json
- HOST 설정은 아래와 같이 되어 있다.
```json
{
  "proxy": "http://localhost:8080"
}
```

- api 호출 url은 다음과 같다.
```text
[GET]  /api/books
[GET]  /api/books/{id}
[POST] /api/books
[PUT]  /api/books/{id}
[GET]  /api/stores
[POST] /api/stores
```

#### client.js
- `/api`를 기본 URL로 등록
```javascript
import axios from 'axios';

const client = axios.create({
    baseURL: '/api',
});

export default client;
```

#### book.js
```javascript
import client from './client';

export const getList = () => API.get(`/books`);
export const getBook = id => API.get(`/books/${id}`);
// ...
```

- → 그럼 api 호출 시 http://localhost:8080/api/books로

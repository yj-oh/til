# RESTful API Design Best practices
## 단수보다 복수
#### 예제
- 사용자 목록 조회
```
/user   // [ X ]
/users  // [ O ]
```

- 사용자 단건 조회
```
/user/:id   // [ X ]
/users/:id  // [ O ]
```
# PUT vs PATCH

## PUT
- entity 전달
- entity에 일부 누락된 값이 있으면 해당 값은 null 또는 초기화 된다.
```json
// 기존 데이터
{
    "name" : "jun",
    "sex" : "male",
    "team" : "A"
}

// PUT request
{
    "name" : "jun",
    "sex" : "male",
    "team" : "B"    // 수정
}

// Result
{
    "name" : "jun",
    "sex" : "male",
    "team" : "B"
}
```

- entity 일부 값만 보낼 경우
```json
// 기존 데이터
{
    "name" : "jun",
    "sex" : "male",
    "team" : "A"
}

// PUT request
{
    "team" : "B"    // 수정
}

// result
{
    "name" : null,  // 초기화
    "sex" : null,   // 초기화
    "team" : "B"    // 수정
}
```

## PATCH
- 변경하고자 하는 속성만 전달.
```json
// 기존 데이터
{
    "name" : "jun",
    "sex" : "male",
    "team" : "A"
}

// PATCH request
{
    "team" : "B"    // 수정
}

// Result
{
    "name" : "jun",
    "sex" : "male",
    "team" : "B"
}
```

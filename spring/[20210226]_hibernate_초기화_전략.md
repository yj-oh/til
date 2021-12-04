# Hibernate 초기화 전략
- `spring.jpa.hibernate.ddl-auto`

## application.yml
```yaml
server.port: 8080

spring:
  jpa:
    hibernate:
      ddl-auto: # property values
```

## The standard Hibernate property values
| Value       | Description                                       |
|-------------|---------------------------------------------------|
| none        | 아무 동작도 하지 않음                                      |
| create      | drop 후 생성                                         |
| update      | 변경된 스키마 적용                                        |
| create-drop | 시작할 때 생성, 종료할 때 drop                              |
| validate    | 테이블과 컬럼의 존재 여부만 확인하고, 그렇지 않으면 throws an exception |

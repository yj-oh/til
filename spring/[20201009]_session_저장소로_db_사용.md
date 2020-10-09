# session 저장소로 DB 사용하기
- 로그인 요청마다 DB IO 발생하므로 성능상의 문제 발생 가능
- 규모가 작고 로그인 요청이 많이 없는 서비스에서 주로 사용

#### build.gradle
- 의존성 추가
```groovy
implementation 'org.springframework.session:spring-session-jdbc'
```

#### application.yml
```yaml
spring:
  session:
    store-type: jdbc
    jdbc:
      initialize-schema: always
      table-name: spring_session
```
- 테이블 `SPRING_SESSION`, `SRPING_SESSION_ATTRIBUTES` 생성

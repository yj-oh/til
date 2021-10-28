# Spring Boot 환경별 설정(YAML) - 2.4에 달라진 점
- 새로운 회사에서 새 프로젝트를 돌려보면서 `application.yml`을 살피는데, 
  기존에 쓰던 방식과 다르게 작성되어 있어서 뭔가 하고 찾아보게 됐다.

---

## Multi-document YAML Ordering
버전 | 내용
--- | ---
2.3 이하 | profile activation order 에 따라 문서 추가
2.4 이상 | 선언된 순서 대로 작동함. 나중에 선언된 애들은 먼저 선언된 애들을 덮어씀.
```yaml
test: "value"
---
test: "overridden-value"
```

## Profile Specific External Configuration
버전 | 내용
--- | ---
2.3 이하 | jar 외부의 application.properties 파일은 jar 내부의 application-<profile>.properties 파일을 덮어쓰지 않음.
2.4 이상 | 모든 외부 파일이 항상 패키지 파일을 재정의함.

## Profile Specific Documents
버전 | 내용
--- | ---
2.3 이하 | `spring.profiles`
2.4 이상 | `spring.config.activate.on-profile` <br/> (`spring.profiles` deprecated)

- 2.3 이하
```yaml
spring:
  profiles: "prod"
secret: "production-password"
```
- 2.4 이상
```yaml
spring:
  config:
    activate:
      on-profile: "prod"
secret: "production-password"
```

## Profile Activation
- `spring.profiles.active` 사용
```yaml
spring:
  profiles:
    active: "prod"
```
- `spring.config.active.on-profile` 프로퍼티가 있는 문서에서
  `spring.profiles.include`, `spring.profiles.active` 사용할 수 없음.
  - non profile-specific documents 에서만 사용 가능.
- 아래 불가.
```yaml
spring:
  config:
    activate:
      on-profile: "prod"
  profiles:
    include: "metrics"
```
- on-profile conditions 은 한 번만 평가되기 때문.
- 이 제한이 없으면 평가 시점에 따라 다른 결과가 나올 수 있음.

## Profile Groups
버전 | 내용
--- | ---
2.3 이하 | 종종 `spring.profiles` + `spring.profiles.include`로 active profiles 확장.
2.4 이상 | `Profile Groups`

- 2.3 이하
```yaml
spring.profiles: "debug"
spring.profiles.include: "debugdb,debugcloud"
```
- 2.4 이상에서 표현하면 아래와 같지만, 위에서 말한 이유로 유효하지 않다.
  - "`spring.config.active.on-profile` 프로퍼티가 있는 문서에서 `spring.profiles.include` 사용 불가"
```yaml
spring:
  config:
    activate:
      on-profile: "debug"
  profiles:
    include: "debugdb,debugcloud"
```

- 그래서 `Profile Groups` 등장
```text
if you see profile 'x', also activate profiles 'y' & 'z'
```
```yaml
spring:
  profiles:
    group:
      debug: "debugdb,debugcloud"
```
- 역시 profile-specific documents, `spring.config.activate.on-profile` 프로퍼티가 있는 문서에서 사용 불가

## Migration Example
- 2.3 이하
```yaml
spring.application.name: "customers"
---
spring.profiles: "production"
spring.profiles.include: "mysql,rabbitmq"
---
spring:
  profiles: "mysql"
  datasource:
    url: "jdbc:mysql://localhost/test"
    username: "dbuser"
    password: "dbpass"
---
spring:
  profiles: "rabbitmq"
  rabbitmq:
    host: "localhost"
    port: 5672
    username: "admin"
    password: "secret"
```
- 2.4 이상
```yaml
spring:
  application:
    name: "customers"
  profiles:
    group:
      "production": "mysql,rabbitmq"
---
spring:
  config:
    activate:
      on-profile: "mysql"
  datasource:
    url: "jdbc:mysql://localhost/test"
    username: "dbuser"
    password: "dbpass"
---
spring:
config:
  activate:
    on-profile: "rabbitmq"
  rabbitmq:
    host: "localhost"
    port: 5672
    username: "admin"
    password: "secret"
```

## Using Legacy Processing
```yaml
spring.config.use-legacy-processing=true

# any other properties
```
※ 단일 `application.properties`, `application.yml`만 사용하는 경우,
`spring.profiles<.*>` 사용하지 않는 경우에는 특별한 migrate 필요 없음.

##### * References
- [Config file processing in Spring Boot 2.4](https://spring.io/blog/2020/08/14/config-file-processing-in-spring-boot-2-4)
- [Spring Boot Config Data Migration Guide](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-Config-Data-Migration-Guide)

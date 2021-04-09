# Spring Boot - H2 innoDB Error
- org.h2.jdbc.JdbcSQLSyntaxErrorException
```
org.h2.jdbc.JdbcSQLSyntaxErrorException: Syntax error in SQL statement
"CREATE TABLE USER (
    ID BIGINT NOT NULL AUTO_INCREMENT,
    NAME VARCHAR(255) NOT NULL,
) ENGINE=[*]INNODB"; expected "identifier";
```
- Spring Boot `2.4.4`
- h2 `1.4.199`

## application.yml
- `spring.datasource.url`에 `;MODE=MYSQL` 추가
```yaml
spring:
  h2:
    console:
      enabled: true
  datasource:
    driver-class-name: org.h2.Driver
    url: jdbc:h2:mem:test
```

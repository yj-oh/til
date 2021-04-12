# @DataJpaTest JdbcSQLSyntaxErrorException: Table not found...

## 상황
- H2 in-memory DB 사용하여 로컬에서 작업 중.
- Repository test - `@DataJpaTest` 사용
```java
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.orm.jpa.DataJpaTest;

@DataJpaTest
public class BookRepositoryTest {
	
    @Autowired
    private BookRepository BookRepository;

    @Test
    void save() {
    	// ...
    }
}
```

- 에러가 난다.
```text
Caused by: org.h2.jdbc.JdbcSQLSyntaxErrorException: 
Table "BOOK" not found; SQL statement:
```

## 해결 방법 검색
```text
In-memory embedded databases generally work well for tests, since they are 
fast and do not require any installation. If, however, you prefer to run tests 
against a real database you can use the @AutoConfigureTestDatabase annotation, 
as shown in the following example:
```
```java
@DataJpaTest
@AutoConfigureTestDatabase(replace=Replace.NONE)
class ExampleRepositoryTests {
    // ...
}
```
- 설정 파일에 명시된 실제 DB로 테스트를 하려면 `@AutoConfigureTestDatabase` 추가해준다.
* Reference : https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#boot-features-testing-spring-boot-applications-testing-autoconfigured-jpa-test

## 해결
```java
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.jdbc.AutoConfigureTestDatabase;
import org.springframework.boot.test.autoconfigure.orm.jpa.DataJpaTest;

@AutoConfigureTestDatabase(replace= AutoConfigureTestDatabase.Replace.NONE)
@DataJpaTest
public class BookRepositoryTest {
	
    @Autowired
    private BookRepository BookRepository;

    @Test
    void save() {
    	// ...
    }
}
```

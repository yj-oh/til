# Entity 기본 키 매핑 - @GeneratedValue
- IDENTITY
- SEQUENCE
- AUTO

## IDENTITY
```java
@GeneratedValue(stratege = GenerationType.IDENTITY)
```
- 기본 키 생성을 데이터베이스에 위임
- 주로 MySQL, PostgreSQL, SQL Server, DB2에서 사용
   - MySQL `auto_increment`
- 데이터를 입력하고나서 키값을 알 수 있음
   - 기본 키 값을 가져오기 위해 추가로 조회함

## SEQUENCE
- `예제 코드` : ⌜자바 ORM 표준 JPA 프로그래밍⌟ - 김영한 저 (136p)
```java
@Entity
@SequenceGenerator(
    name = "BOOK_SEQ_GENERATOR",
    sequenceName = "BOOK_SEQ",
    initialValue = 1, allocationSize = 1
)
public class Book {
    @Id
    @GeneratedValue(stratege = GenerationType.SEQUENCE, generator = "BOOK_SEQ_GENERATOR")
    private Long id;
}
```
- sequence : 유일한 값을 순서대로 생성하는 db object
- 주로 Oracle, PostgreSQL, DB2, H2에서 사용
- ⚠️ allocationSize의 기본값은 50 (최적화 때문)
   - `참고` : ⌜자바 ORM 표준 JPA 프로그래밍⌟ - 김영한 저 (138p)

## AUTO
```java
@GeneratedValue(stratege = GenerationType.AUTO)
```
- DB 방언에 따라 IDENTITY, SEQUENCE, TABLE 전략 중 하나 선택
- MySQL → `IDENTITY`
- Oracle → `SEQUENCE`
- DB를 바꿔도 코드 수정하지 않아도 되는 장점
   - 초기 개발 시 유용

##### * Reference : ⌜자바 ORM 표준 JPA 프로그래밍⌟ - 김영한 저

### 👉 2020.10.15 추가
- MySQL + AUTO 전략을 선택하면 hibernate가 `TABLE` 전략을 사용하는 이슈가 있었다.
   - Spring Boot 2.0 + hibernate 5
- 자세한 내용은 다음 참고 : [@GeneratedValue - auto_increment 문제](orm/[20201015]_generatedvalue_auto_increment.md)

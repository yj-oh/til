# Querydsl Projection

### Projection
- select절에 조회 대상 지정

### 4가지 방법
1. Projections.bean
2. Projections.fields
3. Projections.constructor
4. @QueryProjection

## Projections.bean
- setter 이용
- 쿼리 결과와 매핑할 프로퍼티 이름이 같아야 함
   - 다를 경우 as() 이용하여 별칭 부여
   
```java
import com.querydsl.core.types.Projections;
import com.querydsl.jpa.JPQLQuery;
import org.springframework.data.jpa.repository.support.QuerydslRepositorySupport;

import javax.print.MultiDocPrintService;import java.util.List;

import static com.java.example.book.QBook.book;
import static com.java.example.user.QUser.user;

public class BookRepositoryImpl extends QuerydslRepositorySupport implements BookRepositoryCustom {
    public BookRepositoryImpl() { super(Book.class); }

    @Override
    public List<BookDto> find(Long id) {
        JPQLQuery<BookDto> query = from(book)
                .leftJoin(user).on(book.user.id.eq(user.id))
                .where(book.id.eq(id))
                .select(Projections.bean(BookDto.class,
                        book,
                        user.id.as("userid"),  // 쿼리 결과와 매핑할 프로퍼티 이름이 다를 경우
                        user.name
                ));
        // ...
    }
}
```

## Projections.fields
- 필드 직접 접근
- 필드가 private여도 동작
- setter가 없어도 동작

```java
// ...
@Override
public List<BookDto> find(Long id) {
    JPQLQuery<BookDto> query = from(book)
            .leftJoin(user).on(book.user.id.eq(user.id))
            .where(book.id.eq(id))
            .select(Projections.fields(BookDto.class,
                    book,
                    user.id.as("userid"),
                    user.name
            ));
    // ...
}
```

## Projections.constructor
- 생성자 이용
- 고로 파라미터 순서가 일치해야 함

```java
// ...
@Override
public List<BookDto> find(Long id) {
    JPQLQuery<BookDto> query = from(book)
            .leftJoin(user).on(book.user.id.eq(user.id))
            .where(book.id.eq(id))
            .select(Projections.constructor(BookDto.class,
                    book,
                    user.id.as("userid"),
                    user.name
            ));
    // ...
}
```

## @QueryProjection
- Q 타입(query type) 객체의 생성자를 이용
- 해당 객체 생성자에 `@QueryProjection` annotation을 달아준다

```java
// BookDto.java
public class BookDto {
    private final Long id;
    private final String title;
    // ...

    @QueryProjection
    public BookDto(Book book, Long userid, String name) {
        this.id = book.getId();
        // ...
    }
}
```
```java
// ...
@Override
public List<BookDto> find(Long id) {
    JPQLQuery<BookDto> query = from(book)
            .leftJoin(user).on(book.user.id.eq(user.id))
            .where(book.id.eq(id))
            .select(new QBookDto(
                    book,
                    user.id.as("userid"),
                    user.name
            ));
    // ...
}
```

##### * References
- ⌜자바 ORM 표준 JPA 프로그래밍⌟ - 김영한 저
- [Querydsl Projection 방법 소개 및 선호하는 패턴 정리](https://cheese10yun.github.io/querydsl-projections/)
- [🙈[Spring JPA] 방명록 애플리케이션 (4) - QueryDSL로 변경하기🐵](https://victorydntmd.tistory.com/206)

# Querydsl case문
- 로직적인 부분을 repository에서 처리하는 게 찝찝하긴 하지만 알아는 두자.

### 예제
#### BookRepositoryImpl.java
```java
public class BookRepositoryImpl extends QuerydslRepositorySupport implements BookRepositoryCustom {
    public BookRepositoryImpl() { 
        super(Book.class); 
    }

    @Override
    public List<BookDto> find(int edition) {
        return from(book)
                .leftJoin(bookmark)
                    .on(book.id.eq(bookmark.bookId))
                .where(book.edition.eq(edition))
                .select(new QBookDto(
                        book.id,
                        book.title,
                        bookmark.id,
                        new CaseBuilder()
                                .when(book.deletedAt.isNull())
                                .then("판매")
                                .otherwise("절판")
                ))
                .fetch();
    }
}
```

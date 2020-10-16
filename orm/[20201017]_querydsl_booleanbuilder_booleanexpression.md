# Querydsl BooleanBuilder, BooleanExpression

## 👉 BooleanBuilder
- 조건에 따라 where절 조건문 생성

### 예제
#### BookRepositoryImpl.java
```java
import com.querydsl.core.BooleanBuilder;
import com.study.jpa.dto.BookDto;
import com.study.jpa.dto.QBookDto;
import com.study.jpa.entity.Book;
import org.springframework.data.jpa.repository.support.QuerydslRepositorySupport;

import java.util.List;

import static com.study.jpa.entity.QBook.book;
import static com.study.jpa.entity.QBookmark.bookmark;

public class BookRepositoryImpl extends QuerydslRepositorySupport implements BookRepositoryCustom {
    public BookRepositoryImpl() { 
        super(Book.class); 
    }

    @Override
    public List<BookDto> find(int edition, boolean isBookmark, boolean isDeleted) {
        
        BooleanBuilder builder = new BooleanBuilder();
        // 필터링 - 북마크
        if(isBookmark) {
            builder.and(book.bookmark.isNotNull());
        }
        // 절판 여부
        if(isDeleted) {
            builder.and(book.deletedAt.isNotNull());
        }

        return from(book)
                .leftJoin(bookmark)
                    .on(book.id.eq(bookmark.bookId))
                .where(builder)
                .where(book.edition.eq(edition))
                .select(new QBookDto(
                        book.id,
                        book.title,
                        bookmark.id
                ))
                .fetch();
    }
}
```

### 문제점
- 쿼리를 한눈에 파악하기 어렵다.

## 👉 BooleanExpression

### 개선 예제
```java
import com.querydsl.core.types.dsl.BooleanExpression;
import com.study.jpa.dto.BookDto;
import com.study.jpa.dto.QBookDto;
import com.study.jpa.entity.Book;
import org.springframework.data.jpa.repository.support.QuerydslRepositorySupport;

import java.util.List;

import static com.study.jpa.entity.QBook.book;
import static com.study.jpa.entity.QBookmark.bookmark;

public class BookRepositoryImpl extends QuerydslRepositorySupport implements BookRepositoryCustom {
    public BookRepositoryImpl() { 
        super(Book.class); 
    }

    @Override
    public List<BookDto> find(int edition, boolean isBookmark, boolean isDeleted) {
        
        BooleanBuilder builder = new BooleanBuilder();
        // 필터링 - 북마크
        if(isBookmark) {
            builder.and(book.bookmark.isNotNull());
        }
        // 절판 여부
        if(isDeleted) {
            builder.and(book.deletedAt.isNotNull());
        }

        return from(book)
                .leftJoin(bookmark)
                    .on(book.id.eq(bookmark.bookId))
                //.where(builder)
                .where(book.edition.eq(edition))
                .where(isBookmark(isBookmark))
                .where(isDeleted(isDeleted))
                .select(new QBookDto(
                        book.id,
                        book.title,
                        bookmark.id
                ))
                .fetch();
    }

    private BooleanExpression isBookmark(boolean isBookmark) {
        if(isBookmark) {
            return book.bookmark.isNotNull();
        }
        return null;
    }

    private BooleanExpression isDeleted(boolean isDeleted) {
        if(isDeleted) {
            return book.deletedAt.isNotNull();
        }
        return null;
    }
}
```
* *개선 내용 참고 : [기억보단 기록을 - \[Querydsl\] 다이나믹 쿼리 사용하기](https://jojoldu.tistory.com/394)*

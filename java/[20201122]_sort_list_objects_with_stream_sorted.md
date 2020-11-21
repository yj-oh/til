# Sort List Objects with stream.sorted()
```java
import java.time.ZonedDateTime;
import java.util.Arrays;
import java.util.Comparator;
import java.util.List;
import java.util.stream.Collectors;

public class Del {
    public static void main(String[] args) {
        List<Book> list = Arrays.asList(
            new Book(1L, "노인과 바다", ZonedDateTime.now().minusMonths(5)),
            new Book(2L, "쇼펜하우어 ", ZonedDateTime.now().minusMonths(4)),
            new Book(3L, "존재와 시간", ZonedDateTime.now().minusMonths(3)),
            new Book(4L, "깊 은 슬 픔", ZonedDateTime.now().minusMonths(2)),
            new Book(5L, "순수이성비판", ZonedDateTime.now().minusMonths(1))
        );

        List<Book> sortedList = list.stream()
                .sorted(Comparator.comparing(Book::getTitle))
                .collect(Collectors.toList());
        sortedList.forEach(System.out::println);

        System.out.println("==========================================================");

        sortedList = list.stream()
                .sorted(Comparator.comparing(Book::getPublishedAt))
                .collect(Collectors.toList());
        sortedList.forEach(System.out::println);
    }

    static class Book {
    	private Long id;
    	private String title;
    	private ZonedDateTime publishedAt;

    	public Book(Long id, String title, ZonedDateTime publishedAt) {
            this.id = id;
            this.title = title;
            this.publishedAt = publishedAt;
    	}

    	public Long getId() {
            return id;
    	}
    	public String getTitle() {
            return title;
    	}
    	public ZonedDateTime getPublishedAt() {
            return publishedAt;
    	}
    	@Override
    	public String toString() {
            return "{ id : " + id + ", title : " + title + ", publishedAt : " + publishedAt + " }";
    	}
    }
}
```

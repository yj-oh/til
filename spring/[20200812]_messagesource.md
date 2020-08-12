# MessageSource
- 국제화(i18n)를 제공하는 interface
- 기본 형태 : key=value

### src/main/resources
##### messages.properties    : 기본 메시지
```properties
book.title=hello {0}
```
##### messages_ko.properties : 한글
```properties
book.title=안녕 {0}
```
##### messages_en.properties : 영어
```properties
book.title=hello {0}
```

### 사용하기
```java
@RequiredArgsConstructor
@Service
public class BookService {
    
    private final MessageSource messageSource;

    public void get() {
        String krTitle = messageSource.getMessage("book.title", new String[]{"JAVA"}, Locale.KOREA);
        String enTitle = messageSource.getMessage("book.title", new String[]{"JAVA"}, Locale.US);

        System.out.println(krTitle);  // 안녕 JAVA
        System.out.println(enTitle);  // hello JAVA
    }   
}
```

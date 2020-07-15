# Constructor Injection with Lombok

## @AllArgsConstructor
- 클래스의 모든 필드에 대한 생성자

## @NoArgsConstructor
- 빈 생성자

## @RequiredArgsConstructor
- Generates a constructor with required arguments.
- Required arguments are uninitialized final fields and fields with constraints such as @NonNull.
   - 필수 arguments? 초기화 되지 않은 `final` 필드나 `@NonNull` 필드
- Default access modifier is public.
   - private constructor
     ```java
     @RequiredArgsConstructor(access = AccessLevel.PRIVATE)
     ```
- with Lombok
```java
@RequiredArgsConstructor
@Service
public class BookService {
    private final BookRepository bookRepository;
    private Long id;
    private final String bookStoreName = "YJ";
    private static string address = "Seoul";
    @NonNull
    private int employee = 1;
}
```
- Vanilla Java
```java
public class BookService {
    private final UserRepository userRepository;  // [ O ] 초기화 되지 않은 final field
    private Long id;                              // [ X ] final 아님, @NonNull 아님
    private final String bookStoreName = "YJ";    // [ X ] 초기화 된 final
    private static String address = "Seoul";      // [ X ] static
    @NonNull private int employee = 1;            // [ X ] 초기화 된 @NonNull

    public BookService(final UserRepository userRepository) { 
        this.userRepository = userRepository;
    }
}
```

* References
   - https://projectlombok.org/features/constructor
   - https://javabydeveloper.com/lombok-requiredargsconstructor-examples/
   - https://www.baeldung.com/spring-injection-lombok

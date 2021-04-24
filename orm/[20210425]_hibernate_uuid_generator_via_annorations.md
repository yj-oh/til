# Hibernate UUID Generator via annotations
- @GeneratedValue
- @GenericGenerator
```java
import org.hibernate.annotations.Type;
import javax.persistence.*;
import org.hibernate.annotations.GenericGenerator;

@Entity
public class User {
    @Id
    @Type(type = "uuid-char")
    @GeneratedValue(generator = "uuid2")
    @GenericGenerator(name = "uuid2", strategy = "uuid2")
    @Column(length = 36)
    private UUID id;
}
```

## uuid? uuid2?
- uuid
```text
ff808081790f62e701790f6305fa0000
```
- uuid2
```text
3b57020a-6dc3-4ad3-a425-e2b7e9430c1a
```

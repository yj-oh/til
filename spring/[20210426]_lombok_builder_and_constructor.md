# Lombok @Builder and constructor
- Lombok `@Builder` 사용할 때 자주 만나는 에러가 있다.
- 해결 방법은 아는데 왜 그런지 생각해본 적이 없는 듯하여 정리한다.
  
## 🤔 상황
- 에러는, 정확히 말하면 `@Builder`와 `모든 필드를 가지지 않은 생성자`를 함께 사용할 때다.
```java
import lombok.Builder;
import lombok.NoArgsConstructor;
import javax.persistence.Entity;

@Builder
@NoArgsConstructor
@Entity
public class User {
    // ...
}
```
```text
error: constructor User in class User cannot be applied to given types;
@Builder
^
  required: no arguments
  found: ...
  reason: actual and formal argument lists differ in length
```

## 💭 원인
```text
Finally, applying @Builder to a class is as if you added 
@AllArgsConstructor(access = AccessLevel.PACKAGE) to the class and applied 
the @Builder annotation to this all-args-constructor. 
This only works if you haven't written any explicit constructors yourself.
If you do have an explicit constructor, 
put the @Builder annotation on the constructor instead of on the class.
```
- _참고 : https://projectlombok.org/features/Builder_
  
### 정리
- 클래스에 `@Builder`를 적용한 것은, 
  클래스에 `@AllArgsConstructor(access = AccessLevel.PACKAGE)`를 적용하고
  `모든 필드를 가진 생성자`에 `@Builder`를 적용한 것과 같다.
- 그러나 다른 생성자가 있을 경우에는 적용되지 않음.
- 고로 다른 생성자를 사용할 때는 클래스에 `@Builder` 적용하지 말고 그 생성자에 적용해라.

## 💡 해결

### 방법 1. 클래스가 아닌, 생성자에 @Builder 적용
```java
import lombok.NoArgsConstructor;
import javax.persistence.Entity;

@NoArgsConstructor
@Entity
public class User {
    // ...

    @Builder
    public User(String name, String password) {
    	this.name = name;
    	this.password = password;
    }
}
```

### 방법 2. @AllArgsConstructor 를 추가
- 위에서 설명한 상황에서는 클래스에 `@NoArgsConstructor`를 사용하고 있기 때문에
  생성자에 `@Builder`를 적용하지는 못한다.
- 대신 클래스 자체에 `@AllArgsConstructor` 를 적용해서 
  Lombok 이 생성하지 못하는 모든 필드 생성자를 대신 생성해준다.
```java
import lombok.Builder;
import lombok.AllArgsConstructor;
import lombok.NoArgsConstructor;
import javax.persistence.Entity;

@Builder
@AllArgsConstructor
@NoArgsConstructor
@Entity
public class User {
    // ...
}
```

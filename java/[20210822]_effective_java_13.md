# 13. 클래스와 멤버의 접근 권한은 최소화하라

# 💡 요약
- 접근 권한은 최소한으로
  - 최소한의 public API를 설계하고 다른 것들은 제외할 것.
- public static final 필드를 제외한 모든 필드는 public 으로 선언하지 말 것.
- public static final 필드가 참조하는 객체는 변경 불가능 객체일 것.

---

# 👉 은닉, 캡슐화
- 잘 설계된 모듈은 구현 세부사항을 다른 모듈에 잘 감춘다.
- 모듈들은 API 로만 통신하고 내부적인 것까지는 신경쓰지 않는다.
- 소프트웨어 설계의 기본적인 원칙 가운데 하나.

# 👉 은닉의 장점
#### 1. 의존성을 낮춘다
- 각 모듈을 병렬적으로 개발할 수 있게 됨으로써 개발 속도 향상
#### 2. 효과적인 성능 최적화
- 다른 모듈의 영향도를 고려하지 않고 디버깅이 가능해짐
#### 3. 재사용성 향상
- 모듈간 의존성이 낮으므로 각 모듈이 다른 소프트웨어 개발에도 유용하게 쓰일 가능성 높음
#### 4. 개발 과정의 위험성 낮춤
- 전체 시스템의 성공 여부와 별개로 개발, 테스트, 최적화 가능

# 👉 Java 접근 제한자
Accessibility | Description
--- | ---
private | 최상위 레벨 클래스
package-private (default) | 같은 패키지의 모든 클래스
protected | 같은 패키지의 모든 클래스, 하위 클래스
public | 모든 클래스

# 👉 원칙
### ⭐⭐⭐️ 각 클래스와 멤버는 가능한 한 접근 불가능하도록 만들라

## 접근 제한자의 적절한 사용
- `public` : 공개 API, 호환성을 보장하기 위해 계속 지원해야 함.
- `package-private` : 해당 패키지 안에서만 유효하므로 클라이언트의 코드를 깨뜨릴 걱정 없이
  변경 가능.

## 중첩 클래스, 중첩 인터페이스 사용
- 한 클래스에서만 사용하는 최상위 클래스/인터페이스는 사용자 클래스의 private 중첩 클래스로
  만들 것을 고려해볼 것.
```java
class Shop {
    private String name;
    private int position;
    private List<Toy> toys;
}

class Toy {
    private String id;
    private String name;
    private int price;
}
```
↓ 이렇게?
```java
class Shop {
    private String name;
    private int position;
    private List<Toy> toys;

    private static class Toy {
    	private String id;
    	private String name;
    	private int price;
    }
}
```

# 👉 주의
## 객체 필드는 절대 public 이어서는 안 된다
- 메서드를 통하지 않고도 필드의 값을 변경할 수 있기에 값을 제한할 수 없게 된다.
  → 불변식을 보장할 수 없다.
- 변경 가능 public 필드를 가진 클래스는 다중 스레드에 안전하지 않다.
- public static final 필드로 상수를 공개하는 것은 예외.
  - 대문자, _ (underscore) 사용
  - 기본 자료형 값을 갖거나 불변 객체를 참조해야 함.

## public static final 배열 필드는 보안 문제를 초래한다
```java
public static final Thing[] VALUES = { ... };
```
- 참조를 변경할 수는 없으나 배열 내부의 값을 변경하는 게 가능하다.

### 대신 배열을 private 로 만들고
### 1. 불변의 public 리스트 추가
```java
private static final Thing[] PRIVATE_VALUES = { ... };

public static final List<Things> VALUES =
    Collections.unmodifiableList(Arrays.asList(PRIVATE_VALUES));
```
### 2. 해당 배열을 복사해서 반환하는 public 메서드 추가
```java
private static final Thing[] PRIVATE_VALUES = { ... };

public static final Thing[] values() {
    return PRIVATE_VALUES.clone;
}
```

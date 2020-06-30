# overloading
- 기존에 없는 새로운 메소드를 정의하는 것.
- 메소드의 이름은 같지만 매개변수의 개수와 타입은 달라야 함.
- 반환 타입은 영향을 주지 않음.

# overriding
- 상속받은 메서드의 내용 변경
- 선언부(메소드 이름, 매개변수, 반환 타입)가 완전히 일치해야 함.
- 상속관계에 있는 클래스 간에 이루어짐.

```java
class Parent {
    void parentMethod() {}
}

class Child extends Parent {
    void parentMethod() {}       // overriding
    void parentMethod(int i) {}  // overloading
}
```
# overloading
- 기존에 없는 새로운 메소드 정의

# overriding
- 상속받은 메서드의 내용 변경

```java
class Parent {
    void parentMethod() {}
}

class Child extends Parent {
    void parentMethod() {}       // overriding
    void parentMethod(int i) {}  // overloading
}
```
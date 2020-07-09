# How to compile and run a Java program using terminal
## 전제
1. Java가 설치되어 있어야 함.
2. jdk 환경 변수 설정되어 있어야 함.

## Java program
```text
$ vim Hello.java
```
```java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello, world!");
    }
}
```
```text
$ ls
Hello.java
```

## compile
```text
$ javac Hello.java
```
```text
$ ls
Hello.class     Hello.java
```

## run
```text
$ java Hello
Hello, world!
```

# 프로젝트 구조화
###  기존 알고 있던 방식
```text
com
 +- example
     +- myapplication
         +- Application.java
         |
         +- entity
         |   +- Customer.java
         |   +- Order.java
         |
         +- controller
         |   +- CustomerController.java
         |   +- OrderController.java
         |
         +- service
         |   +- CustomerService.java
         |   +- OrderService.java
         |
         +- repository
             +- CustomerRepository.java
             +- OrderRepository.java
```
- 개인적 의견
   - customer 관련 코드만 보는데 이 package 저 package 넘나들어야 함.
   - 파일 수가 적을 때는 그나마 괜찮았는데 기능이 많아지면서 파일 찾느라 스크롤 열일함.

```text
💡 Spring Boot does not require any specific code layout to work. 
However, there are some best practices that help.
```

### 공식 문서에서 권장하는 방식
```text
com
 +- example
     +- myapplication
         +- Application.java
         |
         +- customer
         |   +- Customer.java
         |   +- CustomerController.java
         |   +- CustomerService.java
         |   +- CustomerRepository.java
         |
         +- order
             +- Order.java
             +- OrderController.java
             +- OrderService.java
             +- OrderRepository.java
```

##### * Reference
   - https://docs.spring.io/spring-boot/docs/current/reference/html/using-spring-boot.html#using-boot-structuring-your-code

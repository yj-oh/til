# @GeneratedValue - auto_increment 문제

## 상황
- 회사에서 Spring Boot 2.0 + hibernate + MariaDB로 작업 중.
- 별 문제 없이 계속 작업을 해왔다.
- **금일, 새로 생성한 테이블에 새로운 데이터를 insert 하는데 @GeneratedValue 걸어놨던 PK에 500번대 id가 생성되는 상황이 있다는 걸 동료 개발자를 통해 알게됨.**
- **그리고 그 상황이라 함은 기본키 매핑시 @GeneratedValue 전략을 `AUTO`로 설정했을 때였음.**
- 🤷‍♀️ "......???"
- 내 사전 지식은,
   - Oracle DB에는 sequence 개념이 있지만 MySQL에는 없고 대신 pk에 auto_increment를 사용
   - 9월 20일 @GeneratedValue에 대해 공부한 바에 따르면 (참고 : [@GeneratedValue]([20200920]_generatedvalue.md))
      - 기본키 매핑에는 IDENTITY, SEQUENCE, AUTO, (위에는 정리하지 않았지만) `TABLE` 전략이 있음
   - `IDENTITY`는 기본키 생성을 데이터베이스에 위임
   - `AUTO`는 DB dialect에 따라 전략을 선택하는데, 오라클의 경우 SEQUENCE, MySQL의 경우 IDENTITY가 선택됨
- #### 결론적으로 `IDENTITY나 AUTO나 어쨌든 MySQL은 auto_increment를 사용한다`라고 알고 있었다.

## 그래서 혼돈의 카오스에 빠짐
- MariaDB를 쓰고 있고 `AUTO` 전략을 사용했는데 왜 시퀀스를 쓰지?
- DB table을 확인했더니 `hibernate_sequence`가 있다.
- `TABLE` 전략은 쓸 일이 없을 것 같아서 정리 안 했는데 찾아보니 모든 테이블의 시퀀스를 한 테이블에서 관리하는 방식이라고 함.
- 그렇다는 것은 MySQL에서 AUTO 전략을 선택하면 hibernate가 알아서 `TABLE` 전략을 사용한다는 것인데.
- 왜?

---

#### 짝꿍이 아래 링크를 보내주었다
- [기억보단 기록을 - Spring Boot Data JPA 2.0 에서 id Auto_increment 문제 해결](https://jojoldu.tistory.com/295)

## 내용을 요약하면
- Spring Boot는 Hibernate의 id 생성 전략을 그대로 따라갈지 말지를 결정하는 useNewIdGeneratorMappings 설정이 있고,
   - 1.5에선 기본값이 `false`, 2.0부터는 `true`
- Hibernate 5부터 MySQL에서의 GenerationType.AUTO는 IDENTITY가 아닌 TABLE을 기본 시퀀스 전략으로 가져간다.

## 해결
#### 방법 1. application.yml
```yaml
spring:
  jpa:
    hibernate: 
      use-new-id-generator-mappings: false
```

#### 방법 2. AUTO 전략 대신 IDENTITY 전략 사용

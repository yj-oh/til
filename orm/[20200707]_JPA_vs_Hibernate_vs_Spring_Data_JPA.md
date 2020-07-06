# JPA
- Java Persistence API
- 자바 진영의 ORM 기술 표준
- Java application에서 관계형 데이터를 관리하기 위한 `인터페이스`의 집합
- 구현이 필요하므로 단독으로 사용할 수 없음

# Hibernate
- JPA implementation
- JPA provider
- JPA를 구현한 오픈소스 ORM 프레임워크
- JPA가 Java의 interface라면 Hibernate는 그 interface를 구현한 class라고 할 수 있음.
- JPA를 구현한 ORM 프레임워크에는 EclipseLink, DataNucleus 등도 있으나 Hibernate가 가장 대중적

# Spring Data JPA
- JPA data access abstraction
- JPA provider 필요
- 스프링 프레임워크에서 JPA를 편리하게 사용할 수 있도록 지원하는 프로젝트
- 스프링 데이터 프로젝트의 하위 프로젝트 중 하나
- Repository를 개발할 때 인터페이스만 작성하면 실행 시점에 구현 객체를 동적으로 생성하여 주입해주므로 구현 클래스를 작성하지 않아도 됨.

# JPA, Hibernate, Spring Data JPA
![https://suhwan.dev/2019/02/24/jpa-vs-hibernate-vs-spring-data-jpa/](https://suhwan.dev/images/jpa_hibernate_repository/overall_design.png)

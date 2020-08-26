# Maven vs Gradle

## Maven
- Maven is a build automation tool used primarily for Java projects.
- 상속 구조로 유연성이 떨어짐
- pom.xml 이용
   - 설정 내용이 길어짐
   - 가독성 떨어짐
   - 의존 관계가 복잡한 프로젝트의 설정에 부적절
   - 동적 행위에 제약이 있음

## Gradle
- Gradle is a build automation tool for multi-language software development.
- Ant로부터 기본적 빌드 도구 기능을, Maven으로부터 의존 라이브러리 관리 기능 차용
- 그루비 문법 사용
- 설정 주입 방식으로 조금 더 유연함
- Maven보다 빠른 빌드

#### 👉 gradle을 쓰지 않을 이유가 없다.

##### * Reference : https://gradle.org/maven-vs-gradle/

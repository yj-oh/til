# groupId
```text
groupId will identify your project uniquely across all projects, so we need to enforce a naming schema. 
It has to follow the package name rules, what means that has to be at least as a domain name you control, 
and you can create as many subgroups as you want.
eg. org.apache.maven, org.apache.commons

A good way to determine the granularity of the groupId is to use the project structure. That is, if the 
current project is a multiple module project, it should append a new identifier to the parent's groupId.
eg. org.apache.maven, org.apache.maven.plugins, org.apache.maven.reporting
```
- 해당 프로젝트를 고유하게 식별하는 값.
- package 명명 규칙을 따른다.
- 최소한 도메인 이름이어야 한다.
- 원하는 수의 하위 그룹을 만들 수 있다.
- 예) `org.apache.maven`, `org.apache.commons`

- 다중 모듈 프로젝트일 경우 부모의 groupId에 새 식별자를 추가
- 예) `org.apache.maven`, `org.apache.maven.plugins`, `org.apache.maven.reporting`

# artifactId
```text
artifactId is the name of the jar without version. If you created it then you can choose whatever name 
you want with lowercase letters and no strange symbols. If it's a third party jar you have to take the name 
of the jar as it's distributed.
eg. maven, commons-math
```
- 버전 없는 jar 이름
- 소문자, 기호 없이 원하는 이름 선택
- third party jar면 배포된 이름 사용
- 예) `maven`, `commons-math`

# Spring Initializr : Advanced options
- `Group` : project coordinates (id of the project’s group, as referred by the groupId attribute in Apache Maven). Also infers the root package name to use.
- `Artifact` : project coordinates (id of the artifact, as referred by the artifactId attribute in Apache Maven). Also infers the name of the project
- `Name` : display name of the project that also determines the name of your Spring Boot application. For instance, if the name of your project is my-app, the generated project will have a MyAppApplication class
- `Description` : description of the project
- `Package Name` : root package of the project. If not specified, the value of the Group attribute is used
- `Packaging` : project packaging (as referred by the concept of the same name in Apache Maven). start.spring.io can generate jar or war projects
- *(Reference : https://docs.spring.io/initializr/docs/current/reference/html/)*

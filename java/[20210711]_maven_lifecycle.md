# Maven Lifecycle
- IntelliJ의 Maven tool을 열어보면 아래와 같다.

![](.%5B20210711%5D_maven_lifecycle_images/5c4145f2.png)

- 라이프 사이클
  - clean, validate, compile, test, package, verify, install,
    site, deploy
  - 쓰고는 있지만... 뭐지?
- 그래서 정리한다.
- 공식 문서를 참고했고, 역시나 필요한 부분만 가져와서 내 맘대로 번역.
- https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html

---

# 우선, Maven?
: 주로 Java 프로젝트에서 쓰이는 빌드 자동화 도구
- 빌드 프로세스 간소화
- 동일한 빌드 시스템 제공
- 양질의 프로젝트 정보 제공
- 더 나은 개발 관행 장려
- 프로젝트 의존성 관리, 라이브러리 관리, 라이프 사이클 관리
- 객체모델 (POM : Project Object Model) 개념과 플러그인 세트를 사용해 빌드를 수행한다.
- 참고 : https://maven.apache.org/what-is-maven.html

# Build Lifecycle Basics
## Three built-in build lifecycles
| Lifecycle | Description |
|-----------|-------------|
| default   | 프로젝트 배포     |
| clean     | 프로젝트 정리     |
| site      | 프로젝트 문서화    |

## Default lifecycle
| Phase    | Description                                         |
|----------|-----------------------------------------------------|
| validate | 프로젝트의 유효성을 확인                                       |
| compile  | 프로젝트의 소스 코드 컴파일                                     |
| test     | testing framework 를 사용하여 컴파일된 소스 코드 테스트 (패키징, 배포 X) |
| package  | JAR 등 배포 가능한 포맷으로 패키징                               |
| verity   | 패키지가 품질 기준에 적합한지 테스트                                |
| install  | 패키지를 로컬 저장소에 설치                                     |
| deploy   | 패키지를 원격 저장소에 배포                                     |

- 각각이 순차적으로 실행된다.

## Usual Command Line Calls
```text
mvn verify
```
- 위의 명령어를 실행하면 `verify` 전에 `validation`, `compile`, 
  `package`, etc. 등을 순차적으로 실행.
```text
mvn clean deploy
```
- 멀티 모듈 프로젝트에서는 모든 하위 프로젝트에 대해 명령어 실행.

## 플러그인 Plugins
- Maven에 골(goal)을 제공하는 아티팩트.
- 메이븐은 플러그인을 기반으로 동작한다.
- 메이븐은 여러 개의 플러그인으로 구성되어 있고 각각의 플러그인은 하나 이상의 골을 포함한다.

## 골 Goals
- 플러그인에서 실행할 수 있는 작업 단위.
- 여러 골을 묶어서 라이프 사이클 단계(phase)로 만들어 실행. 
  - e.g. `mvn clean deploy`

## 패키징 Packaging
- 각 패키징에는 특정 단계에 바인딩할 골 목록이 포함되어 있다.
- 이를테면 jar 패키징은 기본 수명 주기의 빌드 단계에 아래와 같은 골들을 바인딩한다.

| Phase                  | plugin:goal             |
|------------------------|-------------------------|
| process-resources      | resources:resources     |
| compile                | compiler:compile        |
| process-test-resources | resources:testResources |
| test-compile           | compiler:testCompile    |
| test                   | surefire:test           |
| package                | jar:jar                 |
| install                | install:install         |
| deploy                 | deploy:deploy           |

# Lifecycle Reference
## Clean Lifecycle
| Phase      | Description              |
|------------|--------------------------|
| pre-clean  | 프로젝트 정리 전 필요한 프로세스 실행    |
| clean      | 이전 빌드에서 생성된 모든 파일 제거     |
| post-clean | 프로젝트 정리를 완료하기 위한 프로세스 실행 |

## Default Lifecycle
| Phase                   | Description                                                            |
|-------------------------|------------------------------------------------------------------------|
| validate                | 프로젝트의 유효성을 확인                                                          |
| initialize              | 빌드 상태 초기화 (e.g. set properties, create directories)                    |
| generate-sources        | 컴파일할 모든 소스 코드 생성                                                       |
| process-sources         | 소스 코드 처리, 예를 들어 값을 필터링하기 위해                                            |
| generate-resources      | 패키지에 포함할 리소스 생성                                                        |
| process-resources       | 패키징 할 디렉토리로 리소스를 복사                                                    |
| compile                 | 소스 코드 컴파일                                                              |
| process-classes         | 컴파일 하고 생성된 파일을 사후 처리, 예를 들어 to do bytecode enhancement on Java classes |
| generate-test-sources   | 컴파일 할 테스트 코드 생성                                                        |
| process-test-sources    | 테스트 코드 처리, 예를 들어 값을 필터링 하기 위해                                          |
| generate-test-resources | 테스트 리소스 생성                                                             |
| process-test-resources  | 테스트 디렉토리로 리소스를 복사                                                      |
| test-compile            | 테스트 코드를 컴파일                                                            |
| process-test-classes    | 컴파일 하고 생성된 테스트 파일을 사후 처리                                               |
| test                    | unit testing framework 를 사용해 테스트 실행 (패키징, 배포 X)                        |
| prepare-package         | 패키징 전 필요한 작업 수행                                                        |
| package                 | 컴파일 된 코드를 가져와서 JAR 등과 같이 배포 가능한 포맷으로 패키징                               |
| pre-integration-test    | 통합 테스트 전 필요한 작업 수행 (환경 설정 등)                                           |
| integration-test        | 통합 테스트                                                                 |
| post-integration-test   | 통합 테스트 후 필요한 작업 수행                                                     |
| verify                  | 패키지가 품질 기준에 적합한지 테스트                                                   |
| install                 | 패키지를 로컬에 설치                                                            |
| deploy                  | 패키지를 원격 저장소에 배포                                                        |

## Site Lifecycle
| Phase       | Description      |
|-------------|------------------|
| pre-site    | 사전 작업            |
| site        | 프로젝트의 문서 생성      |
| post-site   | 생성 완료 및 배포 준비 작업 |
| site-deploy | 웹 서버에 문서 배포      |

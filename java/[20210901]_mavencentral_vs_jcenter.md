# mavenCentral vs jCenter
- 이전에 작업했던 gradle 프로젝트 살펴보다가 `build.gradle`에 있는 아래 설정이 궁금해짐.
```groovy
buildscript {
    repositories {
    	mavenCentral()
    	jCenter()
    }
}
```
- mavenCentral, jCenter 무슨 차이지?

---

## repositories {}
- 각종 라이브러리들을 어느 저장소에서 받을 건지 설정한다.

## mavenCentral
- Android studio 의 오픈 소스 라이브러리 저장소.
- https://repo.maven.apache.org/maven2/
- 먼저 나왔다.
- 근데 개발자 친화적이지 않아서 라이브러리를 업로드 할 때 여러 어려운 점이 있었다고 함.
- 그래서 jCenter 등장.

## jCenter
- 세계 최대의 Java 저장소
- mavenCentral 의 superset. 많은 추가적인 jar 포함.
- 성능이 mavenCentral 보다 더 좋다.
- mavenCentral 에도 자동으로 업로드 되도록 설정 가능.

##### * Reference : https://stackoverflow.com/questions/50726435/difference-among-mavencentral-jcenter-and-mavenlocal

---

# 🚨 jCenter : 읽기 전용 저장소로 변경됨!
- 찾다보니 이런 게 나온다.
- https://jfrog.com/blog/into-the-sunset-bintray-jcenter-gocenter-and-chartcenter/
```text
UPDATE 4/27/2021: We listened to the community and will keep JCenter as a read-only 
repository indefinitely. Our customers and the community can continue to rely 
on JCenter as a reliable mirror for Java packages.
```
- 2021년 3월 31일부로 읽기 전용 저장소가 되었단다.
- IntelliJ 켜서 `build.gradle` 확인하니 `jCenter()`에 경고 뜬다.
```text
Builds will no longer be able to resolve artifacts from JCenter after February 1st, 2022 
```
- **그냥 mavenCentral 쓰면 되겠다.**

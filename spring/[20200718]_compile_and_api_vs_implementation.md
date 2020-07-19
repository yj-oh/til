## build.gradle
```groovy
dependencies {
    complie 'library'
    implementation 'library'
    api 'library'
}
```

## compile or api
```text
Dependencies appearing in the api configurations will be transitively exposed to 
consumers of the library, and as such will appear on the compile classpath of consumers.
```
*(consumer : 라이브러리를 사용하는 모듈)*
- `compile`은 deprecated
- `api`를 사용할 것

## implementation
```text
Dependencies found in the implementation configuration will, on the other hand, 
not be exposed to consumers, and therefore not leak into the consumers' compile classpath.
```

## implementation을 사용할 때의 이점
```text
• dependencies do not leak into the compile classpath of consumers anymore, 
  so you will never accidentally depend on a transitive dependency
• faster compilation thanks to reduced classpath size
• less recompilations when implementation dependencies change: 
  consumers would not need to be recompiled
• cleaner publishing: when used in conjunction with the new maven-publish plugin, 
  Java libraries produce POM files that distinguish exactly between what is required 
  to compile against the library and what is required to use the library at runtime 
  (in other words, don’t mix what is needed to compile the library itself and what is 
  needed to compile against the library).
```
- dependency가 compile classpath에 노출되지 않아서, 실수로 transitive dependency를 의존하지 않음.
- 빠른 compile
- dependency 변경될 때 recompile 줄어듦.

## 정리
A library가 B library에 의존하고 B library가 C library에 의존할 때, (A <- B <- C)
- `api` : 종속성이 라이브러리를 사용하는 모듈에 노출되어 classpath에 포함됨.
- `implementation` : 노출되지 않아 classpath에 포함되지 않음.

고로, \
`implementation A`를 사용하면 A만 노출. A를 변경하면 직접 의존하는 B만 recompile. \
`api A`를 사용하면 B, C도 함께 노출. A를 변경하면 B, C 전부 recompile.

##### * References
- https://docs.gradle.org/current/userguide/java_library_plugin.html#sec:java_library_separation
- https://stackoverflow.com/questions/44493378/whats-the-difference-between-implementation-and-compile-in-gradle

# Spring Boot - Querydsl 설정

#### build.gradle
- Querydsl 관련 내용만 추림
```groovy
buildscript {
    ext {
        querydslVersion = '4.3.1'
    }
}

dependencies {
    implementation "com.querydsl:querydsl-apt:${querydslVersion}"
    implementation "com.querydsl:querydsl-jpa:${querydslVersion}"
    implementation "com.querydsl:querydsl-sql:${querydslVersion}"

    annotationProcessor "org.springframework.boot:spring-boot-starter-data-jpa:${springBootVersion}"
    annotationProcessor "com.querydsl:querydsl-apt:${querydslVersion}:jpa"
}
```

#### QClass 생성 위치
- build/generated/

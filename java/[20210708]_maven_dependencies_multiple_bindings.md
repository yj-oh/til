# Maven Dependencies - Multiple bindings

## 🤔 상황
- logback-classic dependency 설정하는데 아래와 같은 경고 메시지가 떴다.
```text
SLF4J: Class path contains multiple SLF4J bindings.
SLF4J: Found binding in [jar:file:/C:/Users/user/.m2/repository/.../org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/C:/Users/user/.m2/repository/.../org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: See http://www.slf4j.org/codes.html#multiple_bindings for an explanation.
```
- 기존에 설정해둔 다른 dependency와 multiple bindings.
  
## ❓ 원인
- 문제는 slf4j
- #### slf4j는 한 번에 하나의 로깅 프레임워크만 바인딩이 가능하다.

## 💡 해결
- 기존에 설정해둔 다른 dependency 에 \<exclusion> 추가해서
  slf4j-log4j12 지정해줬다.
- 다른 dependency에 포함된 걸 제외하고, logback-classic 사용하기 위함.
```xml
<dependencies>
    <dependency>
    	<groupId>...</groupId>
    	<artifactId>...</artifactId>
    	<version>...</version>
        <!-- 여기 추가 -->
    	<exclusions>
            <exclusion>
            	<groupId>org.slf4j</groupId>
            	<artifactId>slf4j-log4j12</artifactId>
            </exclusion>
    	</exclusions>
        <!-- /여기 추가 -->
    </dependency>
</dependencies>
```
- 참고 : http://www.slf4j.org/codes.html#multiple_bindings

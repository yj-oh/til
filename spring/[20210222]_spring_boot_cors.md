# Spring Boot - CORS 설정하기
* _참고 : [CORS에 대한 이해](../etc/[20210221]_cors.md)_
- 설정 방법 2가지
  - configuration
  - @CrossOrigin
    
## ☝️ Configuration
### /src/main/java/{package}/config/WebConfig.java
```java
@EnableWebMvc
@Configuration
public class WebConfig implements WebMvcConfigurer {
    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**")
            .allowedOrigins("*")
            .allowedMethods("GET", "POST")
            .maxAge(1000);
}
```

## ✌️ @CrossOrigin
- https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/web/bind/annotation/CrossOrigin.html
### Class
```java
@RestController
@RequestMapping("/path")
@CrossOrigin(origins = "*", allowedHeaders = "*")
public class ExampleController { }
```

### Method
```java
@RestController
@RequestMapping("/path")
public class ExampleController {
    @DeleteMapping("{id}")
    @CrossOrigin(origins = "*", allowedHeaders = "*")
    public Long delete(@PathVariable Long id) {
        return exampleService.delete(id);
    }
}
```

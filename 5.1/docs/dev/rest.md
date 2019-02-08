# REST API

REST API는 요청/응답 통신을 위한 아키텍처 스타일입니다.   
GET, POST, PUT 등과 같은 HTTP Method를 수용합니다.

spring-boot-starter-web 를 이용해서 REST API 를 개발할 수 있습니다. 

REST API와 관련된 주요 annotation 은 다음과 같습니다.

* @RestController
* @RequestMapping
* @GetMapping
* @PostMapping
* @PutMapping
* @DeleteMapping
* @PathVariable
* @RequestBody
* @RequestParam

다음은 개발시, 필요한 사항입니다. 

1. Maven Dependency  
    [Glue Maven Project](../create-project.html#glue_maven_project)로 프로젝트를 생성하면, pom.xml에 **spring-boot-starter-web** 이 포함되어 있습니다.  
    ```xml
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    ```

1. @SpringBootApplication  
    [Glue Maven Project](../create-project.html#glue_maven_project)로 프로젝트를 생성하면, 
    다음과 같은 **@SpringBootApplication** 이 있습니다.  
```java
@SpringBootApplication
public class SampleApplication {
    public static void main(String[] args) {
        SpringApplication.run(SampleApplication.class, args);
    }
}
```

1. @RestController  
    [Glue Maven Project](../create-project.html#glue_maven_project)로 프로젝트를 생성하면,
    다음과 같은 **@RestController** 가 있습니다.  
```java
@RestController
@RequestMapping( value = "/edu" )
public class SampleController {
    @GetMapping
    public String getVersion() {
        return "1.0.0";
    }
}
```
    개발하고자 하는 Application에서 REST API 를 제공하기, 위해서는 

1. 로그확인  
    RequestMappingHandlerMapping의 INFO 로그에서 ***[/edu],methods=[GET]*** 을 확인할 수 있습니다.  
```
  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::        (v2.0.6.RELEASE)
.
.
.
2019-01-25 09:47:21.494  INFO 6696 --- [           main] s.w.s.m.m.a.RequestMappingHandlerMapping : Mapped "{[/edu],methods=[GET]}" onto public java.lang.String com.poscoict.sample.rest.SampleController.getVersion()
2019-01-25 09:47:21.494  INFO 6696 --- [           main] s.w.s.m.m.a.RequestMappingHandlerMapping : Mapped "{[/edu/{serviceName}],methods=[GET]}" onto public java.util.List<java.util.Map<java.lang.String, java.lang.String>> com.poscoict.sample.rest.SampleController.runGlueService(java.lang.String,javax.servlet.http.HttpServletRequest)
```

## Example

제공되는 예제( ***glue-maven-project*** ) 실행 후, 콘솔 로그를 확인해보세요. 

* java -jar fat.jar 로 실행하기  
```bash
$ git clone https://github.com/poscoict-glueframework/glue-examples.git
$ cd glue-examples/
$ cd glue-maven-project/
$ mvn clean package                   # Maven Build ( Excutable Jar 생성 )
$ java -jar target/sample.jar         # Excutable Jar 실행
```

* spring boot maven plugin 으로 실행하기  
```bash
$ git clone https://github.com/poscoict-glueframework/glue-examples.git
$ cd glue-examples/
$ cd glue-maven-project/
$ mvn spring-boot:run                 # Spring Boot Maven Plugin으로 실행
```

## Try it

제공된 예제( ***glue-maven-project*** )를 Eclipse에 import 합니다.

제공된 예제의 *SampleController* 에 삭제 API(DELETE request)를 추가합니다. 

```java
@RestController
@RequestMapping( value = "/edu" )
public class SampleController {
    @Autowired
    private EmpRepository repository;

    @DeleteMapping( path = "{empno}" )
    public String deleteData(@PathVariable String empno) {
        repository.deleteById(empno);
        return "deleted";
    }
}
```

Spring Application을 실행한 후, 콘솔 로그에서 다음과 같은 것을 확인해 보세요.

```
Mapped "{[/edu],methods=[DELETE]}" onto public java.lang.String com.poscoict.sample.rest.SampleController.deleteData()
```

## Ref. 참고

* [https://spring.io/understanding/REST](https://spring.io/understanding/REST)
* [https://spring.io/guides/gs/rest-service/](https://spring.io/guides/gs/rest-service/)

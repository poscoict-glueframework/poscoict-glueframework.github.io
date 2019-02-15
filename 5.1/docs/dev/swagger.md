# Swagger

Swagger는 REST API 에 대한 매뉴얼 생성 및 테스트 사이트 생성 기능을 제공합니다. 

swagger 와 관련된 주요 annotation 은 다음과 같습니다.

* @EnableSwagger2
* @Api
* @ApiOperation
* @ApiImplicitParams
* @ApiImplicitParam
 
Swagger를 사용하기 위해서는 다음 사항이 필요합니다. 

1. Maven Dependency  
    [Glue Maven Project](../create-project.html#glue_maven_project)로 프로젝트를 생성하면, 
    pom.xml에 **swagger** 가 포함되어 있습니다.  
    ```xml
    <project>
        <properties>
            <springfox.swagger.version>2.9.2</springfox.swagger.version>
        </properties>
        <dependencies>
            <dependency>
                <groupId>io.springfox</groupId>
                <artifactId>springfox-swagger2</artifactId>
                <version>${springfox.swagger.version}</version>
            </dependency>
            <dependency>
                <groupId>io.springfox</groupId>
                <artifactId>springfox-swagger-ui</artifactId>
                <version>${springfox.swagger.version}</version>
            </dependency>
        </dependencies>
    </project>
    ```

1. @EnableSwagger2  
    [Glue Maven Project](../create-project.html#glue_maven_project)로 프로젝트를 생성하면, 
    다음과 같은 **@EnableSwagger2** 이 있습니다. 
```java
@SpringBootApplication
@EnableSwagger2
public class SampleApplication {
    public static void main(String[] args) {
        SpringApplication.run(SampleApplication.class, args);
    }
}
```

1. Docket 
    [Glue Maven Project](../create-project.html#glue_maven_project)로 프로젝트를 생성하면, 
    다음과 같은 **Docket** bean 이 있습니다. 
```java
@SpringBootApplication
@EnableSwagger2
public class SampleApplication {
    public static void main(String[] args) {
        SpringApplication.run(SampleApplication.class, args);
    }
	@Bean
	public Docket api() {
		return new Docket(DocumentationType.SWAGGER_2)
				.select()
				.apis(RequestHandlerSelectors.any())
				.paths(PathSelectors.any())
				.build();
	}
}
```


1. 로그확인  
RequestMappingHandlerMapping의 INFO 로그에서 ***{[/swagger-resources/configuration/ui]}*** 등을 확인할 수 있습니다.  
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
2019-01-25 09:47:21.494  INFO 6696 --- [           main] s.w.s.m.m.a.RequestMappingHandlerMapping : Mapped "{[/swagger-resources/configuration/security]}" onto public org.springframework.http.ResponseEntity<springfox.documentation.swagger.web.SecurityConfiguration> springfox.documentation.swagger.web.ApiResourceController.securityConfiguration()
2019-01-25 09:47:21.494  INFO 6696 --- [           main] s.w.s.m.m.a.RequestMappingHandlerMapping : Mapped "{[/swagger-resources/configuration/ui]}" onto public org.springframework.http.ResponseEntity<springfox.documentation.swagger.web.UiConfiguration> springfox.documentation.swagger.web.ApiResourceController.uiConfiguration()
2019-01-25 09:47:21.494  INFO 6696 --- [           main] s.w.s.m.m.a.RequestMappingHandlerMapping : Mapped "{[/swagger-resoues]}" onto public org.springframework.http.ResponseEntity<java.util.List<springfox.documentation.swagger.web.SwaggerResource>> springfox.documentation.swagger.web.ApiResourceController.swaggerResources()
2019-01-25 09:47:21.509  INFO 6696 --- [           main] s.w.s.m.m.a.RequestMappingHandlerMapping : Mapped "{[/error]}" onto public org.springframework.http.ResponseEntity<java.util.Map<java.lang.String, java.lang.Object>> org.springframework.boot.autoconfigure.web.servlet.error.BasicErrorController.error(javax.servlet.http.HttpServletRequest)
2019-01-25 09:47:21.509  INFO 6696 --- [           main] s.w.s.m.m.a.RequestMappingHandlerMapping : Mapped "{[/error],produces=[text/html]}" onto public org.springframework.web.servlet.ModelAndView org.springframework.boot.autoconfigure.web.servlet.error.BasicErrorController.errorHtml(javax.servlet.http.HttpServletRequest,javax.servlet.http.HttpServletResponse)
2019-01-25 09:47:22.169  INFO 6696 --- [           main] pertySourcedRequestMappingHandlerMapping : Mapped URL path [/v2/api-docs] onto method [public org.springframework.http.ResponseEntity<springfox.documentation.spring.web.json.Json> springfox.documentation.swagger2.web.Swagger2Controller.getDocumentation(java.lang.String,javax.servlet.http.HttpServletRequest)]
.
.
.
2019-01-25 09:47:22.741  INFO 6696 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8080 (http) with context path ''
2019-01-25 09:47:22.756  INFO 6696 --- [           main] com.poscoict.sample.SampleApplication    : Started SampleApplication in 23.07 seconds (JVM running for 24.867)
```

## SwaggerUI

SpringApplication 을 실행한 후, `http://localhost:8080/swagger-ui.html`를 통해 REST API를 확인할 수 있습니다.

### 기타 ( 작성중 )

1. 개발계, 운영계에 따라 Swagger 기능을 on/off 하기  
    ```java
    @Profile("!prod")
    @SpringBootApplication
    @EnableSwagger2
    public class SampleApplication {
        public static void main(String[] args) {
            SpringApplication.run(SampleApplication.class, args);
        }
    }
    ```

## Example

제공되는 예제( ***glue-maven-project*** ) 실행 후, SwaggerUI를 실행해보세요. 

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

Docket 을 다음과 같이 수정해보고, swagger-ui를 실행해보세요. 
```java
@SpringBootApplication
@EnableSwagger2
public class SampleApplication {
    public static void main(String[] args) {
        SpringApplication.run(SampleApplication.class, args);
    }
	@Bean
	public Docket api() {
		return new Docket(DocumentationType.SWAGGER_2)
				.select()
				.apis(RequestHandlerSelectors.basePackage(getClass().getPackage().getName())) // <- 수
				.paths(PathSelectors.any())
				.build();
	}
}
```

RestController를 다음과 같이 수정해보고, swagger-ui를 실행해보세요.
SampleController 클래스에 @Api를 추가합니다.  
SampleController 의 runGlueActivity 메소드에 @ApiOperation과 ApiImplicitParams 를 추가합니다. 
```java
@Api(tags={"샘플컨트롤러"}, description="Swagger @ApiXXXX 테스트용입니다.")
@RestController
@RequestMapping( value = "/edu" )
public class SampleController
{
// 중략
    
    @ApiOperation(value = "GlueActivity 실행예제")
    @ApiImplicitParams({
    	@ApiImplicitParam(name = "serviceName", value = "GlueService명", required = true, dataType = "string", paramType = "path", defaultValue = "no-service"),
    	@ApiImplicitParam(name = "empno", value = "emp number", required = true, dataType = "string", paramType = "query", defaultValue = "1"),
    	@ApiImplicitParam(name = "ename", value = "emp name", required = true, dataType = "string", paramType = "query", defaultValue = "POSCOICT")})
    @PostMapping( path = "{serviceName}", params = { "empno", "ename" } )
    public void runGlueActivity( @PathVariable String serviceName, @RequestParam String empno, @RequestParam String ename )
    {

// 중략
```

## Ref. 참고

* [http://springfox.github.io/springfox/docs/current/](http://springfox.github.io/springfox/docs/current/)

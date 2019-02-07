# Swagger

Swagger는 REST API 에 대한 매뉴얼 생성 및 테스트 사이트 생성 기능을 제공합니다. 

swagger 와 관련된 주요 annotation 은 다음과 같습니다.

* @RestController
 
Swagger를 사용하기 위해서는 다음 사항이 필요합니다. 

1. Maven Dependency  
    [Glue Maven Project](../create-project.html#glue_maven_project)로 프로젝트를 생성하면, 
    pom.xml에 swagger 가 포함되어 있습니다.  
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

2. @EnableSwagger2
    [Glue Maven Project](../create-project.html#glue_maven_project)로 프로젝트를 생성하면, 
    다음과 같은 @EnableSwagger2 이 있습니다. 
    ```java
    @SpringBootApplication
    @EnableSwagger2
    public class SampleApplication {
        public static void main(String[] args) {
            SpringApplication.run(SampleApplication.class, args);
        }
    }
    ```

## SwaggerUI

SpringApplication 을 실행한 후, `http://localhost:8080/swagger-ui.html`를 통해 REST API를 확인할 수 있습니다.

## 기타 ( 작성중 )

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
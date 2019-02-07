# index

1. [서론](./intro.html)
1. [개발환경 설정](./env.html)
    * [사전준비](./env.html)
        * [Java 설치](./env.html#java)
        * [Git(Git Bash) 설치](./env.html#git)
        * [Maven 설치](./env.html#maven)
        * [Eclipse 설치](./env.html#eclipse)
    * [Glue 개발환경](./env-glue.html)
        * [Glue Plugins 설치](./env-glue.html#GluePlugins)
        * [GlueSDK 설치](./env-glue.html#GlueSDK)
        * [Local Repository](./env-glue.html#m2)
            * [glue-framework artifact 추가](./env-glue.html#library)
            * [archetype 추가](./env-glue.html#archetype)
1. [프로젝트 생성](./create-project.html)
    - [Glue Maven Project](./create-project.html#glue_maven_project)
    - [archetype](./create-project.html#archetype)
    - [Spring Initializr](./create-project.html#spring_initialzr)
1. [Glue Activity Diagram](./glue-activity-diagram.html)
    - [Palette](./glue-activity-diagram.html#palette)
    - [Activity Setting](./glue-activity-diagram.html#activity)
    - [Transaction Setting](./glue-activity-diagram.html#transaction)
    - [Generate Service](./glue-activity-diagram.html#generate_xml)
    - [Generate Document](./glue-activity-diagram.html#generate_doc)
1. [개발](./glue.html)
    - [GlueService](./glue.html#GlueServie)
    - [GlueServiceManager](./glue.html#GlueServiceManager)
    - [GlueBizController](./glue.html#GlueBizController)
    - GlueActivity
    - Caching
    - Transaction
    - Logging
1. [REST API](./dev/rest.html)
    - [Swagger 사용하기](./dev/swagger.html)
    - RestTemplate
    - FeignClient
1. [JPA](./dev/jpa.html)
    - [h2](./dev/h2.html)
    - [mariadb](./mariadb.html)
    - [HeidiSQL](./mariadb.html)
1. Event
1. [Spring Framework](./spring-framework.html)
    * [IoC Container](./spring-framework.html#core)
    * [dependency injection](./spring-framework.html#core)
    * [ApplicationContext](./spring-framework.html#ApplicationContext)
    * [@Configuration](./spring-framework.html#@Configuration)
    * [@Bean](./spring-framework.html#@Bean)
    * [@Autowired](./spring-framework.html#@Autowired)
    * [@Component](./spring-framework.html#@Component)
    * [@Transactional](./spring-framework.html#@Transactional)
    * [@Cacheable](./spring-framework.html#@Cacheable)
1. [Spring Boot](./spring-boot.html)
    * [starter-parent](./spring-boot.html#maven)
    * [spring-boot-dependencies](./spring-boot.html#maven)
    * [spring-boot-maven-plugin](./spring-boot.html#maven-plugin)
    * [spring boot application starter](./dev/spring-boot-starter.html)
    * @SpringBootApplication
    * @Configuration
    * @ComponentScan
    * Run as ...
    * java -jar target/myapplication.jar
    * mvn spring-boot:run
    * spring-boot-devtools
    * banner
    * externalized configuration
    * profiles
    * logging
1. [Spring Data](./spring-data.html)
    * spring data jpa
    * spring data rest
1. [Spring Cloud](./spring-cloud.html)
    * config server
    * eureka server
1. [Spring Security](./spring-security.html)
1. Microservice 개발환경
    * [Lombok](../guide/lombok.html)
    * [h2](./dev/h2.html) [h2-console](./dev/h2.html#h2-console)
    * [mariadb](./dev/mariadb.html) [HeidiSQL](../guide/heidisql.html)
    * [kafka](./apache-kafka.html)
    * [activemq](./apache-activemq.html)
    * [gemfire](./pivotal-gemfire.html)
    * [zipken](../guide/zipkin.html)

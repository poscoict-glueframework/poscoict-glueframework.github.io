1. [서론](./intro.html)
1. 개발환경
    * [사전준비](./env.html) : Java, Git, Maven, Eclipse
    * [개발환경](./env-glue.html) : GlueSDK, Local Respository
        * [Glue Plugins 설치](./env-glue.html#GluePlugins)
        * [GlueSDK 설치](./env-glue.html#GlueSDK)
        * [Local Repository](./env-glue.html#m2)
            * [glue-framework artifact 추가](./env-glue.html#library)
            * [archetype 추가](./env-glue.html#archetype)
1. [프로젝트 생성](./create-project.html) : Glue Maven Project, Archetype, Spring Initializr
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
    - [Examples](./glue-examples.html)
1. [REST API](./dev/rest.html)
    - [Swagger 사용하기](./dev/swagger.html)
    - [RestTemplate](./dev/rest-resttemplate.html)
    - FeignClient
1. [JPA](./dev/jpa.html) : h2, mariadb
1. [Event](./dev/event.html) : kafka, activemq
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
    * [starter](./dev/spring-boot-starter.html)
    * @SpringBootApplication
    * @Configuration
    * @ComponentScan
    * [SpringApplication 실행하기](./dev/spring-boot-run-app.html)
        * java -jar 로 실행하기
        * IDE(Eclipse)에서 실행하기
        * Maven Plugin(mvn spring-boot:run)으로 실행하기
        * spring-boot-devtools
    * banner
    * externalized configuration
    * profiles
    * logging
1. [Spring Data](./spring-data.html)
    * spring data jpa
    * spring data rest
1. [Spring Cloud](./spring-cloud.html)
    * [config server](./spring-cloud-config.html)
    * [eureka server](./spring-cloud-netflix.html)
    * stream
    * sleuth
1. [Spring Security](./spring-security.html)
1. WebSocket
1. Microservice 개발환경
    * [Lombok](../guide/lombok.html)
    * [h2-console](../guide/h2-console.html)
    * [mariadb](../guide/mariadb.html)
    * [kafka](../guide/apache-kafka.html)
    * [activemq](../guide/apache-activemq.html)
    * [gemfire](../guide/pivotal-gemfire.html)
    * [zipkin](../guide/zipkin.html)
    * [HeidiSQL](../guide/heidisql.html)

# Glue Version

Glue Framework(*glue-core.jar*) 은 다음과 같은 버전을 사용합니다.
GlueSDK*-version*.zip 에 포함된 glue-core*-version*.pom 에서 spring boot 버전을 확인할 수 있습니다.

|Spring       | version|
|-------------|--------|
|Spring Boot|2.0.6.RELEASE|

> 스프링 프로젝트 생성시 `spring-boot-parent` 를 상속받거나, 
`spring-boot-dependencies` 를 추가해서 사용할 때, 참고하세요.

[Glue Maven Project](./create-project.html) 는 다음과 같은 버전을 사용합니다.  
Glue Maven Project의 pom.xml에서 spring 버전을 확인할 수 있습니다.
 
|Spring       | version|
|-------------|--------|
|Spring Cloud|Finchley.SR2|
|Spring Boot|2.0.6.RELEASE|

다음은 pom.xml 의 일부입니다. 
```xml
<project>
    <properties>
        <spring.boot.version>2.0.6.RELEASE</spring.boot.version>
        <spring.cloud.version>Finchley.SR2</spring.cloud.version>
    </properties>
</project>
```

## Ref. 참고

* [Spring Framework Versions](https://github.com/spring-projects/spring-framework/wiki/Spring-Framework-Versions)
* [Spring Boot Wikis](https://github.com/spring-projects/spring-boot/wiki)
* [Spring Cloud의 Release Trains](http://spring.io/projects/spring-cloud#release-trains)
* [https://opennote46.tistory.com/123](https://opennote46.tistory.com/123)

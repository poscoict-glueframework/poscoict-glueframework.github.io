# Spring Boot application starter

Spring Boot은 다양한 [Starter](../spring-boot.html#starter)를 제공합니다.

Spring의 official starter들은 `spring-boot-starter-*` 과 같은 네이밍을 따릅니다. 

## spring-boot-starter

spring-boot-starter은 기본 Starter로서, auto-configuration support, logging, YAML을 포함합니다.  
[quick-start](../quick-start.html) 예제에서는 `spring-boot-starter`가 사용되었습니다.

```xml
<project>
	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter</artifactId>
		</dependency>
	</dependencies>
</project>
```

[GlueMavenProject] 는 

```
com
 +- poscoict
     +- sample
         +- SampleApplication.java
         |
         +- jpa
         |   +- EmpJpo.java
         |   +- EmpRepository.java
         |
         +- rest
             +- SampleController.java
``` 
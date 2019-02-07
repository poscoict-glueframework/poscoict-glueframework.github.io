# Glue

Glue Framework 은 다음과 같은 버전을 사용합니다.

|             | version|
|-------------|--------|
|Spring Boot|2.0.6.RELEASE|

`spring-boot-parent` 를 상속받거나, 
`spring-boot-dependencies` 를 추가해서 사용할 때, 
사용되는 버전입니다. 

## Glue Maven Project 

Glue Maven Project 는 다음과 같은 버전을 사용합니다.  
pom.xml의 properties 부분을 확인하세요. 예제소스들도 이를 따릅니다.
 
|             | version|
|-------------|--------|
|Spring Cloud|Finchley.SR2|
|Spring Boot|2.0.6.RELEASE|

```xml
<project>
	<properties>
		<spring.boot.version>2.0.6.RELEASE</spring.boot.version>
		<spring.cloud.version>Finchley.SR2</spring.cloud.version>
	</properties>
</project>
```

## 예제

예제는 [GitHub](https://github.com/poscoict-glueframework/glue-examples)의 glue-maven-project와 quick-start를 참고하세요.

```bash
git clone https://github.com/poscoict-glueframework/glue-examples.git
``` 

Eclipse에서 `glue-maven-project` 와 `quick-start` 를 import 하면 다음과 같습니다.
![Image](../images/example-glue-maven-project.png)
![Image](../images/example-quick-start.png)

### ref

* [https://opennote46.tistory.com/123](https://opennote46.tistory.com/123)
* [https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-dependencies/2.0.6.RELEASE](https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-dependencies/2.0.6.RELEASE)
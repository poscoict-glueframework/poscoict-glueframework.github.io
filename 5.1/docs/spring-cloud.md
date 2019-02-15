# Spring Cloud

* Spring Cloud Config

* Spring Cloud Netflix ( Eureka, Zuul, etc )

* Spring Cloud Stream  
마이크로서비스, 외부 어플리케이션 간의 연계, 이벤트 드리븐 ( Kafka, RabbitMQ, etc )

* Spring Cloud Sleuth  
분산 트레이싱 ( Zipkin, etc )

Spring Cloud 는 여러 Release Trains가 있으며, 
GlueFramework 예제는 Finchley.SR2 를 사용합니다.  
Glue Maven Project로 프로젝트를 생성할 경우에는 다음을 추가하세요. 

```xml
<project>
	<dependencyManagement>
		<dependencies>
			<dependency>
				<groupId>org.springframework.cloud</groupId>
				<artifactId>spring-cloud-dependencies</artifactId>
				<version>Finchley.SR2</version>
				<type>pom</type>
				<scope>import</scope>
			</dependency>
		</dependencies>
	</dependencyManagement>
</project>
```

## Ref. 참고

* [Spring Cloud](https://spring.io/projects/spring-cloud)
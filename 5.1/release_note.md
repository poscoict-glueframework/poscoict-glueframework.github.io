# Release Note

### 5.1.2-RELEASE Released (2019-02-01)

* GlueServiceManager 수정 : RestTemplate을 생성하지 않고, autowired로 변경.

* GlueSDK 수정  
    swagger version up( 2.8.0 -> 2.9.2 )  
    templateFolder의 pom.xml 수정 ( h2 추가 )

* glue-core 의 dependency 수정 : h2 제거
    
### 5.1.1-RELEASE Released (2019-01-23)

GlueRestClientActivity 수정 : RestTemplate를 생성하지 않고, bean으로 주입받는 것으로 변경.( spring cloud sleuth 를 위해서 ) 

```java
//private RestTemplate restTemplate = new RestTemplate();

@Autowired
private RestTemplate restTemplate;
```

### 5.1.0-RELEASE Released (2018-12-28)

dependency 수정

- Spring Boot 2.0.6.RELEASE

### 5.1.0-SNAPSHOT Released (2018-10-31)

5.0.0-RELEASE 버전과는 호환되지 않으며, 사용환경은 다음과 같습니다. 

- Java 8이상

- Spring Framework 5.0.8.RELEASE

- Spring Boot 2.0.4.RELEASE
# Spring Framework

Spring Framework은 Java 기반의 엔터프라이즈 어플리케이션을 위한 개발 프레임워크입니다. 

[Glue](./glue.html)에서는 Spring Boot 버전을 2.0.6.RELEASE를 사용하므로, 
Spring Framework 버전은 5.0.10.RELEASE 입니다.

<a name="core"></a>IoC ( Inversion of Control, 제어의 역전 ) 는 DI ( Depencency Injection, 의존주입 ) 으로도 알려져 있고, 
Spring IoC 컴테이너에 의해 관리되는 오브젝트는 Bean 이라고 합니다.

![Image](https://docs.spring.io/spring/docs/5.0.10.RELEASE/spring-framework-reference/images/container-magic.png)

그림과 같이 Configuration Metadata에 근거해서 Spring IoC Container가 만들어진다. 
Configuration Metadata는 XML-based, Java-based 2가지가 가능하나, 여기서는 Java-based(annotaion-based)만 다룹니다. 

## <a name="ApplicationContext"></a>ApplicationContext

Spring Boot Application 이 아닌 경우에는 다음과 같이 ApplicationContext 를 생성해서 Spring IoC Container를 구동합니다. 

```java
public class ApplicationContextTest{
    public static void main(String[] args) {
        // Java-based configuration 일 경우임.
        ApplicationContext ctx = new AnnotationConfigApplicationContext(GlueConfiguration.class);
        // XML-based configuration 일 경우임.
        // ApplictionContext ctx = new ClassPathXmlApplicationContext( "applicationContext.xml" );
        for( String name : ctx.getBeanDefinitionNames() ) {
            System.out.println( name + " : " + ctx.getBean(name) );
        }
    }
}
```

Spring Boot Application 인 경우, 다음과 같이 SpringApplication을 실행하면, Spring IoC Container가 구동됩니다.

```java
@SpringBootApplication
public class SampleApplication {
	public static void main(String[] args) {
		SpringApplication.run(SampleApplication.class, args); 
		// SpringApplication 내부에서 new AnnotationConfigApplicationContext()이 생성됨
	}
}
```

## <a name="@Configuration"></a><a name="@Bean"></a>Configuration & Bean

Java-based 설정은 Spring 3.0부터 제공되며, @Configuration 과 @Bean 과 같은 annotation을 사용하면 됩니다. 
 
@Configuration이 붙은 class 를 통해 Bean을 구성할 수 있습니다.

```java
@Configuration
public class GlueConfiguration{
    @Bean
    public RestTemplate restTemplate()
    {
        return new RestTemplate();
    }
}
``` 

## <a name="@Autowired"></a><a name="@Component"></a>Autowired

Spring IoC Container에서 관리되는 Bean을 사용하기 위해서는 @Autowired를 사용하면 됩니다. 
@Autowired를 사용하기 위해서는 해당 클래스는 Sprign IoC Container 에 등록된 Bean이어야 합니다. 
@Component가 적용된 클래스는, @Component 등과 같은 annotaion을 통해, 
Spring IoC Container에 Bean으로 등록되며, 다른 Bean을 DI(주입) 할 수 있습니다. 

```java
@Component
public class GlueRestClientActivity extends GlueActivity<GlueContext>
{
    @Autowired
    private RestTemplate restTemplate;

    @Override
    public String runActivity( GlueContext ctx )
    {
        String uri = "http://localhost:8080/cateringpass/{userId}";
        Map<String, Object> uriVariables = new HashMap<>();
        uriVariables.put("userId", "poscoict");
        result = this.restTemplate.getForObject( uri, String.class, params );
        ctx.put("result", result);
        return "success";
    }
}
```

## <a name="@Transactional"></a>Transactional

Spring 에서 트랜잭션을 설정하는 방법은 크게 XML파일을 이용하는 설정과, 어노테이션을 이용한 설정이 있습니다. 
여기서는 어노테이션을 이용한 설정을 다룹니다(선언적 트랜잭션).

트랜잭션은 로컬 트랜잭션과 분산 트랜잭션을 고려해야하며, 여기서는 로컬 트랜잭션만 다룹니다. 
MSA환경에서의 Pattern(Saga, CQRS, Event Sourcing 등)을 이용해 분산 트랜잭션을 처리합니다.  

로컬 트랜잭션을 처리하려면, @EnableTransactionManagement 과 @Transactional을 사용합니다. 
트랜잭션이 필요한 메소드에 @Transactional 이라는 어노테이션을 달아주고, Configuration에  @EnableTransactionManagement 를 추가합니다.  

동작은 그림과 같습니다. 트랜잭션이 필요한 메소드(Target Method)를 실행하기 위해, AOP Proxy가 불려서, 
Transaction Advisor 가 트랜잭션을 생성해서, 비지니스 로직 처리후 에 commit/rollback 을 처리합니다. 

![Image](https://docs.spring.io/spring/docs/5.0.10.RELEASE/spring-framework-reference/images/tx.png)

다음은 Target Method 예시입니다. 
@Transactional의 default 설정값은 PROPAGATION_REQUIED와, ISOLATION_DEFAULT 입니다.

```java
@Repository
public class SampleStore
{
    @Autowired
    JpaRepository repository;
     
    @Transactional
    public Object targetMethod( Object ... obj ){
        repository.save( obj[1] );
        repository.save( obj[2] );
        repository.save( obj[3] );
    }
}
```

다음은 Configuration 예시입니다. 

```java
@EnableTransactionManagement
@SpringBootApplication
public class SampleApplication {
	public static void main(String[] args) {
		SpringApplication.run(SampleApplication.class, args); 
	}
}
```

## <a name="@Cacheable"></a>Cacheable

어플리케이션에서 빈번한 읽기가 발생하는 데이타가 있다면, 데이타베이스와 같은 데에서 빈번한 읽기가 발생한다면, 캐싱을 적용할 수 있을 것입니다.
Spring에서는 Cache Abstraction을 제공합니다.  Spring의 Cache Abstraction을 사용하기 위해서는 다음이 필요합니다. 

* @Cacheable
* @EnableCaching
* CacheManager

@Cacheable 어노테이션은 Cache를 적용하기를 원하는 Method에 붙이면 됩니다.
다음은 glue-core의 GlueServiceManager에 적용해보았습니다. 

```java
@Component
public class GlueServiceManager
{
    @Cacheable( value = "_service-region", key = "#serviceName", unless = "#result==null" )
    public GlueService getService( String serviceName )
    {
        URL url = GlueFileResourceUtil.getResource( "service" + File.separator + serviceName + ".xml" );
        return new GlueService( GlueServiceParser.parseXml( url ) );
    }
}
```

@EnableCaching 어노테이션은 은 Configuration에 추가합니다.
다음은 Application에 @EnableCaching을 적용한 예시입니다.

```java
@EnableCaching
@ComponentScan(basePackages = { "com.poscoict.glueframework" })
@SpringBootApplication
public class SampleApplication {
	public static void main(String[] args) {
		SpringApplication.run(SampleApplication.class, args); 
	}
}
```

CacheManager 는 구현해주어야하며, glue-core에서는 다음과 같이 Ehcache를 사용하는 것으로 구현되어 있습니다. 

```java
@Configuration
public class GlueConfiguration
{
    @Value( "${glue.cache.configuration:com/poscoict/glueframework/configuration/ehcache.xml}" )
    private String location;

    @Bean
    public CacheManager cacheManager()
    {
        EhCacheManagerFactoryBean factory = new EhCacheManagerFactoryBean();
        factory.setConfigLocation( new ClassPathResource( location ) );
        factory.setShared( true );
        factory.afterPropertiesSet();
        return new EhCacheCacheManager( factory.getObject() );
    }
}
```

## 참고 

* [https://spring.io/projects/spring-framework](https://spring.io/projects/spring-framework)
* [https://docs.spring.io/spring/docs/5.0.10.RELEASE/javadoc-api/](https://docs.spring.io/spring/docs/5.0.10.RELEASE/javadoc-api/)
* [https://docs.spring.io/spring/docs/5.0.10.RELEASE/spring-framework-reference/](https://docs.spring.io/spring/docs/5.0.10.RELEASE/spring-framework-reference/)
* [https://docs.spring.io/spring/docs/5.0.10.RELEASE/spring-framework-reference/data-access.html#transaction](https://docs.spring.io/spring/docs/5.0.10.RELEASE/spring-framework-reference/data-access.html#transaction)
* [https://docs.spring.io/spring/docs/5.0.10.RELEASE/spring-framework-reference/integration.html#cache](https://docs.spring.io/spring/docs/5.0.10.RELEASE/spring-framework-reference/integration.html#cache)
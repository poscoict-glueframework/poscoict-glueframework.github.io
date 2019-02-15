# RestTemplate

RESTful 웹서비스를 실행하기 위해서는 RestTemplate 을 직접사용하거나, GlueRestClientActivity 를 사용하는 방법이 있습니다.

Glue Example 중에 **glue-maven-project** 과 **quick-start** 를 Eclipse에 import 합니다.


## GlueRestClientActivity

Rest client activity는 다음과 같은 property를 갖습니다([참고](https://www.solutionpot.co.kr/doc/framework5.1/apidocs/com/poscoict/glueframework/biz/activity/GlueRestClientActivity.html)). 

* uri : Spring REST API 에 해당(key)
* method : HTTP method에 해당(value). GET,POST,PUT,DELETE  
* data : data(key)
* param-count : parameter 수(value). 
* param# : RestTempalte 의 uriVariable 구성에 사용되는 값에 해당(key)
* result-key : Activity의 수행 결과(key)

## RestTemplate

RestTemplate은 다음과 같은 method를 제공합니다([참고](https://docs.spring.io/spring/docs/5.0.10.RELEASE/javadoc-api/org/springframework/web/client/RestTemplate.html)). 

* getForObject(url, responseType, uriVariables)
* postForObject(url, request, responseType, uriVariables)
* put(url, request, uriVariables)
* delete(url, uriVariables)

## Try it 

glue-maven-project 는 RESTful 웹서비스를 제공하는 Applicaton으로,  
quick-start 는 RESTful 웹서비스를 사용(호출)하는 Application으로 사용합니다. 

제공된 예제( ***glue-maven-project*** )를 Eclipse에 import 합니다.
```bash
$ cp -r glue-examples/glue-maven-project/ sample-x  # RESTful 웹서비스 제공
$ cp -r glue-examples/quick-start/ demo-x           # 웹서비스 호출
$ 
$ # demo-x/pom.xml 의 artifactId 값을 수정한 후 import할 것.
```

### case 1
 
GlueRestClientActivity 을 사용해보세요.  

**demo-*****x*** 의 DempApplication을 다음과 같이 수정합니다. 

```java
public class DemoApplication {
    // 중략
    @Bean
    public CommandLineRunner run_case1( GlueRestClientActivity activity )
    {
        return ( args -> {
            Map<String, String> props = new HashMap<>();
            props.put("uri", "uri-key"); // http://localhost:8080/edu/
            props.put("method", "GET");
            props.put("result-key", "result");
            
            GlueDefaultContext ctx = new GlueDefaultContext( "no-service" );
            ctx.setActivityProperties(activity, props);
            ctx.put("uri-key", "http://localhost:8080/edu/");
            activity.runActivity(ctx);
            
            System.out.println( "GlueRestClientActivity 실행결과: " + ctx.get("result") );
        } );
    }
```

**sample-*****x*** 의 다른 REST API를 호출해보세요. uri를 변경해보세요. 

```java
public class DemoApplication {
    // 중략
    @Bean
    public CommandLineRunner run_case1( GlueRestClientActivity activity )
    {
        return ( args -> {
            Map<String, String> props = new HashMap<>();
            props.put("uri", "uri-key"); // http://localhost:8080/edu/{serviceName}
            props.put("method", "GET");
            props.put("param-count", "1");
            props.put("param1", "serviceName");
            props.put("result-key", "result");
            
            GlueDefaultContext ctx = new GlueDefaultContext( "no-service" );
            ctx.setActivityProperties(activity, props);
            ctx.put("uri-key", "http://localhost:8080/edu/{serviceName}");
            ctx.put("serviceName", "sample-service");
            activity.runActivity(ctx);
            
            System.out.println( "GlueRestClientActivity 실행결과: " + ctx.get("result") );
        } );
    }
```


### case 2
 
RestTemplate 을 사용해 보세요.  

**demo-*****x*** 의 DempApplication을 다음과 같이 수정합니다. 

```java
public class DemoApplication {
    // 중략
    @Autowired
    private RestTemplate restTemplate;
    @Bean
    public CommandLineRunner run_case2( RestTemplate restTemplate )
    {
        return ( args -> {
            String result = this.restTemplate.getForObject("http://localhost:8080/edu/", String.class);
            System.out.println("RestTemplate 실행결과: " + result);
        } );
    }
```

**sample-*****x*** 의 다른 REST API를 호출해보세요. uri를 변경해보세요. 

```java
public class DemoApplication {
    // 중략
    @Autowired
    private RestTemplate restTemplate;
    @Bean
    public CommandLineRunner run_case2( RestTemplate restTemplate )
    {
        return ( args -> {
            Map<String, Object> uriVariables = new HashMap<>();
            uriVariables.put("serviceName", "sample-service");
            String result = this.restTemplate.getForObject("http://localhost:8080/edu/{serviceName}", String.class, uriVariables);
            System.out.println("RestTemplate 실행결과: " + result);
        } );
    }
```

## Ref. 참고

* [https://spring.io/guides/gs/rest-service/](https://spring.io/guides/gs/rest-service/)
* [https://spring.io/guides/gs/consuming-rest/](https://spring.io/guides/gs/consuming-rest/)
* [GlueRestClientActivity javadoc](https://www.solutionpot.co.kr/doc/framework5.1/apidocs/com/poscoict/glueframework/biz/activity/GlueRestClientActivity.html)
* [RestTemplate javadoc](https://docs.spring.io/spring/docs/5.0.10.RELEASE/javadoc-api/org/springframework/web/client/RestTemplate.html)
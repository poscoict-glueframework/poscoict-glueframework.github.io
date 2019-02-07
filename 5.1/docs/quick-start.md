# Quick Start

순서는 다음과 같습니다. 

1. [Spring Boot 프로젝트 생성하기](./quick-start.html#createPrj)
1. [Sample Application 작성](./quick-start.html#dev)
1. [Sample Application 실행](./quick-start.html#run)

## <a name="createPrj"></a>Spring Boot 프로젝트 생성하기

[Spring Initializr](https://start.spring.io/) 에서 프로젝트를 생성합니다.

1. Spring Initializr 사이트에 접속합니다.
1. Generate Project 버튼을 클릭한다.
1. 압축을 푼 후, Eclipse에서  import 합니다.

> 참고 : [guide](./create-project.html#spring_initialzr)

## <a name="dev"></a>Sample Application 작성

GlueService를 구현합니다.  

1. Maven Dependency
1. GlueService

최종 결과는 다음과 같습니다. 

```
demo/
demo/pom.xml                                                 # 1. pom.xml 수정
demo/src/main/java/com/example/demo/DemoApplication.java     # 2. DemoApplication 수정
demo/src/main/resources/service/hello-service.xml            # 3. hello-service 추가
demo/src/main/java/sample/activity/HelloActivity.java        # 4. HelloActivity 추가
```

#### <a name="dev_pom"></a>pom.xml 수정

pom.xml 에 `glue-core` dependecy 를 추가합니다.  

```xml
<project>
    <dependencies>
        <dependency>
            <groupId>com.poscoict.glueframework</groupId>
            <artifactId>glue-core</artifactId>
            <version>5.1.1-RELEASE</version>
        </dependency>
    </dependencies>
```

> `glue-core` 는 [Glue 개발환경](./env-glue.html)에서 [glue-framework artifact 추가](./env-glue.html#library) 파트가 선행되어야 합니다.  
> `spring-boot-starter-parent` 의 최소 버전은 2.0.6.RELEASE 입니다.  
> `glue-core` 의 최소 버전은 5.1.0-RELEASE 입니다. 

#### <a name="dev_service"></a>hello-service.xml 생성

src/main/resources 에 service 디렉토리를 생성하세요.  
service 디렉토리에 hello-service.xml 을 생성하세요.  
hello-service.xml 파일의 내용은 다음과 같습니다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<service name="hello-service" initial="HelloActivity" xmlns="http://www.poscoict.com/glueframework/service">
    <activity name="HelloActivity" class="sample.activity.HelloActivity">
        <transition name="success" value="end"/>
        <property name="belongTo" value="POSCOICT"/>
    </activity>
</service>
```

> GluePlugin이 설치된 경우, [Glue Activity Diagram](./glue-activity-diagram.html#generate_xml)을 작성한 후, 
> Generate Service 기능을 통해 xml 파일을 생성할 수 있습니다.

#### <a name="dev_activity"></a>HelloActivity.java 생성

src/main/java 에 sample.activity.HelloActivity 클래스를 생성하세요.
HelloActivity.java 파일의 내용은 다음과 같습니다.   

```java
package sample.activity;

import org.springframework.stereotype.Component;

import com.poscoict.glueframework.biz.activity.GlueActivity;
import com.poscoict.glueframework.biz.activity.GlueActivityConstants;
import com.poscoict.glueframework.context.GlueContext;

@Component
public class HelloActivity extends GlueActivity<GlueContext>
{
    @Override
    public String runActivity( GlueContext ctx )
    {
        System.out.println( "ServiceName : " + ctx.getServiceName() );
        System.out.println( "This is '" + ctx.getActivityName() + "' activity" );

        Object input = ctx.get( "input" );
        System.out.println( "data : " + input );

        String belongTo = ctx.getProperty("belongTo");
        System.out.println( "data : " + belongTo );

        Object output = "["+belongTo+"] Hello " + input + "!!!";
        ctx.put( "result", output );

        return GlueActivityConstants.SUCCESS;
    }
}
```

> GlueActivity를 상속하고, @Component를 붙입니다.  

#### <a name="dev_application"></a>DemoApplication.java 수정

```java
package com.example.demo;

import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.ComponentScan;

import com.poscoict.glueframework.biz.control.GlueBizController;
import com.poscoict.glueframework.context.GlueContext;
import com.poscoict.glueframework.context.GlueDefaultContext;

@SpringBootApplication
@ComponentScan( basePackages = { "sample", "com.poscoict.glueframework" } )
public class DemoApplication {
    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
    @Bean
    public CommandLineRunner run( GlueBizController bizController )
    {
        return ( args -> {
            GlueContext ctx = new GlueDefaultContext( "hello-service" );
            ctx.put( "input", "Glue" );

            bizController.doAction( ctx );

            System.out.println( ctx.get( "result" ) );
        } );
    }
}
```

> @ComponentScan 의 basePackage 를 통해, HelloActivity 와 GlueBizController 를 찾아서 bean으로 생성합니다.  
> CommandLineRunner 를 통해 SpringApplication이 시작될 때, 해당 code를 한번 실행시킬 수 있으며, 
> 본 예제는 hello-service 를 실행시킵니다.

### <a name="run"></a>Sample Application 실행

다음은 전체 로그입니다. 
```
  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::        (v2.0.6.RELEASE)

2018-10-30 11:35:12.559  INFO 51352 --- [           main] com.example.demo.DemoApplication         : Starting DemoApplication on PICFAIRIES with PID 51352 (C:\Users\Administrator\Downloads\demo\target\classes started by fairies in C:\Users\Administrator\Downloads\demo)
2018-10-30 11:35:12.575  INFO 51352 --- [           main] com.example.demo.DemoApplication         : No active profile set, falling back to default profiles: default
2018-10-30 11:35:12.718  INFO 51352 --- [           main] s.c.a.AnnotationConfigApplicationContext : Refreshing org.springframework.context.annotation.AnnotationConfigApplicationContext@79ad8b2f: startup date [Tue Oct 30 01:35:12 KST 2018]; root of context hierarchy
2018-10-30 11:35:14.617  INFO 51352 --- [           main] o.s.c.ehcache.EhCacheManagerFactoryBean  : Initializing EhCache CacheManager
2018-10-30 11:35:16.247  INFO 51352 --- [           main] o.s.j.e.a.AnnotationMBeanExporter        : Registering beans for JMX exposure on startup
2018-10-30 11:35:16.263  INFO 51352 --- [           main] o.s.j.e.a.AnnotationMBeanExporter        : Bean with name 'dataSource' has been autodetected for JMX exposure
2018-10-30 11:35:16.263  INFO 51352 --- [           main] o.s.j.e.a.AnnotationMBeanExporter        : Located MBean 'dataSource': registering with JMX server as MBean [com.zaxxer.hikari:name=dataSource,type=HikariDataSource]
2018-10-30 11:35:16.295  INFO 51352 --- [           main] com.example.demo.DemoApplication         : Started DemoApplication in 4.592 seconds (JVM running for 5.477)
2018-10-30 11:35:16.311  INFO 51352 --- [           main] c.p.g.biz.control.GlueBizController      : ServiceName:[hello-service] StartTime[Tue Oct 30 01:35:16 KST 2018]
ServiceName : hello-service
This is 'HelloActivity' activity
data : Glue
data : POSCOICT
2018-10-30 11:35:16.663  INFO 51352 --- [           main] c.p.g.biz.control.GlueBizController      : ServiceName:[hello-service] EndTime[Tue Oct 30 01:35:16 KST 2018] RunTime:[352]
[POSCOICT] Hello Glue!!!
2018-10-30 11:35:16.663  INFO 51352 --- [       Thread-4] s.c.a.AnnotationConfigApplicationContext : Closing org.springframework.context.annotation.AnnotationConfigApplicationContext@79ad8b2f: startup date [Tue Oct 30 01:35:12 KST 2018]; root of context hierarchy
2018-10-30 11:35:16.679  INFO 51352 --- [       Thread-4] o.s.j.e.a.AnnotationMBeanExporter        : Unregistering JMX-exposed beans on shutdown
2018-10-30 11:35:16.679  INFO 51352 --- [       Thread-4] o.s.j.e.a.AnnotationMBeanExporter        : Unregistering JMX-exposed beans
```

다음은 GlueService 실행 로그만 분리했습니다. 
```
2018-10-30 11:35:16.295  INFO 51352 --- [           main] com.example.demo.DemoApplication         : Started DemoApplication in 4.592 seconds (JVM running for 5.477)
2018-10-30 11:35:16.311  INFO 51352 --- [           main] c.p.g.biz.control.GlueBizController      : ServiceName:[hello-service] StartTime[Tue Oct 30 01:35:16 KST 2018]
ServiceName : hello-service
This is 'HelloActivity' activity
data : Glue
data : POSCOICT
2018-10-30 11:35:16.663  INFO 51352 --- [           main] c.p.g.biz.control.GlueBizController      : ServiceName:[hello-service] EndTime[Tue Oct 30 01:35:16 KST 2018] RunTime:[352]
[POSCOICT] Hello Glue!!!
```

소스는 [GitHub](https://github.com/poscoict-glueframework/glue-examples/tree/master/quick-start)를 참고하세요.
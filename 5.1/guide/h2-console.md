# H2 Console

http://localhost:8080/h2-console

다음 3가지를 충족하면 H2 Web Console을 사용할 수 있습니다. 

* `spring-boot-starter-web` 과 `spring-boot-starter-data-jpa` 를 사용한다.   
* classpath에 H2가 있다.
* `spring-boot-devtools` 을 사용한다.  
    `spring-boot-devtools`을 사용하지 않는다면, `spring.h2.console.enabled` property를 true로 지정합니다.

> pom.xml 의 dependency에서 확인가능합니다.   
> application.yml 의 spring.h2.console 를 수정할 수 있습니다.

## Spring Property

h2 console과 관련된 주요 property는 다음과 같습니다.  

* spring.h2.console.enabled
* spring.h2.console.path


```yml
spring:
  h2:
    console:
      enabled: true
      path: /h2-console
```

로그와 관련된 property 예시는 다음과 같습니다.

```yml
logging:
  level: 
    ROOT: INFO
    com.zaxxer.hikari: DEBUG
```

다음은 로그 예시입니다.
```
2019-01-31 15:53:54.894 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : Driver class org.h2.Driver found in Thread context class loader org.springframework.boot.devtools.restart.classloader.RestartClassLoader@493c140e
2019-01-31 15:53:55.161 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : HikariPool-1 - configuration:
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : allowPoolSuspension.............false
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : autoCommit......................true
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : catalog.........................none
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : connectionInitSql...............none
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : connectionTestQuery.............none
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : connectionTimeout...............30000
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : dataSource......................none
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : dataSourceClassName.............none
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : dataSourceJNDI..................none
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : dataSourceProperties............{password=<masked>}
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : driverClassName................."org.h2.Driver"
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : healthCheckProperties...........{}
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : healthCheckRegistry.............none
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : idleTimeout.....................600000
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : initializationFailFast..........true
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : initializationFailTimeout.......1
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : isolateInternalQueries..........false
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : jdbc4ConnectionTest.............false
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : jdbcUrl.........................jdbc:h2:mem:testdb;DB_CLOSE_DELAY=-1;DB_CLOSE_ON_EXIT=FALSE
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : leakDetectionThreshold..........0
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : maxLifetime.....................1800000
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : maximumPoolSize.................10
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : metricRegistry..................none
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : metricsTrackerFactory...........none
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : minimumIdle.....................10
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : password........................<masked>
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : poolName........................"HikariPool-1"
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : readOnly........................false
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : registerMbeans..................false
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : scheduledExecutor...............none
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : scheduledExecutorService........internal
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : schema..........................none
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : threadFactory...................internal
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : transactionIsolation............default
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : username........................"sa"
2019-01-31 15:53:55.176 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.HikariConfig           : validationTimeout...............5000
2019-01-31 15:53:55.176  INFO 8232 --- [  restartedMain] com.zaxxer.hikari.HikariDataSource       : HikariPool-1 - Starting...
2019-01-31 15:53:55.660 DEBUG 8232 --- [  restartedMain] com.zaxxer.hikari.pool.HikariPool        : HikariPool-1 - Added connection conn0: url=jdbc:h2:mem:testdb user=SA
```
# JPA

spring-boot-starter-data-jpa 를 이용해서 Data Access 를 개발할 수 있다. 

JPA(Java Persistent API)는 객체(데이타)를 데이타베이스(관계형DB)에 저장하는 기술입니다.
JPA와 관련된 주요 annotation 은 다음과 같습니다.

* @Entity
* @Id
* @Table
* @EnableJpaRepositories

다음은 개발시, 필요한 사항입니다. 

1. Maven Repository
    [Glue Maven Project](../create-project.html#glue_maven_project)로 프로젝트를 생성하면, 
    pom.xml에 `spring-boot-starter-data-jpa`, `h2` 가 포함되어 있습니다. 
    ```xml
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    <dependency>
        <groupId>com.h2database</groupId>
        <artifactId>h2</artifactId>
    </dependency>
    ```

1. Configuration  
    H2와 같은 in-memory를 사용하면, Spring Boot에서 제공된 configuration을 사용할 수 있습니다.  
    [Glue Maven Project](../create-project.html#glue_maven_project)로 프로젝트의 
    pom.xml 에는 `h2`가 있으므로, autoconfigure 가 적용됩니다.  

1. @Entity
   [Glue Maven Project](../create-project.html#glue_maven_project)로 프로젝트를 생성하면, 
   EmpJpo 라는 예제가 포함되어 있습니다. 
   ```java
    @Entity(name="Emp")
    public class EmpJpo {
        @Id
        private int empno;
        private String ename;
        // 중략
    }
   ```

1. Repository
    [Glue Maven Project](../create-project.html#glue_maven_project)로 프로젝트를 생성하면, 
    EmpRepository 라는 예제가 포함되어 있습니다.
    ```java
    public interface EmpRepository extends PagingAndSortingRepository<EmpJpo, String> {
        Optional<EmpJpo> findByEname( String name );
    }
    ```

## Sample

Sample 실행 후, swagger-ui를 통해 data crud를 해보세요. 

```bash
$ git clone https://github.com/poscoict-glueframework/glue-examples.git
$ cd glue-examples/
$ cd glue-maven-project/
$ mvn clean package
$ java -jar target/sample.jar
```

## Try it

H2 에서 MariaDB로 변경해보세요.

## 참고

* [https://spring.io/guides/gs/accessing-data-jpa/](https://spring.io/guides/gs/accessing-data-jpa/)
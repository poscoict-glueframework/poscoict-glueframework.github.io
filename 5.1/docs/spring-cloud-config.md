# Spring Cloud Config

분산시스템에서는 application의 설정값을 config server으로부터 제공받습니다.  
Git과 같은 외부환경에 property들이 관리되고, 
config server에서 client들(application)에게 property를 제공합니다. 
 
![Image](https://i0.wp.com/blog.leekyoungil.com/wp-content/uploads/2017/04/1.png)

Config Server는 Spring Boot Application으로 개발할 수 있습니다.
* **spring-cloud-config-server** 를 dependency로 가져갑니다.  
* @EnableConfigServer 를 통해 Spring Boot Application에 Config Server 기능을 추가합니다.
* **spring.cloud.config.server.git.uri** 에 git repository 주소를 지정합니다.  
git uri는 2가지 유형으로 지정할 수 있습니다. 
    * remote Git 예시는 다음과 같습니다. 
```properties
spring.cloud.config.server.git.uri=https://github.com/poscoict-glueframework/msa-service-config.git
``` 

    * 로컬 file 시스템 예시는 다음과 같습니다. ( 윈도우, 리눅스 예시 )
```properties
spring.cloud.config.server.git.uri=file:///C:/workspace/config-repo
spring.cloud.config.server.git.uri=file://workspace/config-repo
```

Spring Boot Application 들은 Config Server를 바라보도록 합니다. 
* **bootstrap.properties** ( 또는 bootstrap.yml ) 를 사용합니다.
* **spring-cloud-startere-config** 를 dependency로 가져갑니다.
* Application 들은 **spring.application.name** 으로 구분됩니다.  
* config server 주소는 * **spring.cloud.config.uri** 에 설정합니다. 
    * 로그를 통해 다음을 확인할 수 있습니다. 
```
Fetching config from server at : http://localhost:8888
Located environment: name=demo, profiles=[default], label=null, version=3d596858e79b8a2ff9f18762e5d0470c7443d6fe, state=null
```      

## Try it

### Git 준비 

config-repo 라는 git repository를 만드세요.   

```bash
$ # 1. config-repo 생성
$ cd /c/workspace
$ mkdir config-repo
$ 
$ # 2. git init
$ cd config-repo
$ git init .
$ 
$ # 3. application의 property 파일 추가
$ echo app.title: Welcome. > demo.properties
$ echo biz.name: DemoBiz >> demo.properties
$ echo app.title: Demo Developing.. > demo-dev.properties 
$ echo app.title: Demo Testing.. > demo-test.properties 
$ echo app.title: Hi.  > sample.properties
$ echo biz.name: SampleBiz >> sample.properties
$ echo app.title: Sample Develooping.. > sample-dev.properties 
$ echo app.title: Sample Testing.. > sample-prod.properties
$ 
$ # 4. git repository 에 반영 
$ git add -A .
$ git commit -m "init"
```

Spring Boot Application 별 Config 파일은 **spring.application.name** 에 해당하는 값입니다. 
그리고 Profile별로 Config 파일을 생성해서 관리합니다. 

### Server

Server용 Spring Boot Application을 다음과 같이 개발합니다.  

```bash
$ # 1. 프로젝트 생성
$ # 1-1 https://start.spring.io ( 아래 참고 )
$ 
$ # 1-2 다운로드 폴더로 이동
$ cd ~/Downloads
$ 
$ # 1-3. workspace에 압축풀기
$ unzip config-server.zip -d /c/workspace
```

* 1-1 https://start.spring.io  
Spring Initializr에서 다음 정보로 프로젝트를 생성합니다. 그외는 default 로 생성하세요.  
    * Spring Boot 버전은 2.x 최신버전으로 하세요. 
    * Project Meta 정보를 입력하세요.
        - group : ***com.poscoict.sample***  
        - artifact : ***config-server***
    * Dependency를 추가하세요.
        - **Actuator**
        - **Config Server**

```bash
$ # 2. Eclipse 에 import 후 개발
$ # 2-1. Application 수정 ( ConfigServerApplication.java 아래 참고 ) 
$ # 2-2. property 수정 ( application.properties 아래 참고 ) 
```

* 2-1. Application 수정:   
@EnableConfigServer 어노테이션을 추가하세요. 
```java
@EnableConfigServer
@SpringBootApplication
public class ConfigServerApplication {
	public static void main(String[] args) {
		SpringApplication.run(ConfigServerApplication.class, args);
	}
}
```

* 2-2. property 수정 :  
spring.cloud.config.server.git.uri 를 설정합니다. 
```yml
server.port: 8888
spring.cloud.config.server.git.uri: file:///C:/workspace/config-repo
``` 

```bash
$ # 3. 테스트
$ # 3-1 이동
$ cd /c/workspace/config-server
$ 
$ # 3-1. config-server 실행
$ mvn spring-boot:run
$ 
$ # 3-2. config-server 체크
$ # curl localhost:8888/demo-dev.yml
```

* 3-2. config-server 체크  
  브라우저에서 다음과 같은 주소를 실행해봅니다. demo 대신에 sample을 사용하셔도 됩니다. 
    * http://localhost:8888/demo/dev
    * http://localhost:8888/demo-default.yml
    * http://localhost:8888/demo-dev.yml
    * http://localhost:8888/demo-prod.yml
    * http://localhost:8888/demo-dev.properties 
    * http://localhost:8888/demo-prod.properties

## Client Side

Client용 Spring Boot Application을 다음과 같이 개발합니다.  

```bash
$ # 1. 프로젝트 생성
$ # 1-1 https://start.spring.io ( 아래 참고 )
$ 
$ # 1-2 다운로드 폴더로 이동
$ cd ~/Downloads
$ 
$ # 1-3. workspace에 압축풀기
$ unzip config-client.zip -d /c/workspace
```

* 1-1 https://start.spring.io  
Spring Initializr에서 다음 정보로 프로젝트를 생성합니다. 그외는 default 로 생성하세요.  
    * Spring Boot 버전은 2.x 최신버전으로 하세요. 
    * Project Meta 정보를 입력하세요.
        - group : ***com.example***
        - artifact :  ***config-client***
    * Dependency를 추가하세요.
        - **Actuator**
        - **Config Client**
        - **Web**
        - **DevTools** 

```bash
$ # 2. 프로젝트로 이동
$ # 2-1 이동
$ cd /c/workspace/config-client
$ 
$ # 2-2. bootstrap.properties 로 변경
$ mv src/main/resources/application.properties src/main/resources/bootstrap.properties
```

```bash
$ # 3. Eclipse로 import
$ # 3-1. Application 수정 ( ConfigClientApplication.java )
$ # 3-2. property 수정 ( bootstrap.properties )
```

* 3-1. Application 수정 :  
@Value 어노테이션에 property key를 지정하세요. 
```java
@SpringBootApplication
public class ConfigClientApplication {
	public static void main(String[] args) {
		SpringApplication.run(ConfigClientApplication.class, args);
	}
	@RestController
	class ConfigServerTestController{
		@Value("${app.title: Unknown}")
		private String title;
		@RequestMapping("/title")
		String getTitle() {
			return this.title;
		}
	}
}
```

* 3-2. property 수정 :   
spring.cloud.config.uri 를 설정하세요.  
```yml
spring.application.name: demo
spring.cloud.config.uri: http://localhost:8888
``` 

```bash
$ # 4 테스트
$ # 4-1. config-client 실행
$ # mvn spring-boot:run
$ 
$ # 4-2. config-client 체크
$ # curl localhost:8080/title
```

* 4-1. config-client 실행:
    Spring Boot Maven Plugin으로 실행할 때는 *spring-boot.run.profiles* 를 통해 profile를 지정할 수 있습니다.  
    Executable Jar로 실행할 때는 *spring.profiles.active* 를 통해서 profile을 지정할 수 있습니다. 
    * mvn spring-boot:run
    * mvn spring-boot:run -Dspring-boot.run.profiles=dev
    * mvn spring-boot:run -Dspring-boot.run.profiles=prod
    * java -jar config-client.jar
    * java -jar config-client.jar --spring.profiles.active=dev
    * java -jar config-client.jar --spring.profiles.active=prod

* 4-2. config-client 체크
    * http://localhost:8080/title

### etc

```bash
cd /c/workspace
```

```yml
server.port=8888
spring.application.name=config-server
# 
spring.cloud.config.server.git.search-paths='{application}'
spring.cloud.config.server.encrypt.enabled=false
spring.security.user.password= 
encrypt.failOnError=false
encrypt.key=yujin
encrypt.keyStore.location=classpath:server.jks
encrypt.keyStore.password=changeit
encrypt.keyStore.alias=poscoict
encrypt.keyStore.secret=changeit
```

```
curl localhost:8888/encrypt -d user
```
![Image](https://docs.pivotal.io/spring-cloud-services/2-0/common/config-server/images/config-server-fig1.png)

## Ref. 참고

* [Spring Cloud Config](http://spring.io/projects/spring-cloud-config)
* [http://blog.leekyoungil.com/?p=352](http://blog.leekyoungil.com/?p=352)
* [https://docs.pivotal.io/spring-cloud-services/2-0/common/config-server/index.html](https://docs.pivotal.io/spring-cloud-services/2-0/common/config-server/index.html)
* [Common application properties](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#common-application-properties)

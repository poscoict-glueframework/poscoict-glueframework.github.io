# Spring Security

Glue Maven Project 의 pom.xml 에 `spring-boot-starter-security` dependency 를 추가합니다.

```xml
<project ...>
	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-security</artifactId>
		</dependency>
        ...
```

WebSecurityConfigurerAdapter 을 extends한 클래스에 @EnableWebSecurity 를 추가합니다. 

```java
@EnableWebSecurity
public class WebSecurityConfig extends WebSecurityConfigurerAdapter{

}
```

[HttpSecurity](https://docs.spring.io/spring-security/site/docs/5.1.2.RELEASE/reference/htmlsingle/#jc-httpsecurity) 를 수정합니다.

```java
@EnableWebSecurity
public class WebSecurityConfig extends WebSecurityConfigurerAdapter{
    @Override
    protected void configure( HttpSecurity http ) throws Exception
    {
		http
            .authorizeRequests().anyRequest().authenticated()
            .and().formLogin()
            .and().httpBasic();
    }
}
```

Authorize Requests 를 정의합니다.

```java
@EnableWebSecurity
public class WebSecurityConfig extends WebSecurityConfigurerAdapter{
    @Override
    protected void configure( HttpSecurity http ) throws Exception
    {
		http
            .authorizeRequests()
                .antMatchers("/resources/**", "/signup", "/about").permitAll()
                .antMatchers("/admin/**").hasRole("ADMIN")
                .antMatchers("/db/**").access("hasRole('ADMIN') and hasRole('DBA')")
                .anyRequest().authenticated()
            .and().formLogin()
            .and().httpBasic();
    }
}
```


```java
@EnableWebSecurity
public class WebSecurityConfig extends WebSecurityConfigurerAdapter{
	@Override
    protected void configure( AuthenticationManagerBuilder auth ) throws Exception
    {
        this.logger.trace( "##### configure(auth)" );
        auth.authenticationProvider( authenticationProvider() );
    }
}
```

참고사이트
* [https://www.baeldung.com/spring-boot-security-autoconfiguration](https://www.baeldung.com/spring-boot-security-autoconfiguration) 
* [https://docs.spring.io/spring-security/site/docs/5.1.2.RELEASE/reference/htmlsingle/#appendix-schema](https://docs.spring.io/spring-security/site/docs/5.1.2.RELEASE/reference/htmlsingle/#appendix-schema)
* [https://oddpoet.net/blog/2017/04/27/cors-with-spring-security/](https://oddpoet.net/blog/2017/04/27/cors-with-spring-security/)
* [https://www.baeldung.com/spring-security-authentication-with-a-database](https://www.baeldung.com/spring-security-authentication-with-a-database)
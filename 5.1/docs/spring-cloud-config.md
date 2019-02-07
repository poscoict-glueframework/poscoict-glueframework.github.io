# Spring Cloud Config

## Config Server



```yml
server.port=8888
spring.application.name=config-server

# git uri는 2가지 유형으로 ( remote Git, local window Git, local ubuntu git ) 
spring.cloud.config.server.git.uri=https://github.com/poscoict-glueframework/msa-service-config.git
spring.cloud.config.server.git.uri=file://C:/config-repo
spring.cloud.config.server.git.uri=file://home/jinia/config-repo
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
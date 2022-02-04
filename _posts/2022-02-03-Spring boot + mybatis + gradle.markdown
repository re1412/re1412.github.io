---
layout: post
title: Spring boot + mybatis + gradle
date: 2022-02-03 10:03:00 +0900
category: java
---
# gradle 의존성 설정을 통한 mybatis 적용
> build.gradle 추가
```java
dependencies {
    //Mybatis 라이브러리 dependencies 추가
    implementation 'org.mybatis.spring.boot:mybatis-spring-boot-starter:2.2.0'
    runtimeOnly 'mysql:mysql-connector-java:8.0.25'
}
```


# application.propertis 파일 DataSource 설정(mysql)
```java
spring.datasource.driver=com.mysql.cj.jdbc.Driver
spring.datasource.jdbc-url=jdbc:mysql://localhost:3306/app_schema?&serverTimezone=UTC&autoReconnect=true&allowMultiQueries=true&characterEncoding=UTF-8
spring.datasource.username=root
spring.datasource.password=1234
spring.datasource.mapper-locations=classpath:/mapper/**/*.xml
```

---
layout: post
title: IntelliJ 프로젝트 버전(Execution failed for task ':compileJava') 문제
date: 2020-01-10 13:22:00 +0900
category: java
---
# IntelliJ compileJava error
> IntelliJ JDK 버전차이로 발생하는 에러. Setting 방법.  

<br>
start.spring.io, dependencies : Spring Web, Thymeleaf 설정  
IntelliJ로 spring 프로젝트 open 초기 발생하는 에러, 버전을 맞춰주면 해결된다.  
<br>

1\. File -> Project Structure 설정 - SDK 버전 맞추기  
<img src="/public/img/IntelliJ_compileJava1.png" style="width:100%">  
<br>

2\. File -> Settings 설정 - grandle jvm 맞추기  
<img src="/public/img/IntelliJ_compileJava2.png" style="width:100%">  
*Build and run using 및 Run tests using : Grandle -> 'IntelliJ IDEA'로 변경  
(Build가 Gradle을 통해 실행되기 때문에 속도가 느림. IntelliJ IDEA로 변경하면 Gradle을 통하지 않기 때문에 속도가 빠름)  
<br>

3\. File -> Settings 설정 - Project bytecode version 맞추기  
<img src="/public/img/IntelliJ_compileJava3.png" style="width:100%">  
<br>

4\. File -> Settings 설정 - src/build.gradle파일 안에 sourceCompatibility(자바 버전) 값 맞추기  
<img src="/public/img/IntelliJ_compileJava4.png" style="width:100%">  
<br>

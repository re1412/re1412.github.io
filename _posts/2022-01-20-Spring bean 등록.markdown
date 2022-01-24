---
layout: post
title: Spring bean 등록
date: 2022-01-20 00:00:00 +0900
category: java
---
# Spring bean을 등록하는 방법
> 1. 컴포넌트 스캔과 자동 의존관계 설정(annotation 활용)
  

컴포넌트 스캔 방식
 - annotation = '@'를 붙여서 사용

 
 @Controller, @Service, @Repository를 들어가보면 @Component가 붙어 있음을 확인 가능

 Spring이 올라올 때 @Component와 관련된 annotation이 있으면 모두 Spring이 객체를 생성하여 컨테이너에 등록한다.
  
  
자동 의존관계 설정  
 @Autowired를 통하여 연결함. Controller가 Service를 이용하고 Service가 Repository를 이용할 수 있게 된다.

 위 방법이 컴포넌트 스캔과 자동 의존관계 설정하는 방법이다.
   
  
>2. 자바 코드로 직접 Spring bean 등록


---
layout: post
title: CentOS JAVA 환경변수 
date: 2022-01-24 00:00:00 +0900
category: java
---
# JAVA 설치
>openJDK 1.8설치

```ruby
yum install java-1.8.0-openjdk
yum install java1.8.0-openjdk-devel
```
  
  
    
>환경 변수 등록
경로 확인
```ruby
[root@localhost mannaws]# readlink -f /usr/bin/java
/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.312.b07-1.el7_9.x86_64/jre/bin/java
```
  
  
   
>/etc/profile 내용 수정
```ruby
JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.282.b08-1.el7_9.x86_64
PATH=$PATH:$JAVA_HOME/bin
CLASSPATH=$JAVA_HOME/jre/lib:$JAVA_HOME/lib/tools.jar
export JAVA_HOME PATH CLASSPATH
```  
   
  
 >적용
  ```ruby
  source /etc/profile
  ```
  
     
  
     

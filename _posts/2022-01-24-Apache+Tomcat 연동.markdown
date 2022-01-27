---
layout: post
title: Apache+Tomcat(Spring boot) 연동
date: 2022-01-24 20:03:00 +0900
category: java
---
# CentOS7
```ruby
yum -y install httpd
```

> httpd -v 로 버전확인
>
  
> 방화벽 설정
```ruby
firewall-cmd --permanent --add-service=http  //서비스 추가
firewall-cmd --permanent --add-port=80/tcp  // 80번포트 추가 
firewall-cmd --reload  //적용
```


> 서비스 포트 상태 확인
```ruby
netstat -ntlp | grep httpd
```


> Apache + Tomcat 연동
mod_jk 설치
```ruby
yum -y install gcc gcc-c++ httpd-devel
```


> Tomcat Download탭 -> Tomcat Connectors -> JK x.x.xx Source Release tar.gz 링크 복사
```ruby
wget -c 링크 붙여넣기
tar -zxvf tomcat-connectors-x.x.xx-src.tar.gz
cd native/
```


> apache 확장기능 설치를 도와주는 유틸 경로
```ruby
find / -name apxs   // '/usr/bin/apxs'
./configure --with-apx=[apxs경로]
make && make install
ll /etc/httpd/modules | grep mod_jk.so  // mod_jk.so 확인
```


> selinux 보안 관련 설정 변경
```ruby
chcon -u system_u -r object_r -t httpd_modules_t /etc/httpd/modules/mod_jk.so
```


> apache 설정
> vi /etc/httpd/conf/httpd.conf 변경 (/LoadModule 찾기)
```ruby
LoadModule jk_module modules/mod_jk.so
<IfModule mod_jk.c>
JkWorkersFile conf/workers.properties
JkShmFile run/mod_jk.shm
JkLogFile logs/mod_jk.log
JkLogLevel info
JkLogStampFormat "[%y %m %d %H:%M:%S]"
JkMountFile conf/uriworkermap.properties
</IfModule>

Include conf.modules.d/*.conf
```


> vi /etc/httpd/conf/workers.properties
```ruby
worker.list=contom   //워커 이름 임의 설정(connect tomcat이란 뜻)
worker.contom.port=8009  //워커 이름을 가운데 입력
worker.contom.host=localhost  //포트 번호와 타입은 아래 설정 참고
worker.contom.type=ajp13
worker.contom.lbfactor=1 //tomcat인스턴스 부하 분산 지수, 균등하게 분산하려고 1로 설정
```

> vi [톰캣경로]/conf/server.xml
spring boot 내장 톰캣 사용하여 application.properties에 server.port만 맞춰줌



> vi /etc/httpd/conf/uriworkermap.properties
```ruby
/*=contom
```


> vi /etc/httpd/conf/httpd.conf (/DocumentRoot 검색, /ServerName 검색)
```ruby
DocumentRoot "[톰캣 경로]/webapps/ROOT"
<Directory "[톰캣 경로]/webapps/ROOT">
    AllowOverride None
    # Allow open access:
    Require all granted
</Directory>

#ServerName www.example.com:80
ServerName localhost:80
```


> 마지막으로 selinux 설정
```ruby
chcon -R -t httpd_sys_rw_content_t [톰캣 경로]/webapps/ROOT/
setenforce 0 <- 안해주면 You don't have permission to access / 이런 상황 발생
systemctl start httpd
```
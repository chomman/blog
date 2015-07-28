---
title: nginx와 Tomcat 구성
layout: post
categories:
  - Java
  - Tomcat
  - nginx
tags:
  - tomcat
  - nginx
---

`Linux` 에서 `Tomcat`과 `nginx`를 연동해 사용하려고 할 때 설정.

#### Tomcat

초기 설정대로 8080 포트로 실행한다.


#### nginx

* /etc/nginx/conf.d/default.conf 수정 : location 정보를 추가해 80포트로 들어오는 요청을 8080 포트로 pass한다.

{% highlight properties %}
    location = /50x.html {
        root   /usr/share/nginx/html;
    }
    location ~ \.do$ {
      proxy_pass              http://localhost:8080;
      proxy_set_header        X-Real-IP $remote_addr;
      proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header        Host $http_host;
    }
    location ~ \.jsp$ {
      proxy_pass              http://localhost:8080;
      proxy_set_header        X-Real-IP $remote_addr;
      proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header        Host $http_host;
    }
    location ^~/servlets/* {
      proxy_pass              http://localhost:8080;
      proxy_set_header        X-Real-IP $remote_addr;
      proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header        Host $http_host;
    }
    location ^~/* {
      proxy_pass              http://localhost:8080;
      proxy_set_header        X-Real-IP $remote_addr;
      proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header        Host $http_host;
    }
{% endhighlight %} 



#### nginx Load Balancer

* 만약 여러대의 서버로 구성된 애플리케이션 서버들이 있고 그 앞에 LB용(세션 정보 공유) 서버가 있다면 아래와 같이 upstream 정보로 서버 ip를 나열하고 proxy_pass로 upstream 정보를 입력한다.

{% highlight properties %}
upstream backend {
    ip_hash;
    server 210.122.7.224:80;
}

server {
    listen       80;
    location /resources/ {
        alias   /home/townus/resources/;
        autoindex off;
        access_log off;
        expires max;
    }
    location / {
        #root   /usr/share/nginx/html;
        #index  index.html index.htm;
        proxy_set_header Host $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_pass  http://backend;
    }
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }
{% endhighlight %} 
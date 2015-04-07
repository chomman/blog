---
title: Spring Boot에서 Log4j.xml 사용
layout: post
categories:
  - Java
  - Log4j
  - Spring
tags:
  - spring
  - spring boot
  - log4j
  - log4j.xml
---

Spring Boot를 이용해 손쉽게 웹개발 환경을 마련할 수 있다. 하지만 Logback을 이용하는 것이 아니라 Log4j.xml을 이용해 로깅 설정을 하고 싶다면 다음과 같이 의존성을 관리해주면 된다. 이 설정은 Maven을 이용한 경우이다.


### Maven

{% highlight xml %}
	<dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-actuator</artifactId>
        <version>1.2.3.RELEASE</version>
        <exclusions>
            <exclusion>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-logging</artifactId>
            </exclusion>
        </exclusions>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <version>1.2.3.RELEASE</version>
        <exclusions>
            <exclusion>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-logging</artifactId>
            </exclusion>
        </exclusions>
    </dependency>
{% endhighlight %} 
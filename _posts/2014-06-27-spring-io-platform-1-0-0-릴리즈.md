---
title: Spring IO Platform 1.0.0 릴리즈
layout: post
categories:
  - Java
  - Programming
  - Spring Framework
tags:
  - Bill-of-Materials release
  - BOM
  - DSL
  - grails
  - spring
  - spring boot
  - spring io
  - spring io platform
  - spring io 플랫폼
---
Spring IO Platform 1.0.0 이 릴리즈되었다는 소식이 들려온다.

<a href="http://spring.io/platform" target="_blank">http://spring.io/platform</a>  
Spring IO 플랫폼의 홈페이지로 도표와 함께 소개가 되어 있다.  
IO의 기반을 이루는 기술들은 응용 프로그램을 만들기 위해 필요한 스프링 진영의 여러 기술들을 응집력있게 모아놓고 이를 IO Foundation 이라 부르고 있다.  
IO 실행레이어는 아직 미포함되었지만 포함 예정인 Spring XD, 이제 버전 1.2를 릴리즈한 Spring Boot, 그리고 Grails로 DSL을 지원하기 위해 모인 삼총사 같은 모습이다.

<img style="line-height: 1.5em;" alt="" src="http://spring.io/img/platform-stack.png" width="623" height="547" />

도표를 보면 딱 드는 느낌은 &#8220;뭐야? Spring 프로젝트를 다 모아놓은 거네.&#8221; 
실제로 Spring IO 1.0은 현재 Spring XD를 제외한 모든 스프링 프로젝트를 다 포함하고 있다.
다만 현대적인 응용 프로그램 개발을 위해 모두가 조화롭게 힘을 합쳤다는 데 그 의미가 있지 않나 싶다.  
코어 스프링 API와 의존성을 가지고 있는 여러 라이브러리도 테스트를 거쳐 함게 제공하고 있다고 한다.  
하나의 플랫폼 안에서 웹개발, 웹소켓, REST 기반 웹, 모바일, 빅데이터 개발 등을 같이 할 수 있다는 하니 훨씬 간편하게 개발할 수 있지 않을까 생각해 본다.


###Spring IO Platform Reference Guide  


<a href="http://docs.spring.io/platform/docs/current-SNAPSHOT/reference/htmlsingle/#getting-started-using-spring-io-platform-maven" target="_blank">http://docs.spring.io/platform/docs/current-SNAPSHOT/reference/htmlsingle/#getting-started-using-spring-io-platform-maven</a>  

Spring IO 플랫폼을 사용하기 위한 레퍼런스 페이지로 Maven과 Gradle을 이용해 Spring IO 플랫폼을 세팅하는 방법과 의존성 라이브러리의 버전을 소개하고 있다.

아래는 1.0.0 버전이 릴리즈되었다고 소개하고 있는 스프링 사이트의 블로그 포스트  
<a href="https://spring.io/blog/2014/06/26/spring-io-platform-1-0-0-released" target="_blank">https://spring.io/blog/2014/06/26/spring-io-platform-1-0-0-released</a>

이 포스트에서 소개하고 있는 Spring IO Platform 1.0.0 Release 의 특징은 다음과 같다.

  * A Bill-of-Materials release (a Maven BOM dependency)
  * Spring IO represents curated and harmonized dependencies that just work together &#8211; tests cover all the Spring projects and lots of popular 3rd party open source
  * One platform, many workloads &#8211; build web (HTML-, websocket-, and REST-powered web apps), mobile, integration, batch, reactive or big data applications, or just great APIs
  * Radically simplified development experience with Spring Boot
  * Production-ready features provided out of the box (monitoring, metrics, etc)
  * Modular platform that allows developers to deploy only the parts they need
  * True portability across standalone JVM, embedded runtimes, full-blown Java EE application server, and PaaS deployments like Cloud Foundry
  * Depends only on Java SE, and supports Groovy, Grails and some Java EE
  * Works with your existing dependency management tools such as Maven and Gradle
  * The Spring IO Platform is certified to work on JDK 7 and 8 (though individual projects may support older JDKs on a project-by-project basis)
  * Ideal platform for building next generation, micro-service style architecture

  
  
스프링 블로그 포스트에서 소개하는 소스 코드를 따라 코딩해 보았다.  
<a href="https://spring.io/blog/2014/06/26/introducing-the-spring-io-platform" target="_blank">https://spring.io/blog/2014/06/26/introducing-the-spring-io-platform</a>

잘 돌아간다. <a href="https://github.com/chomman/tutorials/tree/master/spring-io-platform-tutorial/spring-io-platform-hello" target="_blank">Github</a>에도 올려둔다.


####Tutorial

**pom.xml**

{% highlight xml %}
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.haeny.tutorial</groupId>
	<artifactId>spring-io-platform-tutorial</artifactId>
	<version>0.0.1-SNAPSHOT</version>

	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
	</dependencies>

	<dependencyManagement>
		<dependencies>
			<dependency>
				<groupId>io.spring.platform</groupId>
				<artifactId>platform-bom</artifactId>
				<version>1.0.0.RELEASE</version>
				<type>pom</type>
				<scope>import</scope>
			</dependency>
		</dependencies>
	</dependencyManagement>

</project>
{% endhighlight %}


**Application.java**

{% highlight java %}
package com.haeny.tutorial.springio;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.EnableAutoConfiguration;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

/**
 * @author Taehyun Jung
 * 
 */
@Configuration
@EnableAutoConfiguration
@RestController
public class Application {

	public static void main(String[] args) {
		SpringApplication.run(Application.class, args);
	}

	@RequestMapping("/hello/{name}")
	String hi(@PathVariable String name) {
		return "Hello, " + name + "!";
	}
}
{% endhighlight %}


예제는 Spring Boot를 이용해 REST 앱을 만드는 것밖에 없다. 하지만 저렇게 간단한 pom.xml 설정만으로 JVM 기반의 수많은 개발을 할 수 있다는 사실에 편해진 느낌이다. 앞으로 Spring의 방향은 이런 것인 듯.


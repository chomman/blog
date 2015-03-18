---
title: 메이븐 테스트 생략
layout: post
categories:
  - Java
  - Tool
  - Maven
tags:
  - maven
  - skip test
---

메이븐 빌드를 할 때 테스트를 하고 싶지 않을 때가 있다.
한 번씩 필요한데 자꾸 잊어버려 정리해 본다.


###1. Command line


    {% highlight text %}
	mvn -Dmaven.test.skip=true
    {% endhighlight %}

###2. pom.xml


    {% highlight xml %}
   	<properties>
   		<maven.test.skip>true</maven.test.skip>
   </properties>
    {% endhighlight %} 
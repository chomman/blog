---
title: Maven Tomcat plugin에서 Context.xml 설정
layout: post
categories:
  - Java
  - Maven
  - Tomcat
tags:
  - maven
  - tomcat
  - embedded tomcat
  - context.xml
---

Maven Tomcat Plugin을 이용해 웹 어플리케이션을 구동할 때 특정 context.xml 파일을 이용해 환경설정을 하고 싶은 때가 있다.
방법은 아래와 같다.


### Maven

{% highlight xml %}
<build> 
  ...
  <plugin>
    <groupid>org.apache.tomcat.maven</groupid>
    <artifactid>tomcat7-maven-plugin</artifactid>
    <version>2.2</version>
    <systemproperties>
      <java_opts>-XX:MaxPermSize=2G -XX:PermSize=2G</java_opts>
    </systemproperties>
    <configuration>
      <contextfile>LocalDeployment/myApp.xml</contextfile>
    </configuration>
  </plugin>
  ...
</build>
{% endhighlight %} 


### Context.xml

{% highlight xml %}
<build> 
<context path="/myapp" reloadable="false">
  <!-- some  envrionment variables -->
  <environment name="nodeId" override="false" type="java.lang.String" value="node01">
  </environment>
</context>
</build>
{% endhighlight %} 
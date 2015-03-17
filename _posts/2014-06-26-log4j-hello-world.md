---
title: Log4j Hello World
layout: post
categories:
  - Java
  - Log4j
  - Programming
tags:
  - BasicConfigurator
  - eclipse
  - hello world
  - log4j
  - maven
---
Java 개발자라면 <a href="http://logging.apache.org/log4j/1.2/" target="_blank">Log4j</a>는 다들 알 것입니다. 로깅을 위한 간단한 프레임워크이며 수많은 오픈소스에서 사용되고 있는 유명한 개발도구죠.

이 포스트에서는 maven을 이용해 Log4j를 다운받고 Log4j 로그를 통해 Hello World! 를 찍어보고자 합니다.

해당 소스는 본인의<a href="https://github.com/chomman/tutorials/tree/master/log4j-tutorial" target="_blank"> Github Repository</a>에서도 볼 수 있습니다.

&nbsp;

### 1. 메이븐 프로젝트 생성하기

이클립스와 함께 메이븐 플러그인을 사용한다면

New > Maven Project 를 클릭해 간단히 프로젝트를 생성할 수 있습니다.

CLI 를 이용해 생성하고자 한다면 아래와 같이 하면 되겠습니다.

{% highlight text %}
mvn archetype:generate -DgroupId=your.domain java -DartifactId=YourProject
 -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
{% endhighlight %}


### 2. pom.xml 파일에 log4j 라이브러리 추가하기

{% highlight xml %}
<dependency>
    <groupId>log4j</groupId>
    <artifactId>log4j</artifactId>
    <version>1.2.17</version>
</dependency>
{% endhighlight %}


### 3. BasicConfigurator 를 이용해 Hello World 찍기

{% highlight java %}
package com.haeny.tutorial.log4j;

import org.apache.log4j.BasicConfigurator;
import org.apache.log4j.Logger;

public class HelloWorld {

	static final Logger logger = Logger.getLogger(HelloWorld.class);

	public static void main(String[] args) {
		BasicConfigurator.configure();
		logger.debug("Hello World!");
	}
}
{% endhighlight %}



여기까지 했다면 아래와 같은 결과가 콘솔에 찍힐 것입니다.

{% highlight text %}0 [main] DEBUG com.haeny.tutorial.log4j.HelloWorld  - Hello World!{% endhighlight %}


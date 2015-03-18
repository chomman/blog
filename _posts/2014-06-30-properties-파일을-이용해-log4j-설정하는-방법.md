---
title: properties 파일을 이용해 Log4J 설정하는 방법
layout: post
categories:
  - Java
  - Log4j
  - Programming
tags:
  - appender
  - category
  - configuration
  - layout
  - log4j
  - main
  - maven
  - properties
  - PropertyConfigurator
  - 설정
  - 세팅
---
log4j를 설정하는 방법은 일반적으로 두가지인데 xml 파일을 이용하는 방법과 properties파일을 이용하는 방법이 있다.

이 포스트에서는 properties 파일을 이용해 설정하는 방법을 알아보도록 하자.

해당 소스는 <a href="https://github.com/chomman/tutorials/tree/master/log4j-tutorial/2-propertiest-setup" target="_blank">Github</a>에서 다운로드 할 수 있다.



###1) maven을 이용해 java 프로젝트를 만들고 log4j 의 의존성을 기술

이에 대한 자세한 설명은 [이전 포스트][1]를 참고.


###2) log4j.properties 파일을 생성  

* maven을 이용할 경우 src/main/resources 아래 위치시킨다

이 파일은 lg4j 프레임워크가 사용하는 설정 파일이다. log4j가 런타임 시 로그를 기록할 때 사용되는 appender 정보와 로그 레벨 정보, 로그가 기록될 파일의 이름이나 로그정책 등이 모두 이 파일에 기록된다.  
log4j는 크게 3가지 요소로 구성되며 그 구조는 다음과 같습니다.

1. Logger Category : 로깅 메세지를 Appender에 전달한다.  
2. Appender : 전달된 로깅 메세지를 어떠한 output으로 내보낼지 설정한다. 예를 들어 파일에 출력할 것인지 콘솔로 출력할 것인지를 결정한다.  
3. Layout : 로깅을 출력할 때 어떠한 문자형식으로 출력할지 설정한다.

예시를 보자.

{% highlight properties %}
#최상위 카테고리에 DEBUG 레벨로 consoleAppender와 fileAppender에 로구를 출력하겠다고 선언
log4j.rootLogger=DEBUG, consoleAppender, fileAppender
#ConsoleAppender의 이름을 consoleAppender로 정의
log4j.appender.consoleAppender=org.apache.log4j.ConsoleAppender
#consoleAppender의 Layout을 PatternLayout으로 설정
log4j.appender.consoleAppender.layout=org.apache.log4j.PatternLayout
#로그출력패턴을 정의
log4j.appender.consoleAppender.layout.ConversionPattern=%d %-5p [%t] %-17c{2} (%13F:%L) %3x - %m%n
#RollingFileAppender 의 이름을 fileAppender로 정의
log4j.appender.fileAppender=org.apache.log4j.RollingFileAppender
log4j.appender.fileAppender.layout=org.apache.log4j.PatternLayout
log4j.appender.fileAppender.layout.ConversionPattern=%d %-5p [%t] %-17c{2} (%13F:%L) %3x - %m%n
#fileAppender가 로그를 남길 파일명을 test.log로 설정
log4j.appender.fileAppender.File=test.log
{% endhighlight %}


###3) 응용 프로그램에서 테스트  

테스트를 위해 소스를 짜고 로그가 찍히는지 보자.  
maven의 src/main/resource 는 클래스패스가 자동으로 잡혀있기 때문에 따로 설정파일을 읽어올 필요가 없다.
만약 설정파일을 수동으로 가져와야 하는 경우라면 다음 코드를 추가해야 한다.

{% highlight java %}
import org.apache.log4j.PropertyConfigurator;
...
PropertyConfigurator.configure("log4j.properties");
{% endhighlight %}

&nbsp;

{% highlight java %}
package com.haeny.tutorial.log4j;

import org.apache.log4j.Logger;

public class PropertiesSettingTest {

    static final Logger logger = Logger.getLogger(PropertiesSettingTest.class);

    public static void main(String[] args) {
        logger.debug("Log4j Propertiest configuration success.");
    }
}
{% endhighlight %}


test.log 파일이 생성되고 로그가 찍혀있는 것을 볼 수 있다.

{% highlight text %}
2014-06-30 10:45:34,863 DEBUG [main] log4j.PropertiesSettingTest (PropertiesSettingTest.java:10) - Log4j Propertiest configuration success.</pre>
{% endhighlight %}


 [1]: http://chomman.github.io/blog/java/log4j/programming/log4j-hello-world/
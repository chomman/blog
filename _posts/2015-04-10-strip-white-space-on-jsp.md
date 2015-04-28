---
title: Jsp에서 공백을 제거하는 방법
layout: post
categories:
  - Java
  - jsp
  - jstl
tags:
  - whitespace
  - 공백
  - 공백 제거
  - jsp
  - jstl
---

`jsp` 를 사용하다 보면 `jstl`이 있던 자리가 `html`로 변경되고 나서 빈줄(whitespace)로 남아있는 것을 보게 된다.
크게 문제는 없지만 깔끔해 보이지도 않고 파일의 용량도 늘어나게 되니 없애고 싶다. 그럴 때 선택할 수 있는 방법이 몇 가지 있다.

#### Jsp에 선언하는 방법 

{% highlight jsp %}
<%@ page trimDirectiveWhitespaces="true" %>
{% endhighlight %} 


#### web.xml에 설정하는 방법

{% highlight xml %}
<jsp-config>
  <jsp-property-group>
    <url-pattern>*.jsp</url-pattern>
    <trim-directive-whitespaces>true</trim-directive-whitespaces>
  </jsp-property-group>
</jsp-config>
{% endhighlight %} 


#### Tomcat의 conf/web.xml에 설정하는 방법

{% highlight xml %}
<init-param>
    <param-name>trimSpaces</param-name>
    <param-value>true</param-value>
</init-param>
{% endhighlight %} 
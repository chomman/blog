---
title: Servlet에서 User-Agent 정보를 손쉽게 찾는 Library
layout: post
categories:
  - Java
  - Programming
tags:
  - servlet
  - user agent
  - user agent util
  - library
---

`Servlet`에서 `Request`의 `User-Agent` 정보를 손쉽게 얻을 수 있는 Library가 있어 정리한다.

http://www.bitwalker.eu/software/user-agent-utils

### Maven Dependency

{% highlight xml %}
<dependency>
   <groupId>eu.bitwalker</groupId>
   <artifactId>UserAgentUtils</artifactId>
   <version>1.16</version>
</dependency>
{% endhighlight %}

### Java Usage

{% highlight java %}
UserAgent userAgent = UserAgent.parseUserAgentString(request.getHeader("User-Agent"));
{% endhighlight %}
---
title: joda.time jstl 사용법
layout: post
categories:
  - Java
  - jsp
  - jstl
tags:
  - joda
  - time
  - format
  - jstl
---

`joda.time` 을 사용할 때 `jstl`을 이용해 포맷팅을 해야 할 때가 있다.
fmt 태그를 이용하려고 하면 에러가 발생한다. 이런 경우 joda 태그 라이브러리를 선언해 사용한다.

#### Jsp에 선언하는 방법 

{% highlight xml %}
<%@taglib prefix="joda" uri="http://www.joda.org/joda/time/tags" %>
...
<joda:format value="${review.creationTime}" pattern="yyyy.MM.dd"/>
...
{% endhighlight %} 
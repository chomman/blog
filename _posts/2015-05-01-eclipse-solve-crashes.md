---
title: 이클립스에서 `populate auto detected configs` 반응이 없을 때 해결방법
layout: post
categories:
  - eclipse
tags:
  - crash
---

`eclipse` 는 정말 좋은 `IDE`지만 개발자의 속을 썩이는 여러 경우가 있다. 
그 중 한가지, `populate auto detected configs` 가 지속되지 않고 아무 반응도 없는 경우 해결방법이다.

#### eclipse.ini 파일에 다음 설정을 추가하고 재시작한다

{% highlight ini %}
<%@taglib prefix="joda" uri="http://www.joda.org/joda/time/tags" %>
...
-clearPersistedState
...
{% endhighlight %} 
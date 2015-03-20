---
title: Spring Security를 이용하여 사용자의 정보를 찾는 방법
layout: post
categories:
  - Spring Framework
tags:
  - principal
  - security
  - SecurityContextHolder
  - spring
  - user
  - 사용자
---
`Spring Security`를 사용하다 보면 현재 세션 사용자의 정보를 알아야 하는 경우가 발생한다.  
그런 경우 다음 방법을 사용할 수 있다.


### 1. SpringContextHolder를 이용하는 방법

{% highlight java %}
Authentication authentication = SecurityContextHolder.getContext().getAuthentication();
System.out.println(authentication.getName());
{% endhighlight %}

### 2. Controller 의 경우 메서드 인자로 받는 방법

{% highlight java %}
	@RequestMapping("/")
    public String index(Principal principal) {
        System.out.println(principal.getName());
        return "index";
    }
{% endhighlight %}

### 3. User 클래스로 형변환하여 정보를 조회하는 방법

{% highlight java %}
User user = (User) SecurityContextHolder.getContext().getAuthentication().getPrincipal();
System.out.println(user.getUsername());
{% endhighlight %}

&nbsp;  
이때 `User` 클래스는 `org.springframework.security.core.userdetails.User`이다.

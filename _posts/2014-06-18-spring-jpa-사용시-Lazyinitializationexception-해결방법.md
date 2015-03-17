---
title: Spring + JPA 사용시 LazyInitializationException 해결방법
layout: post
categories:
  - Java
  - Programming
  - Spring Framework
tags:
  - java
  - jpa
  - LazyInitializationException
  - OpenEntityManagerInViewFilter
  - OpenSessionInViewFilter
  - spring
---
JPA를 사용하다 보면 @OneToMany나 @ManyToMany 등의 어노테이션을 이용해 객체간 관계를 설정해 줘야 할 때가 있다. 이런 경우 부모자식 관계가 맺어져 하위 객체가 List나 Set과 같은 가변배열이 되는데 toString() 메서드를 이용해 출력을 하려다 보면 다음과 같은 LazyInitializationException 이 발생하게 된다.

{% highlight text %}
org.hibernate.LazyInitializationException: failed to lazily initialize a collection of role
{% endhighlight %} 

Hibernate를 이용하는 경우 web.xml에 OpenSessionInViewFilter 클래스를 적용해 해결할 수 있다.

{% highlight xml %}
<filter> 
    <filter-name>openSessionInViewFilter</filter-name> 
    <filter-class>org.springframework.orm.hibernate3.support.OpenSessionInViewFilter</filter-class> 
</filter> 

<filter-mapping> 
    <filter-name>openSessionInViewFilter</filter-name> 
    <servlet-name>yourAction</servlet-name> 
</filter-mapping>
{% endhighlight %} 

하지만 Spring에서 JPA만을 사용한다면 위의 방법으로 해결되지 않는다. 이런 경우 Spring orm에서 제공하는 OpenEntityManagerInViewFilter를 적용해 문제를 해결할 수 있다.

{% highlight xml %}
<filter>
    <filter-name>OpenEntityManagerInViewFilter</filter-name>
    <filter-class>org.springframework.orm.jpa.support.OpenEntityManagerInViewFilter</filter-class>
</filter>

<filter-mapping>
    <filter-name>OpenEntityManagerInViewFilter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
{% endhighlight %} 

물론 spring-orm-X.X.X.jar 가 있어야 한다. 메이븐을 사용한다면 아래 의존성 코드를 추가하면 되겠다.

{% highlight xml %}
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-orm</artifactId>
    <version>${spring.ver}</version>
</dependency>
{% endhighlight %} 

만약 XML이 아닌 Java Config를 사용한다면 WebApplicationInitializer에 아래처럼 코딩해 web.xml과 동일한 설정을 할 수 있다.

{% highlight java %}
public class ArtresetApplicationConfig implements WebApplicationInitializer {

    @Override
    public void onStartup(ServletContext servletContext) throws ServletException {
        ....
        FilterRegistration.Dynamic openEntityManagerInViewFilter = servletContext.addFilter("openEntityManagerInViewFilter", new OpenEntityManagerInViewFilter());
        openEntityManagerInViewFilter.addMappingForUrlPatterns(dispatcherTypes, true, "/*");

        ....
    }
{% endhighlight %} 
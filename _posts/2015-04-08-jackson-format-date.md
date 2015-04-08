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

`Jackson` 라이브러리를 사용할 때 `@RequestBody` 객체 파라미터  내에 있는 `Date`형 필드로 값을 제대로 전달하는 방법

#### DTO Class 

{% highlight java %}
<build> 
...
	@JsonFormat(shape = JsonFormat.Shape.STRING, pattern = "yyyy-MM-dd", timezon = "GMT+9")
	private Date targetFeild;
...
{% endhighlight %} 


#### Controller Class 

{% highlight java %}
<build> 
...
    @InitBinder    
    public void initBinder(WebDataBinder binder){
    	CustomDateEditor editor = new CustomDateEditor(new SimpleDateFormat("yyyy-MM-dd HH:mm"), true);
        binder.registerCustomEditor(Date.class, editor);
    }
...
{% endhighlight %} 
---
title: JsonFormat을 이용한 Jackson Date 파라미터 전달
layout: post
categories:
  - Java
  - jackson
  - rest
tags:
  - jackson
  - JsonFormat
  - Date format
  - pattern
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
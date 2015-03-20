---
title: Spring Security 로그인 후 이전 페이지로 이동
layout: post
categories:
  - Java
  - Spring security
  - Programming
tags:
  - spring
  - security
  - redirect to previous page after login
  - 로그인 후 이전 페이지로 이동
---

`Spring security`를 사용할 때 특정 페이지에서 인증이 필요하면 로그인 페이지로 리다이렉트를 시키면 된다.
 그런데 로그인 후 첫 페이지로 가는 것이 아니라 원래 이용하려던 서비스 페이지로 가야하는 기능이 필요하다면 `AuthenticationSuccessHandler` 인터페이스를 구현하면 된다.
 물론 로그인 페이지로 이동하는 시점에 원래 페이지를 기억하도록 해야 한다.
실제 소스로 해보자.


### 1. Success Handler 구현

{% highlight java %}
public class CustomLoginSuccessHandler extends SavedRequestAwareAuthenticationSuccessHandler {
    public CustomLoginSuccessHandler(String defaultTargetUrl) {
        setDefaultTargetUrl(defaultTargetUrl);
    }

    @Override
    public void onAuthenticationSuccess(HttpServletRequest request, HttpServletResponse response, 
    	Authentication authentication) throws ServletException, IOException {
        HttpSession session = request.getSession();
        if (session != null) {
            String redirectUrl = (String) session.getAttribute("prevPage");
            if (redirectUrl != null) {
                session.removeAttribute("prevPage");
                getRedirectStrategy().sendRedirect(request, response, redirectUrl);
            } else {
                super.onAuthenticationSuccess(request, response, authentication);
            }
        } else {
            super.onAuthenticationSuccess(request, response, authentication);
        }
    }
}
{% endhighlight %}


### 2. 인증 페이지로 이동하기 전 URL 기억

{% highlight java %}
@RequestMapping(value = "/login", method = RequestMethod.GET)
public String loginPage(HttpServletRequest request) {
    String referrer = request.getHeader("Referer");
    request.getSession().setAttribute("prevPage", referrer);
    return "login";
}
{% endhighlight %}

### 3. Security Config 설정

**Java Config의 경우**

{% highlight java %}
@Override
protected void configure(HttpSecurity http) throws Exception {
    http
        .formLogin()
            .loginPage("/login")
            .successHandler(successHandler())
            .permitAll()
            ...
    ;
}

.
.
.

@Bean
public AuthenticationSuccessHandler successHandler() {
    return new CustomLoginSuccessHandler("/defaultUrl");
}

{% endhighlight %}

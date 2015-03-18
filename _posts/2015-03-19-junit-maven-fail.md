---
title: 이클립스에서 성공한 테스트 케이스가 메이븐 빌드 시 실패한다면
layout: post
categories:
  - Java
  - Tool
  - Maven
tags:
  - maven
  - eclipse
  - surefire
  - 'test fail'
---

정말 희한하게도 `eclipse`에서 모두 성공하는 `jUnit` 단위 테스트가 메이븐 빌드 시 실패를 하는 경우가 있다.
구글링을 해 본 결과 `메이븐 Command line` 명령어를 이용하는 경우 `@Autowired` 테스트 코드가 제대로 작동하지 않는 문제점이 있다고 한다.
테스트를 담당하는 `surefire 플러그인`에 아래와 같은 설정을 해줘서 해결할 수 있다.


{% highlight xml %}
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-surefire-plugin</artifactId>
    <version>2.16</version>
    <configuration>
        <reuseForks>false</reuseForks>
        <forkCount>1</forkCount>
    </configuration>
</plugin>
{% endhighlight %}


`surefire 2.14` 이전 버전에서는 설정이 다음과 같다. 이 설정은 `2.14` 버전에서 `deprecated` 되었다.


{% highlight xml %}
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-surefire-plugin</artifactId>
    <version>2.12</version>
    <configuration>
        <forkMode>always</forkMode>
    </configuration>
</plugin>
{% endhighlight %} 
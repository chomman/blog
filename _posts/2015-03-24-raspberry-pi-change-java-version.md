---
title: 라즈비안(데비안 계열)에서 자바 버전 변경
layout: post
comments: true
categories: 
  - Java
  - Linux
  - Raspberry pi
tags: 
  - change java version
  - debian
  - openjdk
  - rasbian
---

`Raspberry Pi`에 `Rasbian`을 설치하면 이미 `java`가 설치되어 잇다. `Debian` 계열 리눅스 운영체제에는 기본적으로 `OpenJDK`가 깔려있다. 
기본 자바 버전을 변경하고 싶은 경우에 어떻게 해야 할까?
자바를 설치만 한다고 해서 바뀌지 않는다.
[alternative path](http://www.debian-administration.org/article/91/Using_the_Debian_alternatives_system)를 변경하는 방법을 알아보자.

{% highlight ssh %}
$java -version
java version "1.6.0_31"
OpenJDK Runtime Environment (IcedTea6 1.13.3) (6b31-1.13.3-1~deb7u1)
OpenJDK 64-Bit Server VM (build 23.25-b01, mixed mode)
{% endhighlight %}

자바 설치 경로를 살펴보면 다음과 같다.

{% highlight ssh %}
$ ls -lsa /usr/bin/ | grep java
0 lrwxrwxrwx  1 root   root    22 Jul  9 03:50 java -> /etc/alternatives/java
 
$ ls -lsa /etc/alternatives/java
0 lrwxrwxrwx 1 root root 46 Jul 12 23:02  /etc/alternatives/java -> /usr/lib/jvm/java-6-openjdk-amd64/jre/bin/java
{% endhighlight %} 


### 변경방법

####1. 자바 설치

{% highlight ssh %}
$ sudo apt-get install openjdk-7-jdk openjdk-7-jre
{% endhighlight %} 

####2. 자바 alternative path 수정

{% highlight ssh %}
$ sudo update-alternatives --config java
There are 2 choices for the alternative java (providing /usr/bin/java).
 
  Selection    Path                                            Priority   Status

* 0            /usr/lib/jvm/java-6-openjdk-amd64/jre/bin/java   1061      auto mode
  1            /usr/lib/jvm/java-6-openjdk-amd64/jre/bin/java   1061      manual mode
  2            /usr/lib/jvm/java-7-openjdk-amd64/jre/bin/java   1051      manual mode
 
Press enter to keep the current choice[*], or type selection number: 2
update-alternatives: using /usr/lib/jvm/java-7-openjdk-amd64/jre/bin/java 
	to provide /usr/bin/java (java) in manual mode
{% endhighlight %} 


{% highlight ssh %}
$ java -version
java version "1.7.0_55"
OpenJDK Runtime Environment (IcedTea 2.4.7) (7u55-2.4.7-1~deb7u1)
OpenJDK 64-Bit Server VM (build 24.51-b03, mixed mode)
{% endhighlight %}
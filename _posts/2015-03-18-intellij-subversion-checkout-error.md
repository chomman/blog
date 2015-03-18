---
title: Jetbrain 계열 IDE에서 SVN checkout 에러 해결
layout: post
categories:
  - Tool
  - subversion
tags:
  - jetbrain
  - intellij
  - 'android studio'
  - svn
  - checkout
  - error
  - 'Cannot load supported formats: Cannot run program "svn": CreateProcess error=2, The system cannot find the file specified'
  - 'CreateProcess error=2'
  - 'The system cannot find the file specified'
---

안드로이드 스튜디오에서 SVN 체크아웃을 받다가 아래와 같은 에러가 발생했다. 물론 소스는 내려받지 못했다.

    {% highlight text %}
	Cannot load supported formats: Cannot run program "svn": CreateProcess error=2, The system cannot find the file specified
    {% endhighlight %}


나의 경우, Settings -> Version Controll -> Subversion 메누에서

**Use command line client** 체크박스를 해제함으로써 해결할 수 있었다.
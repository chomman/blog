---
title: Windows에서 파일명이 긴 파일 삭제하기
layout: post
categories:
  - Tip
tags:
  - windows
---

`Windows` 운영체제에서 파일 삭제 시 파일명이 너무 긴 경우(디렉토리명 포함) 파일명이 길어서 삭제할 수 없다는 메세지가 나온다.
아주 짜증나는 경우인데  이를 해결하기 위한 유용한 팁이 있다.

{% highlight shell %}
mkdir empty_dir

robocopy empty_dir the_dir_to_delete /s /mir

rmdir empty_dir

rmdir the_dir_to_delete
{% endhighlight %} 

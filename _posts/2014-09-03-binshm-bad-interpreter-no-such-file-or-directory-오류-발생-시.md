---
id: 1422
title: '/bin/sh^M: bad interpreter: No such file or directory 오류 발생 시'
author: 정태현
layout: post
guid: http://monggu.com/?p=1422
permalink: /binshm-bad-interpreter-no-such-file-or-directory-%ec%98%a4%eb%a5%98-%eb%b0%9c%ec%83%9d-%ec%8b%9c/
exclude:
  - 
url:
  - 
hdimage:
  - 
slide_template:
  - default
custom_sidebar:
  - Default
post_video_type:
  - youtube
categories:
  - Linux
---
linux 에서 스크립트 실행할 때  
/bin/sh^M: bad interpreter: No such file or directory  
와 같은 에러 메시지가 나타날 때가 있다.

이것은 십중 팔구 윈도우에서 스크립트 파일을 만든 뒤, linux 에서 실행했기 때문에 나타나는 오류이다.  
정확히는 줄 끝 (줄바꿈)을 의미하는 개행문자가 달라서 발생하는 문제인데 이것의 해결을 위해서는 다음의 방법 중 한 가지로 처리한다.

vi -b

vi 의 바이너리 모드로 들어가면 ^M 이라는 문자가 보인다. 이것을 지워주면 된다.



<!-- SEO Ultimate (http://www.seodesignsolutions.com/wordpress-seo/) - Code Inserter module -->

  
  
<ins class="adsbygoogle" style="display:inline-block;width:728px;height:90px" data-ad-client="ca-pub-4058194403762977" data-ad-slot="4726363844"></ins>  
<!-- /SEO Ultimate -->
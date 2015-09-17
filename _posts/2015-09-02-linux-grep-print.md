---
title: grep 명령어로 앞뒤라인 출력
layout: post
categories:
  - Linux
tags:
  - grep
  - command
---

{% highlight perl %}
$ grep -A10 "keyword" test.txt
{% endhighlight %}

'keyword'가 등장한 라인 다음부터 '-A'뒤의 숫자만큼 즉 열 줄을 더 출력한다.
'-B'는 반대로 그 라인의 윗부분을 그 숫자만큼 출력한다.

참고로, fgrep은 '하나'의 패턴을 찾을 때 grep보다 빠르게 처리한다고 하며,
두 가지 이상의 패턴을 찾을 때는 egrep을 쓰면 좋다.
egrep은 패턴매치를 인식한다. (awk 또한.)
즉 exp+, exp*, exp?, exp1|exp2|exp3 등의 표현을 쓸 수 있다.

'SampleNumber_SampleName.txt' 파일이
1       KFvE004I06
2       KFvE005E20
3       KFvE007F16
........
49      KFvE002E24
50      KFvE003G18
51      KFvE003G24
52      KFvE005A02
....

이렇게 되어있을 때, egrep 사용법은 다음과 같다. 'OR 매치'를 하고 싶으면,

{% highlight perl %}
$  egrep "^50|^51|^52|^53|^58|^61|^63|^84"  SampleNumber_SampleName.txt
{% endhighlight %}

50      KFvE003G18
51      KFvE003G24
52      KFvE005A02
53      KFvE007C11
58      KFvE010B08

{% highlight perl %}
]$ egrep "50|51"  SampleNumber_SampleName.txt
{% endhighlight %}

50      KFvE003G18
51      KFvE003G24
150     KFVH009J24
151     KFVH010E08
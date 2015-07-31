---
title: Java에서 Timezone 정보를 계산하는 방법
layout: post
categories:
  - Java
  - Programming
tags:
  - timezone
---

`Java`에서 `Timezone` 정보를 얻는 방법

{% highlight java %}
import java.util.Date;
import java.util.TimeZone;
import java.util.concurrent.TimeUnit;


/**
 * @author Taehyun Jung
 *
 */
public class TimezoneTest {

	public static void main(String[] args) {
		String timezoneId = TimeZone.getDefault().getID();
	    TimeZone timeZone = TimeZone.getTimeZone("Asia/Seoul");
	    long millis = timeZone.getRawOffset() + (timeZone.inDaylightTime(new Date()) ? timeZone.getDSTSavings() : 0);

	    String timeDiff = String.format("%s%s:%s",
	            millis < 0 ? "-" : "+",
	            String.format("%02d", Math.abs(TimeUnit.MILLISECONDS.toHours(millis))),
	            String.format("%02d", Math.abs(TimeUnit.MILLISECONDS.toMinutes(millis) - TimeUnit.HOURS.toMinutes(TimeUnit.MILLISECONDS.toHours(millis))))
	    );
	    
	    System.out.println("timezoneId = " + timezoneId);
	    System.out.println("timeDifference = " + millis);
	    System.out.println("timeDiff = " + timeDiff);
	}

}
{% endhighlight %}
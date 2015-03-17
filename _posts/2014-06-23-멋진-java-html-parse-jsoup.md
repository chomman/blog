---
title: 멋진 Java Html Parse, Jsoup
layout: post
categories:
  - Java
  - Programming
  - 미분류
tags:
  - css
  - html
  - jquery
  - jsoup
  - library
  - parse
  - parsing
  - selector
---
프로그램을 하다보면 Html을 파싱해야 할 때가 종종 생긴다.  
이때 날코딩으로 파싱을 할 수도 있겠지만 이미 좋은 라이브러리들이 많기 때문에 이를 활용하는 것이 효율적이다. 그 중에서도 최근에 사용해본 Jsoup 라이브러리가 괜찮다고 느껴져 소개하고자 한다.

Jsoup의 홈페이지는 <a href="http://jsoup.org/" target="_blank">http://jsoup.org/</a> 이며 라이브러리를 다운로드할 수 있으며 관련뉴스와 버그정보를 알 수 있다. API 정보와 Cookbook을 찾아볼 수도 있게 되어있으며 실제로 코딩을 해 볼 수도 있도록 되어있다.

Jsoup이 좋다고 느낀 이유는 다름아닌 css Query를 사용할 수 있기 때문이다. jQuery에서 사용하는 셀렉터와 동일한 문법을 이용해 DOM을 손쉽게 찾을 수 있다는 점이 상당히 매력적이다.

예제를 한 번 보도록 하자. 네이버 뉴스 속보 요약 텍스트를 출력하는 예제이다.

{% highlight java%}
import java.io.IOException;

import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

/**
 * @author Taehyun Jung
 *
 */
public class NaverNewsParser {

	public static void main(String[] args) throws IOException {
		Document naverNews = Jsoup.connect("http://news.naver.com/main/list.nhn?mode=LSD&mid=sec&sid1=001").get();
		Elements elements = naverNews.select("ul.type06_headline &gt; li &gt; dl &gt; dt&gt;  a");
		
		for (Element element : elements) {
			System.out.println(element.text());
		}
	}
}
{% endhighlight %}



이상과 같이 손쉬운 선택자를 제공하는 Jsoup이 마음에 든다. 앞으로 HTML 파싱은 이걸로..


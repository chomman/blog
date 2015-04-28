---
title: Javascript Currency(통화) 변경
layout: post
categories:
  - javascript
tags:
  - currency
  - javascript
  - regular expression
---

`javascript` 에서 3자리마다 쉼표를 넣는 정규표현식 


{% highlight javascript %}
function numberWithCommas(x) {
    return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
}
{% endhighlight %} 
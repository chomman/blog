---
title: Android View.OnClickListener 로 파라미터를 전달하는 방법
layout: post
categories:
  - Android
  - Programming
tags:
  - android
  - OnClickListener
  - 'pass parameter to OnClickListener'
---

안드로이드 프로그램을 짜다 보면 View.OnClickListener 인터페이스를 구현해야 할 때가 수도 없이 많이 생긴다.
이 인터페이스를 상속받으면 onClick 메서드를 구현해야 하는데 이 안에서는 바깥 클래스의 변수를 참조하지 못한다.
정확하게 말하면 final 변수가 아닌 변수는 참조하지 못한다.
하지만 개발을 하다보면 필요에 따라 동적변수를 사용해야 하는 경우가 많다.
예를 들면 반복문 안에서 index 변수를 참조해야 하는데 index 변수를 불변값인 final로 지정할 수는 없는 노릇이다.
여러가지 해결방법이 있겠지만 OnClcickListener를 상속받는 새로운 Listener를 만드는 방법이 좋은 것 같다. 


    {% highlight java %}
		import android.view.View;
		
		/**
		 * @author Taehyun Jung
		 */
		public abstract class KnowIndexOnClickListener implements View.OnClickListener {
		
		    protected int index;
		
		    public KnowIndexOnClickListener(int index) {
		        this.index = index;
		    }
		}
    {% endhighlight %}


    {% highlight java %}
        for (int i = 0 ; i < 10 ; i++) {
            anyView.setOnClickListener(new KnowIndexOnClickListener(i) {
            
                @Override
                public void onClick(View v) {
                    Log.i("Parameter", index);
                }
            });
        }
    {% endhighlight %} 
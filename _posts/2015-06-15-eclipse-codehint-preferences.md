---
title: 이클립스에서 코드힌트가 나타나지 않을 때
layout: post
categories:
  - eclipse
tags:
  - code hint
---

`eclipse` 에서 키보드를 잘못 눌렀는지 갑자기 코드 힌트가 작동하지 않았다.
좀더 정확하게 말하면 ctrl + space 키를 눌렀을 때 코드힌드 창은 나타나는데 추천 구문이 나타나지 않는다.
이럴 때 해결방법은 다음과 같다.

Windows > Preferences > Java > Editor > Content Assist > Advanced

설정으로 들어가 제안받고자 하는 종류를 선택한다.
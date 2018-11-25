---
title: ! "[wargame.kr] flee button"
date: 2018-11-25
tags:
  - wargame.kr
  - web
  - flee button
  - chaem
categories:
  - web
---

wargame.kr의 두번째 문제는 flee button이라는 문제이다.  

[wargame.kr홈페이지](http://wargame.kr/challenge)

![]({{ site.baseurl }}/assets/images/wargame.kr/flee_button_01.JPG)  

click 버튼을 클릭하면 되는 문제인 것 같다.

# 풀이

버튼이 마우스에서 일정거리 떨어져서 클릭할 수 없게 계속 움직인다.  

![]({{ site.baseurl }}/assets/images/wargame.kr/flee_button_02.JPG)  

크롬 개발자 도구를 이용하여 본다.  

![]({{ site.baseurl }}/assets/images/wargame.kr/flee_button_03.JPG)  

빨간 상자로 표시해둔 버튼을 이용하면 원하는 UI에 대한 정보를 볼 수 있다.  

이 버튼을 이용하여 click버튼을 더블 클릭해보니, 간단하게 flag가 출력되었다.  

![]({{ site.baseurl }}/assets/images/wargame.kr/flee_button_04.JPG)  

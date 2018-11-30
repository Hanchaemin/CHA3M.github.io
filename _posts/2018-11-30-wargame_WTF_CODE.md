---
title: ! "[wargame.kr] WTF_CODE"
date: 2018-11-30
tags:
  - wargame.kr
  - web
  - whitespace
  - chaem
categories:
  - wargame.kr
---

오늘 풀 문제는 wargame.kr의 WTF_CODE라는 문제이다.  

[wargame.kr홈페이지](http://wargame.kr/challenge)

![]({{ site.baseurl }}/assets/images/wargame.kr/WTF_01.JPG)  

이건 프로그램 언어이며, 소스코드를 보라고 한다.

# 풀이

홈페이지에 접속하면 다음과 같은 화면이 뜬다.  
![]({{ site.baseurl }}/assets/images/wargame.kr/WTF_02.JPG)  
순순히 코드를 다운받아 보았다. 흠! vscode로 일단 열어봐 볼까?  
![]({{ site.baseurl }}/assets/images/wargame.kr/WTF_03.JPG)  
아무것도 없...지 않았다! 뭔가 있는데, 이게 뭐지?! 하고는 `.ws`확장자를 구글에 찾아봤다.  
검색하다가 아래의 글을 발견했다!  
[whitespace에 대해 설명하는 페북글](https://www.facebook.com/HakSec.Story/posts/%EA%B0%95%EC%9D%98hac%EC%95%88%EB%85%95%ED%95%98%EC%84%B8%EC%9A%94-%EB%8B%A4%EC%8B%9C%EB%8F%8C%EC%95%84%EC%98%A8-saynot%EC%9E%85%EB%8B%88%EB%8B%A4%EA%B7%B8%EB%8F%99%EC%95%88-%ED%95%99%EC%83%9D%EC%8B%A0%EB%B6%84%EC%97%90%EC%9E%88%EC%96%B4%EC%84%9C-%ED%8E%98%EC%9D%B4%EC%A7%80-%EA%B4%80%EB%A6%AC%EC%97%90-%EC%9E%88%EC%96%B4%EC%84%9C-%EC%86%8C%ED%99%80%ED%96%88%EC%97%88%EB%8A%94%EB%8D%B0%EB%8B%A4%EC%8B%9C-%EC%B4%88%EC%8B%AC%EC%9D%84-%EA%B0%96%EA%B3%A0-%EA%B8%80%EC%9D%84-%EC%9E%91%EC%84%B1%ED%95%B4%EB%82%98%EA%B0%80%EA%B2%A0%EC%8A%B5%EB%8B%88%EB%8B%A4%EC%98%A4/1238699326155384/)  
오오 `whitespace`라는 언어가 있다고 한다!!  
whitespace 언어에 대해 찾아보니, 위키에도 있었당! 이런 재미있는 언어가 있다닝...  
![]({{ site.baseurl }}/assets/images/wargame.kr/WTF_04.JPG)  
`공백, 탭, 개행문자`로만 이루어진 언어로, 스택에 임의의 정수를 자유롭게 푸쉬하는 `스택기반 명령어 프로그래밍 언어`라고 한당  
자세한 문법은 위키에 잘 나와있당  
[whitespace 위키](https://ko.wikipedia.org/wiki/%ED%99%94%EC%9D%B4%ED%8A%B8%EC%8A%A4%ED%8E%98%EC%9D%B4%EC%8A%A4_(%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D_%EC%96%B8%EC%96%B4))
[whitespace 나무위키](https://namu.wiki/w/%ED%99%94%EC%9D%B4%ED%8A%B8%EC%8A%A4%ED%8E%98%EC%9D%B4%EC%8A%A4)
이런 것이라면 어딘가에 온라인 디코더가 있겠다 싶어서 뒤적뒤적 해보았다.  
그러다가 찾은 내가 원하는 디코더를 발견하였다!  
![]({{ site.baseurl }}/assets/images/wargame.kr/WTF_05.JPG)  
짠~ 코드를 복붙해 넣으니 바로 이렇게 결과를 출력해주었당!  
디코더 링크는 요기!!!  
[whitespace online decoder](https://vii5ard.github.io/whitespace/)  
끗!  

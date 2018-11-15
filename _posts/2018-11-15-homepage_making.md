---
title: ! "홈페이지 제작기"
date: 2018-11-15
tags:
  - homepage
  - web
  - php
  - chaem
categories:
  - web
---

경진대회 홈페이지를 대대적으로 수정하면서, 웹에 한발짝 더 다가섰습니다 ㅎㅎ  
홈페이지를 만들면서 넣었던 기능들 중에 몇가지를 정리해 보고자합니다.  

## php error reporting
홈페이지를 만들면서, 답답했던 부분이 뭐가 잘못되어서 화면이 안나오는 것인지 알려주지 않는다는 것이었습니다 ㅠㅠ  
웹 초보자인 나에겐 이 부분이 고난...  
그래서 php error를 출력해 주는 코드를 많이 이용했습니다.  
```php
error_reporting(E_ALL);

ini_set("display_errors", 1);

```
덧붙이자면, php.ini에서도 error를 출력하도록 설정해 줄 수 있다고 합니다.  

### php.ini 경로 찾기
> php --ini | grep php.ini 이용
```
ubuntu@ubuntu:/var/www$ php --ini | grep php.ini
Configuration File (php.ini) Path: /etc/php/7.0/cli
Loaded Configuration File:         /etc/php/7.0/cli/php.ini
```

php.ini파일에서 `error_reporting = E_ALL & ~E_DEPRECATED & ~E_STRICT` 부분을 보면
`모든 메세지를 보여주되 deprecated 와 notice 메세지는 출력을 하지 마라` 라는 것을 알 수 있습니다.  
이를 수정하여 모든 메시지를 출력해주게 할 수 있지만, 개발할 때만 잠시 사용하는 것을 추천합니다.  

## 쿠키값 암호화

쿠키값을 암호화하지 않으면 쿠키값이 그대로 노출되게 됩니다.  
![]({{ site.baseurl }}/assets/images/homepage_making/homepage_making_01.PNG)  

`editthiscookie`와 같은 프로그램으로 다음과 같은 쿠키 값을 url 디코딩하면 이렇게 정보가 유출되게 됩니다.  
![]({{ site.baseurl }}/assets/images/homepage_making/homepage_making_02.PNG)  

중요한 정보는 없지만 ㅎㅎ 이런 부분도 신경써주면 좋을 것 같습니다!  
저는 그래서 쿠키값을 암호화해 주기위해 mcrypt라는 툴을 사용하였습니다.  
```
root@chaem:~# apt install php-mcrypt
```
이렇게 간단하게 설치하여 이용할 수 있습니다.  
mcrypt를 설치하고 `service apache2 restart`를 하면 바로 적용되었던 것 같습니다.  
서비스를 재시작했는데도 적용이 안된다면 `application/config/config.php`의 다음 설정을 한번 변경해 보시길 바랍니다.  
```php
$config['encrypted cookie'] = TRUE;
```

## auto scroll 기능

rank를 보여줄때, 사용자가 많으면 시야를 벗어나는 랭킹도 생깁니다. 이걸 전광판 용으로 사용하려면 계속해서 자동으로 스크롤해주면 좋겠다 하여...!  
찾아보니 다음과 같은 스크립트를 사용할 수 있었습니다.  
```php
window.setTimeout(function(){ $(".rank").animate({  scrollTop: (window.outerHeight)+(window.outerHeight/10) }, 20 * 1000) }, 7000);
```

아래의 두개의 코드를 참고하여 작성하였습니다.  
```php
setTimeout(function(){ alert("Hello"); }, 3000);
```
참고 링크 : https://www.w3schools.com/jsref/met_win_settimeout.asp

```php
var target_id='#image_point';
$('body, html').css('scrollTop', $(target_id).offset().top);
$('body, html').animate({ scrollTop: $(target_id).offset().top }, 1000);
window.scrollTo(0, $(target_id).offset().top);
```
참고 링크 : http://forum.falinux.com/zbxe/index.php?document_srl=868728&mid=lecture_tip


## php 문법
> php 함수 출력 예시

function foo()
{
    return 'Hi';
}
$my_foo = 'foo';
echo "{$my_foo()}";

> isset() 함수
변수의 존재여부 판단
변수가 존재하면 true, 존재하지 않으면 false return

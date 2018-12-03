---
title: ! "[wargame.kr] login filtering"
date: 2018-11-30
tags:
  - wargame.kr
  - web
  - filtering
  - mysql_query
  - chaem
categories:
  - wargame.kr
---

wargame.kr의 login filtering이라는 문제이다.  

[wargame.kr홈페이지](http://wargame.kr/challenge)

![]({{ site.baseurl }}/assets/images/wargame.kr/login_filtering_01.JPG)  

이 문제는 혼자서 풀이 못하였다 엉엉 ㅠㅠ  
처음에 injection문제인줄 알았으나, `mysql_real_escape_string`함수가 있기때문에 injection 공격은 통하지 않는다고 한다.  
결론부터 말하자면 이 문제는 `mysql은 기본적으로 대소문자를 구분하지 않는다`는 것을 알아야 풀이가 가능한 문제이다.

# 분석

![]({{ site.baseurl }}/assets/images/wargame.kr/login_filtering_02.JPG)

문제에 접속하면 다음과 같이 로그인 창이 나오며, 소스를 볼 수 있습니다.  
해당 소스는 다음과 같습니다.  

```php
<?php

if (isset($_GET['view-source'])) {
    show_source(__FILE__);
    exit();
}

/*
create table user(
 idx int auto_increment primary key,
 id char(32),
 ps char(32)
);
*/

 if(isset($_POST['id']) && isset($_POST['ps'])){
  include("../lib.php"); # include for auth_code function.

  mysql_connect("localhost","login_filtering","login_filtering_pz");
  mysql_select_db ("login_filtering");
  mysql_query("set names utf8");

  $key = auth_code("login filtering");

  $id = mysql_real_escape_string(trim($_POST['id']));
  $ps = mysql_real_escape_string(trim($_POST['ps']));

  $row=mysql_fetch_array(mysql_query("select * from user where id='$id' and ps=md5('$ps')"));

  if(isset($row['id'])){
   if($id=='guest' || $id=='blueh4g'){
    echo "your account is blocked";
   }else{
    echo "login ok"."<br />";
    echo "Password : ".$key;
   }
  }else{
   echo "wrong..";
  }
 }
?>
<!DOCTYPE html>
<style>
 * {margin:0; padding:0;}
 body {background-color:#ddd;}
 #mdiv {width:200px; text-align:center; margin:50px auto;}
 input[type=text],input[type=[password] {width:100px;}
 td {text-align:center;}
</style>
<body>
<form method="post" action="./">
<div id="mdiv">
<table>
<tr><td>ID</td><td><input type="text" name="id" /></td></tr>
<tr><td>PW</td><td><input type="password" name="ps" /></td></tr>
<tr><td colspan="2"><input type="submit" value="login" /></td></tr>
</table>
 <div><a href='?view-source'>get source</a></div>
</form>
</div>
</body>
<!--

you have blocked accounts.

guest / guest
blueh4g / blueh4g1234ps

-->
```

공부도 할겸 소스코드를 분석해 보겠습니당ㅎㅎ  
우선, 처음은 소스코드를 보여주는 코드입니다.  
```php
if (isset($_GET['view-source'])) {
    show_source(__FILE__);
    exit();
}
```

다음은 isset함수로 인자가 있는 것을 확인하여 id와 ps가 있으면 lib.php를 함수에 포함시킨다는 의미입니다.  
```php
if(isset($_POST['id']) && isset($_POST['ps'])){
 include("../lib.php"); # include for auth_code function.
```

그리고 mysql을 사용하기위해 쿼리를 연결시킵니다.  
```php
mysql_connect("localhost","login_filtering","login_filtering_pz");
mysql_select_db ("login_filtering");
mysql_query("set names utf8");
```

사용자가 입력한 id와 ps를 각각 $id와 $ps에 넣고 실행한 명령문을 $row에 기록하도록 합니다.  
```php
$key = auth_code("login filtering");

$id = mysql_real_escape_string(trim($_POST['id']));
$ps = mysql_real_escape_string(trim($_POST['ps']));

$row=mysql_fetch_array(mysql_query("select * from user where id='$id' and ps=md5('$ps')"));
```

여기에서보면, php는 사용자가 입력하는 대소문자를 그대로 입력받는데 db query에서는 대소문자를 구분하지 않고 입력 받기 때문에 대문자를 섞어서 입력하면 if문을 우회할 수도 있고, 로그인도 가능하게 된다.  
```php
if(isset($row['id'])){
 if($id=='guest' || $id=='blueh4g'){
  echo "your account is blocked";
 }else{
  echo "login ok"."<br />";
  echo "Password : ".$key;
 }
}else{
 echo "wrong..";
}
}
```

중간에 html부분은 건너뛰고, 마지막에 보면 주석으로 계정정보가 적혀있어 이가 노출된 것을 알 수 있습니다.  
```php
<!--

you have blocked accounts.

guest / guest
blueh4g / blueh4g1234ps

-->
```

# 풀이

```php
if(isset($row['id'])){
 if($id=='guest' || $id=='blueh4g'){
  echo "your account is blocked";
 }else{
  echo "login ok"."<br />";
  echo "Password : ".$key;
 }
}else{
 echo "wrong..";
}
}
```

따라서 위에서도 언급했듯이, guest / guest 또는 blueh4g / blueh4g1234ps 계정을 사용하되, 대문자를 섞어서 로그인을 하면 위의 if문을 통과할 수 있기때문에 flag를 획득할 수 있습니다.  

![]({{ site.baseurl }}/assets/images/wargame.kr/login_filtering_03.JPG)

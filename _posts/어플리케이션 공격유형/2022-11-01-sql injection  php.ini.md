---
title:  "sql injection 방어" 

categories:
  - appatack
tags:
  - [injection]

toc: true

date: 2022-11-01
last_modified_at: 2022-11-01
---

## sql injection : php.ini

- magic_quotes_gpc 옵션이 on이면, GPC(***GET, POST, COOKIE***)에서

  '(싱글 쿼터), "(더블 쿼터), \(백 슬래시), NULL을 자동적으로 백슬래시로 이스케이프 된다

  ```
  # vi /etc/php.ini
  ```

  ![화면 캡처 2022-11-01 181403](../../assets/img/화면 캡처 2022-11-01 181403.png)

  ```
  # service httpd restart
  ```

- injection 다시 시도

  ```
  ' union select  1,2,3,4,5,6,7,8,9,10,flag from jason.Kh5fM #
  ```

  ![화면 캡처 2022-11-01 181821](../../assets/img/화면 캡처 2022-11-01 181821.png)







## sql injection : mysql_real_escape_string()

- 설정전 로그인 테스트

  ![화면 캡처 2022-11-01 195040](../../assets/img/화면 캡처 2022-11-01 195040.png)

  ![화면 캡처 2022-11-01 195400](../../assets/img/화면 캡처 2022-11-01 195400.png)
  
  ![화면 캡처 2022-11-01 195424](../../assets/img/화면 캡처 2022-11-01 195424.png)
  
- mysql query에서 특수 문자열을 이스케이프하기 위해

  - \x00, \n, \r, \, ', ", \x1a 문자에 백슬래시를 붙임

  ```
  # vi /var/www/html/member/member_login_check.php
  
  $strSQL = mysql_real_escape_string($strSQL);
  ```

  ![화면 캡처 2022-11-01 190733](../../assets/img/화면 캡처 2022-11-01 190733.png)

- 로그인 창에서 테스트

  ![화면 캡처 2022-11-01 190904](../../assets/img/화면 캡처 2022-11-01 190904.png)

  ![화면 캡처 2022-11-01 190918](../../assets/img/화면 캡처 2022-11-01 190918.png)

  

## sql injection : 문자열 필터링

- injection 테스트

  ```
  ' union select 1,2,3,4,5,6,7,8,9,10,SCHEMA_NAME from information_schema.SCHEMATA #
  ```

  ![화면 캡처 2022-11-01 192728](../../assets/img/화면 캡처 2022-11-01 192728.png)

- php 파일 수정

  ```
  $str = $_GET['contents'];
  str_replace("'", "\');
  if(eregi(" |/|\(|\)|\t|\||&|union|select|from|0x",$_GET[no])) exit("no hack");
  if(preg_match("/select|insert|delete|update|drop/i", $str) exit("no hack");
  
  /   /i : 비교시 대소문자 가리지 말것
  if(preg_match("/union|from|limit|information_schema/i", $key)) exit("no hack");
  ```
  
  ```
  # vi /var/www/html/board/board_list.php
  
  if(preg_match("/union|from|limit|information_schema/i", $key)) exit("no hack");
  ```
  
  ![화면 캡처 2022-11-02 184925](../../assets/img/화면 캡처 2022-11-02 184925.png)

- 다시 테스트

  ```
  ' union select 1,2,3,4,5,6,7,8,9,10,SCHEMA_NAME from information_schema.SCHEMATA #
  ```

  ![화면 캡처 2022-11-02 185230](../../assets/img/화면 캡처 2022-11-02 185230.png)
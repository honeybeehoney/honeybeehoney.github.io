---
title:  "Directory Listing" 

categories:
  - injection
tags:
  - [injection]

toc: true

date: 2022-11-01
last_modified_at: 2022-11-01f
---

## Directory Listing

- http://172.16.0.111/board/

![화면 캡처 2022-11-01 193440](../../assets/img/화면 캡처 2022-11-01 193440.png)

- http://172.16.0.111/member/

![화면 캡처 2022-11-01 193553](../../assets/img/화면 캡처 2022-11-01 193553.png)

- 웹서버의 하위 디렉터리 별로 index.html 이 없으면 디렉터리내의 모든 내용이 보여진다

  ```
  [root@localhost html]# cd /var/www/html/member/
  [root@localhost member]# ls
  ```

  ![화면 캡처 2022-11-01 193804](../../assets/img/화면 캡처 2022-11-01 193804.png)

  ```
  [root@localhost member]# echo member > /var/www/html/member/index.html
  [root@localhost member]# ls
  ```

  ![화면 캡처 2022-11-01 193910](../../assets/img/화면 캡처 2022-11-01 193910.png)

  ![화면 캡처 2022-11-01 194013](../../assets/img/화면 캡처 2022-11-01 194013.png)

- httpd 설정 파일

  ```
  [root@localhost member]# grep -n index.html /etc/httpd/conf/httpd.conf
  ```

  ![화면 캡처 2022-11-01 194142](../../assets/img/화면 캡처 2022-11-01 194142.png)

- 차단

  ```
  이전 실습 원복 후
  
  # vim /etc/httpd/conf/httpd.conf
  ```

  ![화면 캡처 2022-11-01 194510](../../assets/img/화면 캡처 2022-11-01 194510-1667299535475-57.png)

- 서비스 재시작후 확인

  ```
  # service httpd restart
  ```

  ![화면 캡처 2022-11-01 194748](../../assets/img/화면 캡처 2022-11-01 194748.png)
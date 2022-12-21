---
title:  docker - image export

categories:
  - docker
tags:
  - [linux, docker, container]

toc: true

date: 2022-11-25
last_modified_at: 2022-11-25
---

## docker : image export

- 실습전 환경 정리

  ```
  $ sudo docker container ps -a
  ```

  ![화면 캡처 2022-11-25 174752](../../assets/img/화면 캡처 2022-11-25 174752.png)

  ```
  $ sudo docker container stop feb5cae4a497
  $ sudo docker container stop 156ce2e71845
  ```

  ![화면 캡처 2022-11-25 174910](../../assets/img/화면 캡처 2022-11-25 174910.png)

  ```
  $ sudo docker ps -a -q
  ```

  ![화면 캡처 2022-11-25 174946](../../assets/img/화면 캡처 2022-11-25 174946.png)

  ```
  $ sudo docker container rm $(sudo docker container  -a -q)
  ```

  

- docker  image 를 tar 로 묶어준다

  ```
  $ sudo docker image ls
  ```

  ![화면 캡처 2022-11-25 175134](../../assets/img/화면 캡처 2022-11-25 175134.png)

  ```
  $ sudo docker image save -o export.tar web_01:1.0
  $ ls
  ```

  ![화면 캡처 2022-11-25 175200](../../assets/img/화면 캡처 2022-11-25 175200.png)

- docker image 삭제

  ```
  $ sudo docker image rm web_01:1.0
  ```

  

- tar 로 묶어놓은 docker image  다시 load

  ```
  $ sudo docker image load -i export.tar
  ```

  ![화면 캡처 2022-11-25 175349](../../assets/img/화면 캡처 2022-11-25 175349.png)
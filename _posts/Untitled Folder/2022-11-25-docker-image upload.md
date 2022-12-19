---
title:  docker : image upload

categories:
  - Docker & Container
tags:
  - [보안,docker,container]

toc: true

date: 2022-11-25
last_modified_at: 2022-11-25
---

## docker : image upload

- [hub.docker.com](http://hub.docker.com/) 로그인

  ![화면 캡처 2022-11-25 175724](../../assets/img/화면 캡처 2022-11-25 175724.png)

- docker hub 에 가입후 ubuntu 터미널에서 로그인 

  ```
  $ sudo docker login
  ```

  ![화면 캡처 2022-11-25 175819](../../assets/img/화면 캡처 2022-11-25 175819.png)

- 이미지 목록 확인

  ```
  $ sudo docker image ls
  ```

  ![화면 캡처 2022-11-25 175349](../../assets/img/화면 캡처 2022-11-25 175349-1669366740408-59.png)

- repository  생성

  ![화면 캡처 2022-11-25 175941](../../assets/img/화면 캡처 2022-11-25 175941.png)

  ![화면 캡처 2022-11-25 180004](../../assets/img/화면 캡처 2022-11-25 180004.png)

  ![화면 캡처 2022-11-25 180031](../../assets/img/화면 캡처 2022-11-25 180031.png)

- image tagging

  - tag 를 이용하여 repository 에 맞게 지정

    ```
    $ sudo docker image tag web_01:1.0 dlsrlrla/webserver:1.0
    $ sudo docker image ls
    ```

    ![화면 캡처 2022-11-25 180238](../../assets/img/화면 캡처 2022-11-25 180238.png)

- image push

  - 추가된  tag 를 지정하여 자신의 저장소(repository) 에 push

    ```
    $ sudo docker image push dlsrlrla/webserver:1.0
    ```

    ![화면 캡처 2022-11-25 180441](../../assets/img/화면 캡처 2022-11-25 180441.png)

    ![화면 캡처 2022-11-25 180532](../../assets/img/화면 캡처 2022-11-25 180532.png)

- image search

  - 주의 : 본인의 리포지터리 명을 입력

    ```
    $ sudo docker search dlsrlrla
    ```

    ![화면 캡처 2022-11-25 180651](../../assets/img/화면 캡처 2022-11-25 180651.png)
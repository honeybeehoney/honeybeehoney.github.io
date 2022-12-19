---
title:  docker : image build

categories:
  - Docker & Container
tags:
  - [보안,docker,container]

toc: true

date: 2022-11-25
last_modified_at: 2022-11-25
---

## docker : image build

#### nginx 의 container 의 html 파일을 추가하여 새로운 image 로 저장

- container run

  ```
  $ sudo docker container run --name web_01 -d -p 80:80 nginx:latest
  
  -d : detach 
  detach 실행 
  실행시 입출력 터미널이 빠져있음 -it 
  ```

  ![화면 캡처 2022-11-25 164646](../../assets/img/화면 캡처 2022-11-25 164646.png)

- ps -a

  ```
  test01@test01-virtual-machine:~$ sudo docker container ps -a
  ```

  ![화면 캡처 2022-11-25 164752](../../assets/img/화면 캡처 2022-11-25 164752.png)

- 서비스 확인

  ![화면 캡처 2022-11-25 164820](../../assets/img/화면 캡처 2022-11-25 164820.png)

- web_01 container 에 attach

  ```
  test01@test01-virtual-machine:~$ sudo docker container attach web_01
  
  반응이 없어서 ctrl + c 또는 ctrl +z 
  ```

  ![화면 캡처 2022-11-25 165301](../../assets/img/화면 캡처 2022-11-25 165301.png)

- 의도하지 않은 컨테이너의 종료가 있었다

  ```
  $ sudo docker container ps -a
  ```

  ![화면 캡처 2022-11-25 165359](../../assets/img/화면 캡처 2022-11-25 165359.png)

  ```
  $ sudo docker container start 0dc62d0c7af6   -> nginx의 컨테이너 id
  $ sudo docker container ps -a
  ```

  ![화면 캡처 2022-11-25 165638](../../assets/img/화면 캡처 2022-11-25 165638.png)

- detach 모드로 실행된 컨테이너에 접근할때는 exec : 이미 실행된 컨테이너에서 해당명령을 실행

  ```
  $ sudo docker container exec -it web_01 /bin/bash
  ```

- webserver contents 디렉터리를 찾기

  ```
  # find / -name html
  ```

  ![화면 캡처 2022-11-25 170025](../../assets/img/화면 캡처 2022-11-25 170025.png)

  ```
  # ls -al /usr/share/nginx/html/
  ```

  ![화면 캡처 2022-11-25 170147](../../assets/img/화면 캡처 2022-11-25 170147.png)

- web_01 컨테이어 html 파일 확인

  ```
  # cat /usr/share/nginx/html/index.html
  ```

  ![화면 캡처 2022-11-25 170237](../../assets/img/화면 캡처 2022-11-25 170237.png)

- 기존 index.html 이름 변경으로 백업 후 새로운 index.html 을 만들기

  ```
  # mv ./index.html ./index.html.bak
  ```

  ![화면 캡처 2022-11-25 170604](../../assets/img/화면 캡처 2022-11-25 170604.png)

- index.html 파일 생성

  ```
  # echo web_01 > index.html
  # cat index.html
  ```

  ![화면 캡처 2022-11-25 170711](../../assets/img/화면 캡처 2022-11-25 170711.png)

  ![화면 캡처 2022-11-25 170732](../../assets/img/화면 캡처 2022-11-25 170732.png)

- ctrl + p  + q

  ```
  $ sudo docker container ps -a
  ```

  ![화면 캡처 2022-11-25 170829](../../assets/img/화면 캡처 2022-11-25 170829.png)

- 현재 컨테이너(기존 이미지에 추가된)의 내용을 새로운 이미지로 commit 

  ```
  $ sudo docker image ls
  ```

  ![화면 캡처 2022-11-25 171028](../../assets/img/화면 캡처 2022-11-25 171028.png)

  ```
  $ sudo docker commit -a "dlsrlrla" web_01 web_01:1.0
  ```

  ![화면 캡처 2022-11-25 171113](../../assets/img/화면 캡처 2022-11-25 171113.png)

  ```
  $ sudo docker image ls
  ```

  ![화면 캡처 2022-11-25 171139](../../assets/img/화면 캡처 2022-11-25 171139.png)

- 이미지의 내부 설정을 확인

  ```
  $ sudo docker image inspect web_01:1.0
  ```

  ![화면 캡처 2022-11-25 171312](../../assets/img/화면 캡처 2022-11-25 171312.png)

#### 새로 생성된 image 를 reference 하여 새로운 컨테이너를 생성 

- 기존 컨테이너 종료후 새롭게 만들어진 이미지로 컨테이너를 생성

  - 80 포트 중복 문제 해결

    ```
    $ sudo docker container ps -a
    ```

    ![화면 캡처 2022-11-25 171849](../../assets/img/화면 캡처 2022-11-25 171849.png)

  - web_01:1.0 이미지를 참조하여 컨테이너 실행 

    ```
    $ sudo docker image ls
    ```

    ![화면 캡처 2022-11-25 171948](../../assets/img/화면 캡처 2022-11-25 171948.png)

    ```
    $ sudo docker container run --name web_02 -d -p 80:80 web_01:1.0
    ```

    ![화면 캡처 2022-11-25 172044](../../assets/img/화면 캡처 2022-11-25 172044.png)

    ```
    $ sudo docker container ps
    ```

    ![화면 캡처 2022-11-25 172128](../../assets/img/화면 캡처 2022-11-25 172128.png)

#### 새로 생성된 이미지로 컨테이너 생성시 포트번호 다르게 

- 구성도

  ![Untitled (7)](../../assets/img/Untitled (7).png)

- 이미 포트 할당되어 있어서 실행 불가

  ```
  $ sudo docker container run --name web_02_clone -d -p 80:80 web_01:1.0
  ```

  ![화면 캡처 2022-11-25 173505](../../assets/img/화면 캡처 2022-11-25 173505.png)

  ```
  $ sudo docker container ps -a
  ```

  ![화면 캡처 2022-11-25 173722](../../assets/img/화면 캡처 2022-11-25 173722-1669365511308-47.png)

- 기존 create 됐지만 start 안된 컨테이너 삭제

  ```
  $ sudo docker container rm web_02_clone
  ```

- 새로운 포트로 컨테이너 시작

  ```
  $ sudo docker container run --name web_02_clone -d -p 8080:80 web_01:1.0
  ```

- 컨테이너 정보 확인

  ```
  $ sudo docker container ps -a
  ```

  ![화면 캡처 2022-11-25 174017](../../assets/img/화면 캡처 2022-11-25 174017.png)

  ![화면 캡처 2022-11-25 174046](../../assets/img/화면 캡처 2022-11-25 174046.png)
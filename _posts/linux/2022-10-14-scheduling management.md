---
title:  "scheduling management"

categories:
  - centos
tags:
  - [linux,scheduling,centos]

toc: true

date: 2022-10-14
last_modified_at: 2022-10-14
---

## scheduling management

- 스케쥴링 관리

  - 일정시간 간격으로 작업을 하도록 설정

- crontab 시간

  ![Untitled](../../assets/img/Untitled-1670600637421-24.png)

  ```
  # vi /etc/crontab
  ```

  ![화면 캡처 2022-12-10 004452](../../assets/img/화면 캡처 2022-12-10 004452.png)

- cronie 패키지 정보 

  - 프로세스 : crond

  - 목록 : crontab

  - 패키지 설치 여부

    ```
    [root@localhost ~]# rpm -qa | grep cron
    ```

    ![image-20221210004749836](../../assets/img/image-20221210004749836.png)

  - 프로세스 실행 여부

    ```
    [root@localhost ~]# ps -ef | grep cron
    ```

    ![화면 캡처 2022-12-10 004836](../../assets/img/화면 캡처 2022-12-10 004836.png)

#### 실습

- 실습환경 설정

  ```
  [root@localhost ~]# mkdir /data1
  [root@localhost ~]# touch /data1/1.txt
  [root@localhost ~]# rdate -s time.bora.net
  ```

- 스케쥴 확인

  - 스케쥴 목록

    ```
    # crontab -l
    ```

    ![image-20221210005127573](../../assets/img/image-20221210005127573.png)

  - 편집

    ```
    # crontab -e
    
    * * * * * touch /data1/1.txt  --> 1분마다 실행
    ```

    ![화면 캡처 2022-12-10 005235](../../assets/img/화면 캡처 2022-12-10 005235.png)

    ![화면 캡처 2022-12-10 005357](../../assets/img/화면 캡처 2022-12-10 005357.png)

    ```
    [root@localhost ~]# crontab -l
    ```

    ![image-20221210005452275](../../assets/img/image-20221210005452275.png)

  - 분 단위로 변경되는 것을 확인

    ```
    1분 마다 touch로 1.txt를 생성하기때문에 시간이 바뀐다
    
    [root@localhost ~]# ll /data1/1.txt 
    ```

    ![화면 캡처 2022-12-10 005715](../../assets/img/화면 캡처 2022-12-10 005715-1670601546664-31.png)

  - crond 작업 내역 확인

    ```
    [root@localhost ~]# tail /var/log/cron
    ```

    ![화면 캡처 2022-12-10 010027](../../assets/img/화면 캡처 2022-12-10 010027.png)

  - 작업취소 

    ```
    [root@localhost ~]# crontab -r
    [root@localhost ~]# crontab -l
    ```

    ![화면 캡처 2022-12-10 005123](../../assets/img/화면 캡처 2022-12-10 005123.png)
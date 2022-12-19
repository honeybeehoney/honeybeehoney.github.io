---
title:  "Disk management : Linux"

categories:
  - centos
tags:
  - [linux,disk]

toc: true

date: 2022-10-13
last_modified_at: 2022-10-13
---

## Disk management : Linux

#### 실습 - 기본디스크:파티션

- 환경설정

  - 다른 가상머신에 있는 디스크파일(vmdk)을 복사하여 옮긴다

    ![화면 캡처 2022-12-09 001622](../../assets/img/화면 캡처 2022-12-09 001622.png)

  - mini에 디스크 등록

    ```
    add > harddisk > SCSI > use an existing disk >
    existing  disk file : vmdk  추가 
    ```

    ![ㄹㅇㅁㄴ](../../assets/img/ㄹㅇㅁㄴ-1670513109833-23.png)

    ![화면 캡처 2022-12-09 002545](../../assets/img/화면 캡처 2022-12-09 002545.png)

    ![화면 캡처 2022-12-09 002600](../../assets/img/화면 캡처 2022-12-09 002600.png)

    ![화면 캡처 2022-12-09 002616](../../assets/img/화면 캡처 2022-12-09 002616.png)

    ![화면 캡처 2022-12-09 002630](../../assets/img/화면 캡처 2022-12-09 002630.png)

    ![화면 캡처 2022-12-09 002717](../../assets/img/화면 캡처 2022-12-09 002717.png)

    ![화면 캡처 2022-12-09 002801](../../assets/img/화면 캡처 2022-12-09 002801.png)

#### partitioning(파티셔닝)

- fdisk

  ![화면 캡처 2022-12-09 003333](../../assets/img/화면 캡처 2022-12-09 003333.png)

  물리적 하드디스크는 추가되는 순서로 /dev/sda , sdb ,sdc ...

- fdisk -l

  ![화면 캡처 2022-12-09 003603](../../assets/img/화면 캡처 2022-12-09 003603.png)

- fdisk를 이용한 파티션 관리

  - n - 파티션 추가 

    ```
    [root@localhost ~]# fdisk /dev/sdb
    ```

    ![화면 캡처 2022-12-09 003803](../../assets/img/화면 캡처 2022-12-09 003803.png)

    ![화면 캡처 2022-12-09 004810](../../assets/img/화면 캡처 2022-12-09 004810-1670514672411-38.png)

  - 파티션타입 선택

    ![화면 캡처 2022-12-09 005037](../../assets/img/화면 캡처 2022-12-09 005037-1670514765557-41.png)

  - 파티션 넘버 지정 및 sector 지정 

    ![화면 캡처 2022-12-09 005321](../../assets/img/화면 캡처 2022-12-09 005321.png)

  - p - 정보 확인

    ![화면 캡처 2022-12-09 005508](../../assets/img/화면 캡처 2022-12-09 005508.png)

  - d - 파티션 삭제

    ![화면 캡처 2022-12-09 005602](../../assets/img/화면 캡처 2022-12-09 005602.png)

  - w - 저장

    ![화면 캡처 2022-12-09 005700](../../assets/img/화면 캡처 2022-12-09 005700.png)

- 파일시스템

  - mkfs

    ```
    [root@localhost ~]# mkfs
    ```

    ![화면 캡처 2022-12-09 005903](../../assets/img/화면 캡처 2022-12-09 005903.png)

  - 종류

    ```
    windows(NT) : FAT,FAT32,NTFS
    linux : ext4, xfs, FAT, FAT32, NTFS
    ```

  - ext4

    ```
    - journaling file sytem : 파일시스템의 입출력을 모두 기록 > 복구 장점
    ```

  - 파일 시스템 부여

    ```
    [root@localhost ~]# mkfs -t ext4 /dev/sdb1
    ```

    ![화면 캡처 2022-12-09 010232](../../assets/img/화면 캡처 2022-12-09 010232.png)

- 마운트

  - 마운트 할 디렉터리 생성 및 파일 생성

    ```
    [root@localhost ~]# mkdir /m1
    [root@localhost ~]# echo hi > /m1/m.txt
    ```

    ![화면 캡처 2022-12-09 010750](../../assets/img/화면 캡처 2022-12-09 010750.png)

  - 마운트하고 마운트 상태 확인

    ```
    [root@localhost ~]# mount /dev/sdb1 /m1
    [root@localhost ~]# df -h
    ```

    ![화면 캡처 2022-12-09 011029](../../assets/img/화면 캡처 2022-12-09 011029-1670515860294-55.png)

  - 마운트 후 디렉터리 내용이 없다

    ```
    [root@localhost ~]# ls -al /m1
    ```

    ![화면 캡처 2022-12-09 011201](../../assets/img/화면 캡처 2022-12-09 011201.png)

  - 해제하면 디렉터리 내용이 원래대로 돌아온다

    ```
    [root@localhost ~]# umount /m1
    [root@localhost ~]# ls -al /m1
    ```

    ![화면 캡처 2022-12-09 011330](../../assets/img/화면 캡처 2022-12-09 011330.png)

  - 마운트 후 파일 생성

    ```
    [root@localhost ~]# mount /dev/sdb1 /m1
    [root@localhost ~]# touch /m1/test.txt
    [root@localhost ~]# ls /m1
    ```

    ![화면 캡처 2022-12-09 011602](../../assets/img/화면 캡처 2022-12-09 011602.png)

  - 해제 한뒤 다시 확인

    ```
    [root@localhost ~]# umount /m1
    [root@localhost ~]# ls /m1
    ```

    ![화면 캡처 2022-12-09 011651](../../assets/img/화면 캡처 2022-12-09 011651.png)

  - 다시 마운트하면 생성 했던 파일이 존재한다

- /etc/fstab

  - 재부팅을 할 경우 마운트 정보가 사라진다

    ```
    # init 6 또는 reboot
    [root@localhost ~]# df -h
    ```

    ![화면 캡처 2022-12-09 120314](../../assets/img/화면 캡처 2022-12-09 120314.png)

  - /etc/fstab 파일을 수정하여 재부팅시에도 정보 저장

    ```
    [root@localhost ~] # vi /etc/fstab
    ```

    ![화면 캡처 2022-12-09 132651](../../assets/img/화면 캡처 2022-12-09 132651-1670560199679-3.png)

  - 장치명대신에 UUID도 사용 가능하다

    ```
    UUID : 장치의 고유번호
    
    [root@localhost ~]# blkid
    ```

    ![화면 캡처 2022-12-09 133123](../../assets/img/화면 캡처 2022-12-09 133123.png)

  - 재시작 후 확인

    ```
    [root@localhost ~]# reboot
    [root@localhost ~]# df -h
    ```

    ![화면 캡처 2022-12-09 133252](../../assets/img/화면 캡처 2022-12-09 133252-1670560403590-7.png)

    

<br>

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}
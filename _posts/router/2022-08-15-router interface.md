---
title:  "Router Interface" 

categories:
  - router
tags:
  - [router,routing]

toc: true

date: 2022-08-14
last_modified_at: 2022-08-14
---

## 🗂️Packet Tracer를 이용한 실습

- <span style="color:blue"><b>구성도</b></span>

![Untitled (1)](../../assets/img/Untitled (1)-16605575660291.png)

- Packet Tracer에서 위 구성도 처럼 만들어보기

![화면 캡처 2022-08-15 191440](../../assets/img/화면 캡처 2022-08-15 191440.png)

![화면 캡처 2022-08-15 192128](../../assets/img/화면 캡처 2022-08-15 192128.png)

![화면 캡처 2022-08-15 192154](../../assets/img/화면 캡처 2022-08-15 192154.png)

![화면 캡처 2022-08-15 191600](../../assets/img/화면 캡처 2022-08-15 191600.png)

![화면 캡처 2022-08-15 194142](../../assets/img/화면 캡처 2022-08-15 194142.png)

## 🗂️pc 주소 설정

![화면 캡처 2022-08-15 194238](../../assets/img/화면 캡처 2022-08-15 194238.png)

> 주소 설정할 pc를 클릭후 Desktop에서 IP Configuration 클릭

![화면 캡처 2022-08-15 235604](../../assets/img/화면 캡처 2022-08-15 235604.png)

![화면 캡처 2022-08-16 000510](../../assets/img/화면 캡처 2022-08-16 000510.png)

> 나머지 컴퓨터에도 해당하는 주소를 모두 입력한다.

## 🗂️Interface 설정

- 설정할 interface에 접근하여 주소입력 및 통신연결하기

  ![fda](../../assets/img/fda-16606435242352.png)

```
Router>
Router>enable 
Router#configure terminal 
Router(config)#interface fastEthernet 0/0
Router(config-if)#ip address 10.10.10.254 255.255.255.0
Router(config-if)#no shutdown
```

![화면 캡처 2022-08-16 185306](../../assets/img/화면 캡처 2022-08-16 185306.png)

- <span style="color:blue"><b>연결 확인</b></span>

  - ping test

    ![화면 캡처 2022-08-16 185424](../../assets/img/화면 캡처 2022-08-16 185424.png)

    ![화면 캡처 2022-08-16 185459](../../assets/img/화면 캡처 2022-08-16 185459.png)

  - 명령어를 통한 입력값 점검

    ```
    Router#show running-config
    ```

  ![화면 캡처 2022-08-16 190106](../../assets/img/화면 캡처 2022-08-16 190106.png)

  ```
  Router#show ip interface brief
  ```

  ![화면 캡처 2022-08-16 214508](../../assets/img/화면 캡처 2022-08-16 214508.png)

- 오른쪽도 같은 방법으로 통신 연결후 ping test

![화면 캡처 2022-08-16 200852](../../assets/img/화면 캡처 2022-08-16 200852.png)

> 연결 확인후 pc끼리 ping test

![화면 캡처 2022-08-16 201151](../../assets/img/화면 캡처 2022-08-16 201151.png)

![화면 캡처 2022-08-16 201221](../../assets/img/화면 캡처 2022-08-16 201221.png)

> 나머지 pc들도 각자 확인해보자

## 🗂️Interface  수정, 설정 삭제

- <span style="color:blue"><b>수정</b></span>

  - 수정은 덮어씌우면 된다

  ```
  Router(config)#interface fastEthernet 0/0
  Router(config-if)#ip address 10.10.10.253 255.255.0.0
  Router#show running-conf
  ```

  ![화면 캡처 2022-08-16 202355](../../assets/img/화면 캡처 2022-08-16 202355.png)

> 변경된 것 확인

- <span style="color:blue"><b>삭제</b></span>

  ```
  Router(config)#interface fastEthernet 0/0
  Router(config-if)#no ip address
  Router#show ip interface brief
  ```

  

![화면 캡처 2022-08-16 214714](../../assets/img/화면 캡처 2022-08-16 214714.png)

> 삭제 확인



<br>

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}
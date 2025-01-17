---
title:  "Router 기본 설정하기" 

categories:
  - router
tags:
  - [router,routing,Layer3]

toc: true

date: 2022-07-31
last_modified_at: 2022-07-31
---

##  🗂️Cisco IOS

- Cisco IOS - Cisco사에서 개발한 Router, Switch의 운영체제 Software

- IOS CLI 
  - IOS에서 제공되는 기본 사용자 인터페이스
  - 명령어를 직접 입력하는 방식
  - 장비 종류 및 IOS 기능에 따라 제공되는 명령어가 달라 짐
  - 장비에서 제공받을 기능에 따라 다양한 Mode를 통해 명령어를 입력 함

- IOS CLI 기본 기능

  - 명령어 목록 제공 

    > 목록을 표시하고 싶은 위치에서 ? (물음표) 입력

    > 지정된 모드 또는 명령어 조합마다 사용할 수 있는 목록만 표시

  - 에러 메시지 제공

    > 장비에서 발생한 이벤트를 표시하여 문제를 해결할 수 있도록 도와 줌

  - History 

    > 이전에 사용한 명령을 기억하여 재사용할 수 있음

- IOS CLI Mode 

  - 특정 기능 또는 동작을 제어 할 수 있는 모드를 따로 제공 함 

  - 지정된 기능설정은 지정된 Mode에서만 할 수 있음 

  - 현재의 Mode를 Prompt로 확인 함

![화면 캡처 2022-07-31 234603](../../assets/img/화면 캡처 2022-07-31 234603.png)

- User Mode 

  - 장비의 초기 모드

  - 기본적인 정보 확인 가능

  - 관리를 위해서 권한을 가지고 있는 계정으로 로그인 해야 함

    > 초기 설정 전에는 그냥 로그인 함

![화면 캡처 2022-07-31 234813](../../assets/img/화면 캡처 2022-07-31 234813.png)

- Privileged Mode 

  - 장비의 관리 모드 

  - 시스템의 기본 설정 및 모든 정보의 관리를 위한 명령 수행 모드

  - 기능 설정은 불가능 함

  - 권한이 있어야 함

    ![화면 캡처 2022-07-31 234831](../../assets/img/화면 캡처 2022-07-31 234831.png)

- Global Configuration Mode 

  - 장비의 기능 설정 모드 

  - 장비 전체에 적용되는 설정

![화면 캡처 2022-07-31 234902](../../assets/img/화면 캡처 2022-07-31 234902-165927974038521.png)

- Regional Setting Mode 
  - 장비의 부분적인 기능 설정 모드 
  - interface, line, router, acl 등 특정 기능에 대한 명령이 적용되는 모드

![화면 캡처 2022-07-31 234920](../../assets/img/화면 캡처 2022-07-31 234920.png)

![화면 캡처 2022-07-31 235011](../../assets/img/화면 캡처 2022-07-31 235011.png)

## 🗂️패킷트레이서 설치하기

- 패킷 트레이서는 시스코에서 제공하는 라우터 시뮬레이터로 각종 router 설정을 연습해볼수 있다

- [Cisco Packet Tracer - Networking Simulation Tool (netacad.com)](https://www.netacad.com/courses/packet-tracer)

![화면 캡처 2022-08-14 162305](../../assets/img/화면 캡처 2022-08-14 162305.png)

- 위에 링크로 사이트에 접속한뒤 회원가입하여 로그인하고 나서 사이트 왼쪽 위편에 보면 Courses란 메뉴에 Packet Tracer를 클릭한다

![화면 캡처 2022-08-14 162417](../../assets/img/화면 캡처 2022-08-14 162417.png)

- View courses를 클릭한다

  ![화면 캡처 2022-08-14 162431](../../assets/img/화면 캡처 2022-08-14 162431.png)

- 위 그림과 같은 창이 나오면 Skills For All을 클릭한다

  ![화면 캡처 2022-08-14 162453](../../assets/img/화면 캡처 2022-08-14 162453.png)

- Getting Strarted with Cisco Packet Tracer 클릭

![화면 캡처 2022-08-14 162600](../../assets/img/화면 캡처 2022-08-14 162600.png)

- Download and Use Cisco Packet Tracer를 클릭한다

![화면 캡처 2022-08-14 162635](../../assets/img/화면 캡처 2022-08-14 162635.png)

- 스크롤을 내리다보면 1.0 Install Cisco Packet Tracer 가 나오는데 클릭하면된다.

![화면 캡처 2022-08-14 162657](../../assets/img/화면 캡처 2022-08-14 162657.png)

- 클릭하여 나온 화면에서 스크롤을 조금 내리면 위와 같은 다운로드링크가 나온다

  ![화면 캡처 2022-08-14 162718](../../assets/img/화면 캡처 2022-08-14 162718.png)

- 다운로드 링크를 눌렀으면 위와 같은 화면이 나오는데 자신의 컴퓨터 OS에 맞는 버전을 클릭하여 다운로드하고 설치하면 완료된다.

<br>

[맨 위로 이동하기](#){: .btn .btn--primary }{: .align-right}
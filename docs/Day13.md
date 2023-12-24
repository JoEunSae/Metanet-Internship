# Day13

## 프로세스 모니터링과 예약관리

### 프로세스 모니터링

#### top
- 리눅스에서 동작중인 프로세스의 상태를 주기적으로 출력하면서 현재 어떤 프로세스가 시스템 자원을 많이 소모하는지, 얼마나 오랫동안 수행되고 있는지를 확인할 수 있는 도구

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/6544b618-06d3-4236-8eee-b0605b20932e)

### 일회성 작업 예약
- 시스템 증설을 위한 서버 Shutdown, 시스템 상태를 점검하기 위한 스크림트 수행 등 일시적으로 수행되어야 하는 경우

#### at 도구를 이용한 일회성 작업 예약
- `at 예약시간`
  - `> 예약명령1`
  - `> 예약명령2`
  - `<Control>D
- 예약시간 표현방법
  - 18:00
  - 11:00am jul 21
  - 3:00pm tomorrow
- 예약 확인 및 취소
- `atq or at -l`:예약 작업 확인
- `atrm or at -r`:작업취소
  - `atrm 작업번호`
  - `at -r 작업번호`
 
### 주기적인 작업 예약
- 매일 새벽 3시에 진행하는 백업 작업이나 주1회 고객에게 메일을 발송하는 업무 등 규칙적으로 반복하는 업무에 활용

#### cron을 이용한 주기적으로 반복적인 작업 등록

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/6efea648-fa53-4f52-8753-79a55e8a4c69)

#### 주기적인 작업 등록 확인
- `crontab -l`

#### 주기적인 작업 등록 취소
- `crontab -r`

## 네트워크 구성과 네트워크 기본 도구

### 네트워크 구성정보

#### TCP/IP 프로토콜
- 정보 교환을 목적으로 컴퓨터들을 연결한 망을 네트워크라고 하며, 이 네트워크를 이용하여 통신을 하려면 프로토콜을 이용해야 함
- 전 세계를 하나의 네트워크로 연결한 인터넷에서 TCP/IP 프로토콜을 이용하고 있음
- TCP/IP 계층구조

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/bd0a15a5-f75f-4e7f-9483-a17d21b1c40a)

#### TCP/IP통신을 위한 네트워크 구성 정보
- IP주소
- 서브넷매스크 주소
- 브로드캐스트 주소
- 게이트웨이 주소
- DNS 서버 주소
- 호스트 명

### 네트워크 설정 도구 및 설정 파일

#### 네트워크 서정 도구 - nmtui

#### 네트워크 설정 파일

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/cd334b53-d583-492a-92bb-665d620b9dd2)

### 네트워크 연결 설정 확인 도구

#### IP 도구
- 네트워크 장치, IP주소 및 라우팅 정보 등을 확인하는 도구
- 사용법) ip 명령
  - addr : 네트워크 장치에 설정되어있는 ip 프로토콜 정보
    ![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/5e173a67-e2c2-476c-8962-c99821d16b3f)

  - route : 라우팅 테이블 항목
  - link : 네트워크 장치에 대한 정보

#### ifconfig 도구
- 네트워크 장치, IP 주소, 서브넷매스크 주소 및 브로드캐스트 주소등을 확인하는 도구
- `ipconfig [인터페이스명]`
  ![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/3d19c1e4-977a-4632-8d06-2833055c5c94)

#### route
- 라우팅 테이블의 정보를 확인하는 도구
- `route`
  ![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/4666575c-2164-4a16-b40e-719cdc55e2c9)




  







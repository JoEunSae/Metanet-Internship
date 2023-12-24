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
- `ip 명령`
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

## 네트워크 진단 도구

### 네트워크 진단 도구
- 네트워크를 통해 정상적인 통신이 가능한지 확인하는 방법

#### ping
- 상대 시스템으로 echo 패킷을 전송하고 이엥 대한 응답 패킷 수신 여부에 따라 통신 가능 여부를 확인
- 통신 양이 많은 서버의 경우 통신이 가능하더라도 응답하지 않도록 설정될 수 있음
- `ping [옵션] 목적지_IP주소`
  - -c # : 목적지로 전송할 echo 패킷 개수(#)
  - -i # : 각 패킷 전송 사이의 전송 시간 간격(초)

#### host
- 인터넷 이용시 사용하는 도메인 명 검색에 사용하는 도구, 주로 DNS 서버의 설정을 확인할 때 사용
- `host 목적지_도메인명`

#### mtr
- ping + 경로 추적 도구
- `mtr 목적지_호스트명 또는 IP주소`

#### netstat
- 각 프로토콜 별 활성화된 서비스 및 서비스 관련 프로세스 목록 확인
- `netstat [옵션]
  ![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/37cc98ee-2aba-4b3e-a88e-0a91af9c2231)


#### TCP 프로토콜의 상태 천이도

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/88ff98c6-9713-4b8a-bda1-9fe7cb068d77)

### 패킷 수집 및 분석도구

#### tcpdump
- 텍스트 기반의 패킷 수집 및 분석 도구
- 리눅스 배포판에 기본적으로 설치됨
- `tcpdump [옵션] [표현식 패턴]`
  - `-i 인터페이스명` : 인터페이스로부터 네트워크 패킷 수집 및 분석
  - `-r 파일명` : 파일로부터 패킷 정보를 읽어들여 분석
  - `-w 파일명` : 인터페이스로부터 수집된 패킷 정보를 파일로 저장
  - `-ttt` : timestamp 기능
  - `-vv` : 분석 정보 상세 보기 설정

## 기타도구

#### 시스템 사양 정보 확인

#### uname
- 리눅스가 설치되어 있는 시스템의 사양에 대한 정보를 간단히 확인할 수 있는 도구
- `uname [옵션]`
  - -a : 시스템 사양에 관한 모든 정보 출력
  - -s : OS의 종류 출력
  - -n : nodename, 즉 호스트명 출력
  - -r : 커널의 릴리즈 번호
  - -m : 머신 종류, 즉 하드웨어 플랫폼 종류 출력
 
### 로그인 되어 있는 사용자 확인

#### who
- 현재 리눅스 서버에 콘솔 또는 원격으로 접속되어 있는 사용자 목록 확인
  ![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/26cbdcee-8c98-435f-a552-d79e4f4feb0b)

#### w
- 현재 리눅스에 로그인 되어 있는 사용자가 어떤 작업을 수행하고 있는지 확인
  ![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/5a95a179-c28d-475f-9fba-0c7ba05eab14)

### 하드웨어 사양 진단 도구

#### lscpu
- cpu 사양에 대한 정보가 상세히 출력

#### lsblk
- 현재 장착되어있는 블록형 장치의 목록 출력

#### lsusb
- 현재 리눅스에 연결되어 있는 USB 장치에 대한 목록 출력

#### lshw
- 현재 리눅스가 설치되어 있는 시스템 하드웨어 사양 목록을 상세하게 출력

## 소프트웨어 패키지 관리

### Ununtu Linux의 SW 패키지 관리자

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/a971d52d-bc2c-457d-98a6-1f7e4716a3d4)

### rpm 관리자를 이용한 오픈소스 패키지 관리

#### rpm 패키지 관리자
- 레드햇사에서 만든 소프트웨어 관리도구
- 윈도우의 setup 또는 installer와 유사
- 소프트웨어를 쉽게 설치 또는 삭제할 수 있음

#### 패키지 설치 및 업그레이드
- `rpm -i[옵션] rpm_패키지파일`
- `rpm -U[옵션] rpm_패키지파일`
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/0a585d8f-3bd7-4406-967d-cc9d49fdd88c)

#### 패키지 삭제
- `rpm -e [옵션] 패키지명`

### dnf 관리자를 이용한 오픈소스 패키지 관리

#### dnf 패키지 관리자
- rpm 기반의 패키지 도구
- 패키지를 분석하여 의존성을 해결
- 패키지 저장소로부터 원격 자동 업데이트 및 설치 가능

#### 저장소 설정
- /etc/yum.repos.d/패키지저장소파일

#### 패키지 목록 확인
- `dnf list [명령] [패키지명]
  - all : 설치되어있거나 설치 가능한 패키지 목록 출력
  - available : 설치 가능한 패키지 목록 출력
  - updates : 업데이트 가능한 패키지 목록 출력
  - installed : 설치되어 있는 패키지 목록 출력
  - 패키지명 : 패키지 설치 여부 상태 확인

#### 패키지 설치 및 업그레이드
- `dnf [-y] install 패키지명`
- `dnf update [패키지명]`
- `dnf upgrade [패키지명]`

#### 패키지 삭제
- `dnf [-y] erase 패키지명`
- `dnf [-y] remove 패키지명`

#### 패키지 정보
- `dnf info 패키지명`

#### 패키지 검색
- `dnf search all "검색키워드"`


# Day20

### 아래 교제로 리눅스 정리
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/2801e6ed-43a7-4653-bff4-b26f2ccd0c7b)

## 2장 리눅스 커널

### 리눅스 아키텍처
- 하드웨어 계층
- 커널 계층
- 사용자 영역계층

### 커널 구성요소
- 프로세스관리
- 메모리 관리
- 네트워킹
- 파일스시템
- 캐릭터 디바이스와 디바이스 드라이버 관리

#### 프로세스 관리
- 세션
- 프로세스 그룹
- 프로세스
- 스레드
- 태스크

## 4장 접근제어

### 접근제어
- 임의접근제어
- 강제접근제어

### 사용자
- 시스템 사용자 또는 시스템 계정
- 일반 사용자

#### 로컬에서 사용자 관리하기
- 사용자 데이터베이스 : /etc/passwd
- 그룹 데이터베이스 : /etc/group
- 사용자 비밀번호 : /etc/shadow
- 그룹 비밀번호 : /etc/gshadow

### 권한

#### 파일권한
- 사용자 : 파일의 소유자
- 그룹 : 그룹은 하나 이상의 구성원이 있다.
- 나머지 : 그 밖의 모두가 이 카테고리에 들어간다.
- 읽기(r)
- 쓰기(w)
- 실행(x)
- chmod : 권한 변경
- chown : 소유자 변경

#### 프로세스 권한
- RUID : 프로세스를 시작한 사용자의 UID
- EUID : SetUID 권한이 설정된 실행 파일에 의해 변경되며, 일시적으로 다른 계정의 UID를 저장해서 사용할 수 있도록 해준다.
- 저장된 SUID : 프로세스가 실제 UID과 저장된 SUID 사이에서 유효 UID를 전환함으로써 권한을 가정할 수 있을 때 사용
- FUID : 리눅스 전용 ID로서 파일 접근 권한을 결정하는 데 사용

## 5장 파일시스템
- 드라이브
- 파티션
- 볼륨
- 슈퍼블록
- 아이노드

#### 링크
- 하드링크 : inode공유
- 심볼릭링크 : 원본파일명공유

### 논리 볼륨 관리자
- 물리 볼륨(PV)
- 논리 볼륨(LV)
- 볼륨 그룹(VG)

### 파일시스템 작업
- `mkfs -t ext4 \ [위치]` : 파일시스템 생성

## 6장 애플리케이션, 패키지 관리, 컨테이너
- 프로그램
- 프로세스
- 데몬
- 애플리케이션
- 패키지
- 패키지 관리자
- 공급망
- 부팅

### systemd
- 일부 리눅스 배포판에서 유닉스 시스템 V나 BSD init 시스템 대신 사용자 공간을 부트스트래핑하고 최종적으로 모든 프로세스들을 관리하는 init 시스템

 #### 유닛
 - service유닛
 - target 유닛 
 - mount 유닛
 - timer 유닛 
 - socket
 - deevice
 - automount
 - swap
 - path
 - sanpshot
 - slice
 - scope

#### systemctl로 관리하기
- `systemctl enable`
- `systemctl daemon-reload`
- `systemctl start`
- `systemctl stop`
- `systemctl restart`
- `systemctl reload`
- `systemctl kill`
- `systemctl status`

#### 컨테이너
- 운영체제 수준의 가상화 기술로 리눅스 커널을 공유하면서 프로세스를 격리된 환경에서 실행하는 기술

#### 리눅스 네임스페이스
- 프로세스를 실행할 때 시스템의 리소스를 분리해서 실행할 수 있도록 도와주는 기능
- clond : 실행 컨텍스트의 일부를 부모 프로세스와 공유할 수 있는 자식 프로세스를 만드는 데 사용된다.
- unshare : 기존 프로세스에서 공유된 실행 컨텍스트를 제거하는 데 사용된다.
- setnx : 기존 프로세스를 기존 네임스페이스에 결합하는 데 사용된다.

## 7장 네트워크

### TCP/IP 스택
- 대부분 IETF 사양에 의해 정의된 여러 프로토콜과 도구로 이루어진 계층 네트워크 모델이다.
- 링크계층
- 인터넷 계층
- 전송 계층
- 애플리케이션 계층

#### 링크계층
- 이더넷
- 무선
- MAC주소
- 인터페이스

#### 인터넷 계층
- IPv4
  - 송신지 주소
  - 수신지 주소
  - 프로토콜
  - TTL
  - 서비스 유형
- IPv6
- 인터넷 제어 메시지 프로토콜
- 라우팅
  - Destination
  - Gateway
  - Genmask
 
### DNS
- 도메인 네임 스페이스
- 리소스 레코드
- 네임 서버
- 리졸

## 8장 관측가능성

### 리눅스 성능측정

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/b8ef542d-13dd-4e2a-be31-3e5e2dedd9d8)

### 관측가능성 전략
- 관측가능성
- 시그널 유형 .
- 소스
- 목적지
- 텔레메트리

### 시그널 유형
- 로그
- 지표
  - 카운터
  - 게이지
  - 히스토그램
- 추적
  
### 로깅
- 개별 이벤트
- 텍스트 페이로드
- 로그 항목, 메시지, 행의 모음
- 메타데이터, 컨텍스트
- 개별 로그 메시지를 해석하는 방법을 보여주는 형식

## Git

깃 교과서<br>
https://git.jiny.dev/

### git저장소 구성하기

1. `git init goodbird`로 git 저장소 생성

2. `git config -- global init.defaultBrach main`로 디폴트 브랜치를 main으로 설정

3. `git config --global user.email gjsl1945@naver.com` 커밋 정보를 전달받을 이메일 지정

4. 해당 저장소 위치로 이동하여 파일 생성해보기

5. `git status`로 확인해보면 수정된 파일이 stage에 올라가지 않은것을 확인할 수 있다.

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/545e46c6-73fe-4568-a1fc-c06c0e0e93e5)

7. `git add hello.txt` 명령어로 stage에 추가

8. `git commit -m "first commit"`명령어로 커밋해준다

9. `git log`명령으로 commit로그 확인가능

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/de0c96a9-08f2-4986-b010-9264febeffbf)


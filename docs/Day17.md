# Day17

## 새로운 서버 설치

vagrant - Virtualbox등 가상화 소프트웨어를 "CUI(캐릭터 유저 인터페이스)"로 조작하기 위한 소프트웨어이다.

- vagrant설치
- virtualbox설치

- cmd에서 `vagrant init ubuntu/focal64`로 vagrantfile 생성
- `vagrant up`으로 vagrant 환경 프로비저닝하고 시작한다.
- `vagrant --help`로 가능한 명령 확인
- `vagrant halt`로 종료하기
- `vagrant destroy`로 삭제


인증
- password
- 키기반인증

virtualbox

ssh-keygen - 키만들기

 sed  -i 's/PasswordAuthentication no/PasswordAuthentication yes/g` /etc/ssh/sshd_config
 systemctl  restart sshd


 ## DNS
 - 사용자가 IP 주소 대신 인터넷 도메인 이름과 검색 가능한 URL을 사용하여 웹사이트에 접속하는 것을 가능하게 해준다.

### DNS 서버 구축

/etc/hosts 파일에 ip를 등록하여 

sudo dnf install -y bind bind-utils

- www : host명
- naver : sub-domain명
- com : tab-level domain명

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/af961848-416b-4684-a19f-29079e2aa143)

/etc/named_conf수정

/etc/named.rfc1912.zones

`dig @192.168.91.128 www.google.com`

**도메인명의 마지막은 '.'**

/etc/resolv.conf - NameServer IP 등록


#### 포워드 존 파일의 문법

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/810ab4f6-38b1-4f0c-a9a7-7f023bf27359)

- ! : 주석
- $TTL : Time to Live의 약자로 www.eaxmple.com의 호스트 이름을 물었을 때 문의한 다른 네임 서버가 해당 IP 주소를 캐시에 저장하는 시간을 의미
- @ : /etc/named.conf에 정의된 example.com을 의미한다.
- SOA : 괄호 안의 숫자는 시간을 의미
- NS : 설정된 도메인의 네임 서버 역학을 하는 컴퓨터를 지정하는 부분이다.
- A : 호스트 이름에 상응하는 IP 주소를 지정하는 부분
- CNAME : 호스트 이름에 별칭을 부여할 때 사용한다.




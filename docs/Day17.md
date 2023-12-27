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
 - IP 주소 및 기타 데이터를 저장하고 이름별로 쿼리할 수 있게 해주는 계층형 분산 데이터베이스

### DNS 서버 구축

/etc/hosts 파일에 ip를 등록하여 

sudo dnf install -y bind bind-utils

- www : host명
- naver : sub-domain명
- com : tab-level domain명

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/af961848-416b-4684-a19f-29079e2aa143)


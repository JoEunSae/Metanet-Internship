# Day17(12월 27일)

## 새로운 OS 설치

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

 `sed  -i 's/PasswordAuthentication no/PasswordAuthentication yes/g` /etc/ssh/sshd_config`
 `systemctl  restart sshd`


 ## DNS
 - 사용자가 IP 주소 대신 인터넷 도메인 이름과 검색 가능한 URL을 사용하여 웹사이트에 접속하는 것을 가능하게 해준다.

### 로컬 네임 서버 장동 순서
1. PC의 웹부라우저에서 domain으로 접근
2. /etc/resolv.conf 파일을 열어서 'nameserver 네임서버IP' 부분을 찾아 로컬 네임 서버 컴퓨터를 알아낸다.
3. 로컬 네임 서버에 요청 도메인의 IP 주소를 묻는다.
4. 로컬 네임 서버는 자신의 캐시 DB를 검색해 도메인의 정보가 들어 있는지를 확인 한다.
5. 로컬 네임 서버가 'ROOT 네임 서버'에 도메인의 주소를 묻는다.
6. 'ROOT 네임 서버'도 도메인의 주소를 모르므로 'com 네임 서버'의 주소를 알려주며 'com 네임 서버'에 물어보라고 한다.
7. 로컬 네임 서버가 'com 네임 서버'에 도메인의 주소를 묻는다.
8. com 네임 서버도 도메인의 주소를 모르므로 `~.com`을 관리하는 네임 서버의 주소를 알려주며 `~.com`네임 서버에 물어보라고 한다.
9. 로컬 네임 서버가 '~.com 네임서버`에 도메인의 주소를 묻는다.
10. 로켈네임서버는 클라이언트에게 요구한 IP주소를 알려준다
11. 클라이언트는 획득한 주소로 접속을 시도한다.

#### 캐싱 전용 네임 서버
- PC에서 URL로 IP 주소를 얻고자 할 때 해당하는 URL의 IP 주소를 알려 주는 네임 서버.
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/af961848-416b-4684-a19f-29079e2aa143)


### DNS 서버 구축

1. `dnf install -y bind bind-utils` 명령으로 네임 서버와 관련된 패키지 설치 
2. `vi /etc/named.conf` 로 설정파일 수정<br>
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/a40a2d1c-66d5-4cda-8cc5-99232eba2099)<br>
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/0f71b2ee-5412-42b2-98bc-e94155064efa)

3. `systemctl restart named` -> 서비스 재시작
   - `systemctl enable named` -> 네임 서버 상시 가동
   - `systemctl status naemd` -> 네임 서버 상태 확인
4. 방화벽 설정을 위해 명령어 수행
- `firewall-cmd --permanent --zone=public --add-port=53/tcp`
- `firewall-cmd --permanent --zone=public --add-port=53/udp`
- `firewall-cmd --reload `
5. `dig@네임서버IP 조회할RUL` : 네임서버가 잘 동작하는지 확인
6. `cat /etc/resolv.conf` : 네임 서버 변경
- `nameserver [네임서버ip]`로 변경

7. firefox로 해당 사이트 접속

#### 포워드 존 파일의 문법

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/810ab4f6-38b1-4f0c-a9a7-7f023bf27359)

- ! : 주석
- $TTL : Time to Live의 약자로 www.eaxmple.com의 호스트 이름을 물었을 때 문의한 다른 네임 서버가 해당 IP 주소를 캐시에 저장하는 시간을 의미
- @ : /etc/named.conf에 정의된 example.com을 의미한다.
- SOA : 괄호 안의 숫자는 시간을 의미
- NS : 설정된 도메인의 네임 서버 역학을 하는 컴퓨터를 지정하는 부분이다.
- A : 호스트 이름에 상응하는 IP 주소를 지정하는 부분
- CNAME : 호스트 이름에 별칭을 부여할 때 사용한다.




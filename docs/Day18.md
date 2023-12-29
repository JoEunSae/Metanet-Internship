# Day18(12월 28일)

**APM(Apache + PHP + MySQL)**

## Apache웹서버와 MariaDB연동하기

### Maria DB 설치
1. MariaDB설치
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/a74cf080-d6e9-4255-8f23-48432c9edd6f)
- 실치 후 ubuntu로 mariadb접속.

3. `$ mysql_secure_installation`로 초기설정

4. root계정으로 DB접속

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/03750219-5d57-4934-abc4-db948c1b1db0)

4. 사용자 계정 생성하기
- `[mysql]> create user 'goodbrid'@'%' identified by '1';`

5. 사용자에게 권한 부여하기
- `grant all on db.* to 'dbuser'@'%';`

6. 원격으로 db에 접속하기
- `mysql - u goodbird -h 192.168.56.10 -p`

7. DB에 접속해서 테이블 생성하기
- `create table product (ID varchar(10), NAME varcahr(10), price(10));`
- `insert into product value("10000","book",15000");`

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/d8f90938-2ef9-478a-933b-e46c2608f2ae)


### Apache web서버 설치

1. `sudo dnf install -y httpd httpd-manual`로 apache설치
   
3.클라이언트 서벗에서 방화벽 수정
   ```bash
   sudo firewall-cmd --list-all
   sudo firewall-cmd --add-service=http --permanent
   sudo firewall-cmd --reload
   ```
   
5. 클라이언트 서버에서 httpd.conf파일에서 도메인별로 경로를 매핑하여 가상 호스트 생성
   ```bash
   cd /etc/httpd/conf
   vi httpd.conf
   ```
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/c58e4da9-e677-42ec-bf5b-010106c667c7)

6. 클라이언트 서버에서 `cd /var/www` 아래에 html과 vi 폴더에 각각 index.html파일 생성

7. 클라이언트 서버에서 `vi /etc/hosts`에 요청할 도메인 입력

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/76216b28-7c27-4374-a377-fb949d53a709)


8. DNS 서버에서 `/etc/resolv.conf` namerserver ip를 자신의 nameserver ip로 변경

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/cc4bb38b-7809-456b-a987-5ed456202719)

9. DNS 서버에서 `/var/named/named.example.com` 파일에서 zoon 설정
    
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/e4b62648-dbcb-4b42-92d4-5593e18e5a17)

10. 해당 도메인으로 접근

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/96aae25d-9849-498d-a7dc-4616d1ef8730)

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/2dede75b-bf9d-4a72-8833-4c1053e5e6d3)


### 웹 서버의 응용 서비스 : 클라우드 저장소 구축

1. php 7.4 설치하기
   ```bash
   dnf -y install dnf-utils http://rpms.remirepo.net/enterprise/remi-release-9.rpm
   dnf -y moudule reset php
   dnf moudule enable php:remi-7.4
   ```
2. APM과 ownCloud를 위한 관련 패키지를 설치한다.

3. `systemctl restart mariadb`와 `systemctl enable mariadb`명령을 입력해 데이터베이스 서비스 시작

4. 스키마 생성하고 사용자도 생성
   `GRANT ALL ON webDB.* To webUser@localhost IDENTIFIED BY '1234';`

5. httpd 서비스를 다시 시작하고 웹포트도 허용해준다
   ```bash
   systemctl restart httpd
   systemctl enable httpd
   firewall-cmd --permanent --add-service=http
   firewall-cmd --permanent --add-service=https
   firewall-cmd --reload
   ```

6. ownCloud를 다운로드하고 압춥을 풀어주고 접근 권한을 변경한다.
   ```bash
   mkdir owncloud/data
   chown -R apache.apache owncloud
   chmod -R 755 ownCloud
   ```

7. 웹 브라우저에서 `http://서버ip주소/owncloud/`로 접속
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/7d3b1826-6eb6-4221-85f5-fed4958c366c)

8. 사진과 같이 클라우드 저장소를 사용할 수 있다
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/f73989fb-a4e3-481e-9209-4feab660a330)





   
   
   

   
 






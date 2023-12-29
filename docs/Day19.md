# Day19 (12월 28일)

## SELinux(Security-Enhanced Linux)
- 어떤 프로세스가 어떤 파일이나 디렉토리 및 포트를 액세스할 수 있는지를 결정하는 일련의 보안 규칙

#### 주요특징
1. Mandatory Access Control (MAC) :  SELinux는 DAC에 추가하여 MAC을 제공합니다. DAC에서는 파일 소유자가 파일에 대한 액세스 권한을 결정하지만, MAC에서는 정책이 사용자에게 어떤 액세스를 허용할지를 결정합니다.
2. 정책 (Policy): SELinux는 시스템의 동작을 제어하기 위한 정책을 정의합니다. 이 정책은 어떤 프로세스가 어떤 리소스에 접근할 수 있는지에 대한 규칙을 정의합니다.
3. 라벨링 (Labeling): SELinux는 파일, 프로세스, 소켓 등의 객체에 라벨을 부여합니다. 이 라벨은 정책에 따라 액세스를 허용하거나 거부하는 데 사용됩니다.
4. 컨텍스트 (Context): SELinux에서는 객체의 라벨을 컨텍스트라고도 부릅니다. 예를 들어, 파일 시스템에서는 파일이나 디렉터리에 대한 SELinux 컨텍스트가 정의됩니다.
5. Enforcing 및 Permissive 모드: SELinux는 두 가지 주요 모드로 작동할 수 있습니다. Enforcing 모드에서는 정책을 엄격하게 시행하며, Permissive 모드에서는 정책을 어긴 작업을 로그에 남기지만 시스템 작동을 중단하지 않습니다.
6. SELinux 유틸리티: SELinux 정책을 설정하고 관리하기 위한 여러 유틸리티가 있습니다. 예를 들면 semanage, setsebool, getsebool, sestatus 등이 있습니다.


#### SELinux Context
- 모든 파일, 프로세스 및 포트에 적용되어 있는 보안레이블로 SELinux Policy에 의해 액세스 여부 결정

#### SELinux 보안 레이블
- user: role:type:sensitivity의 콘텍스트로 구성
- targeted 정책에서는 type 콘텍스트에 대한 룰 기준

#### context 확인하기
- `ps axZ`
- `ls -Z`

#### SElinux 모드
- enforcing
  - 강제 모드에서는 컨텍스트를 사용하여 파일을 읽으려고 하는 웹 서버의 액세스를 거부한다.
  - 강제 모드에서 SELinux 는 로그와 보호를 모두 수행한다.
- permissive
  -  허용 모드는 문제 해결에 주로 사용된다.
  -  명시적 규칙이 없는 경우에도 SELinux 에서 모든 상호 작용을 허용한다.
  -  강제 모드에서 거부할 상호 작용을 로깅한다.  제한하고 있는 콘텐츠에 대한 액세스를 일시적으로 허용한다.
  -  강제에서 허용으로 변경할시 재부팅 하지 않아도 된다.
- disabled
  -  비활성화 모드
  -  강제 모드/허용 모드로 변경시에는 재부팅이 필요하다.
 
**getenforce 명령으로 모드 확인**

#### SELinux 모드변경
- `setenforce [0|1]`
- 
#### SELinux Default 모드 설정
- /etc/selinux/config 파일 수정하면 booting시 

### SELinux 콘텍스트 변경
- SELinux context 일시적인 변경
  - `chcon -t <type> 파일명`
- SELinux 디폴트 context로 변경
  - `restorescon -v 파일명`
- SELinux 디폴트 context 정의
  - `semanage fcontext -a -t <type> 파일명`

### SELinux Troubleshooting

#### SELinux에서 파일에 대한 접근을 금지하는 경우

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/789a220c-9273-4cc1-8dea-7eedcd6ea1f8)

##### SELinux 메시지 로깅
- `setroubleshoot-server 패키지 설치`
- /var/log/audit/audit.log- 감사 메시지
- /var/log/messages - 간단한 요약 로그

#### sealert -l UUID
- 특정 사안에 대한 문제점 보고서
- /var/log/message로 부터 확인


#### sealert -a /var/log/audit/audit.log
- 모든 감사 관련 문제 보고서

## FTP 서버
- Mac, Windows, Linux 컴퓨터 등의 장치에서 다른 장치로 전송하는 소프트웨어 애플리케이션

### vsftp
- 리눅스와 유닉스 환경에서 보안성과 성능이 우수한 FTP서버

1. ubuntu에 `dnf -y install vsftpd`로 vsftpd 패키지 설치

2.  

3. 


filezilla설치후 ftp서버 연동
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/2e6748d3-5fb3-4a8c-bde6-86e83fd329ab)

## NFS 서버
- 리눅스 또는 유닉스 컴퓨터 사이에 저장 공간을 공유할 수 있도록 도와준다.

1. ubuntu에서 `apt install -y nfs-kernel-server'설치

2. 서버에서 `vi /etc/exports`에서 `/share 192.168.56.0/24(rw)추가`

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/6a4b3e76-1c89-4048-8d33-0ebf7270ee8d)

4. 클라이언트에서 아래 명령어로 수동 마운트
```bash
showmount -e 192.168.56.10
mkdir /nfs
mount 192.168.56.10:/share /nfs
cd /nfs
```

4. 서버에서 share폴더에 server.txt파일 생성하고

5. 클라이언트에서 cd폴더로 이동하여 ls명령으로 server.txt파일 확인 가능

6. 서버에서 `chmod 777 /share/`에서 권한을 변경해주면 클라이언트에서도 파일 생성 가능, 소유자와 그룹은 nobody로 생성

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/a419e4aa-b1a5-4785-a447-b8c83ed1b37e)

7. 클라이언트에서 /etc/fstab파일에 `192.168.56.10:/share /nfs nfs defaults 0 0`을 추가해 자동 마운트를 설정해준다.

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/185c8587-ccdb-4c63-8668-62f1e1c820e4)





# Day14

## 시스템 서비스 관리

### 자동으로 기동되는 시스템 프로세스

#### systemd
- 새로운 init+xinetd 시스템
- 빠른 부팅을 위해 병행 처리 가능
- 별도의 서비스 요청 없이도 필요 시 데몬 프로세스 구동
- 연관된 서비스 관리
- cgroup 이용을 통한 프로세스 추적

### systemctl 과 system units

#### systemctl
- systemd의 object (unit) 관리 명령
- unit 종류

![사진](../images/unit종류.png)

**Deamon프로세스**
- terminal과 무관하게 돌아감
- 무한루프
- systemctl로 관리

### 서비스 상태

`systemctl status name.type`

- status종류

![사진](../images/서비스상태.png)

### 서비스 제어

``` bash
systemctl status name.service           상태보기
          stop                          멈추기
          start                         시작
          restart                       서비스 종료 후 재시작
          reload                        설정파일 업데이트
          mask/unmask
          enable/disable
```

### 부팅 과정 제어

![사진](../images/부팅과정제어.png)

#### 부팅과정의 제어
- `systemctl reboot|poweroff`

#### systemd target 제어
- `systemctl isolate <target>`
- `systemctl get-default`
- `systemctl set-default <target>`
- 부팅시 kernel 라인에서 `system.unit=<target>`편집 후 부팅

## 시스템 로그

### 시스템 로그 구조

#### rsystlogd
- type과 priority의 기준에 의해 로그 파일에 기록
- 로그 디렉토리 : /var/log

### 시스템 로그 파일
- /var/log/messages : 대부분의 로그 메시지 기록, 제외 : 메일, 인증 주기적인 작업등
- /var/log/secure : 보안 및 인증 관련 메시지 및 오류 기록
- /var/log/maillog : 메일 서버 관련 메시지 로그
- /var/log/cron : 주기적으로 실행되는 작업에 대한 로그
- /var/log/boot.log : 시스템 기동에 관련된 메시지 기록

### 로그파일

- 로그 로테이션
  - /var/log/messages-20150430
    - 매일 cron 작업으로 logrotate 명령을 수행
- tail -f 로그파일명
- logger -p facility.priority "로그 메시지"

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/10030d9b-51f6-4468-bb3c-e17bf22418a7)

### systemd-journald

#### systemd-journald
- 커널, 부팅 과정의 초기 단계, 대몬 프로세스의 기동이나 실행 중 발생되는 표준 rsyslogd가 수진하는 모든 로그
- 기본적으로 메모리상에 기록되므로 재 기동하면 초기화(/run/)

#### 저널을 디스크로 저장
- 기본 경로 : /var/log//journal
- 기본적으로 파일시스템의 10% 이상을 초과하거나
- 파일시스템의 free 공간이 15% 미만이 되면 기록 중단

#### journalctl
- 가장 오래된 로그부터 시작하여 모든 시스템 저널을 보여주는 명령

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/778a1ed6-0098-46ee-9603-5811495680cd)


```bash
[student@localhost shell]$ dir_path=/home/student/testdir
[student@localhost shell]$ echo ${dir_path#/*}
home/student/testdir
[student@localhost shell]$ echo ${dir_path##/*}

[student@localhost shell]$ echo ${dir_path##*/}
testdir
[student@localhost shell]$ echo ${dir_path#*/}
home/student/testdir
[student@localhost shell]$ ^C
[student@localhost shell]$ echo ${dir_path%/*}
/home/student
[student@localhost shell]$ echo ${dir_path%%/*}

[student@localhost shell]$ dir_path=
[student@localhost shell]$ echo ${dir_path:-hello}
hello
```

### 셸 스크립트 작성과 실해

#### 셸 스크립트 작성

name.sh
```bash        
#!/bin/sh
echo "사용자 이름:" $USER
echo "홈 디렉터리:" $HOME
exit 0
```

#### 셸 스크립트 실행

- `sh name.sh`
- `./name.sh`

#### 파라미터 변수

paravar.sh
```bash
#!/bin/sh
echo "실행파일 이름은 <$0>이다"
echo "첫번째 파라미터는 <$1>이고, 두번째 파라미터는 <$2>다"
echo "전체 파라미터는 <$*>다"
exit 0
```

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/24e4b65c-fc55-4f47-91a4-5b1c91d66602)


### if문과 case문

#### 기본 if문

```bash
if [ 조건 ]
then
   참일 경우 실행
fi
```

#### if~else문
```bash
if [ 조건 ]
then
   참일 경우 실행
else
   거짓인 경우 실행
fi
```

#### 조건에 들어가는 비교 연산자

**문자열 비교**
- "문자열1" = "문자열2" 두 문자열이 같으면 참
- "문자열1" != "문자열2" 두 문자열이 같이 않으면 참
- -n "문자열" 문자열 NULL이 아니면 참
- -z "문자열" 문자열이 NULL이면 참

**산술 비교 연산자**
- 수식1 -eq 수식2 :두 수식이 같으면 참
- 수식1 -ne 수식2 : 두 수식이 같지 않으면 참
- 수식1 -gt 수식2 : 수식1이 크다면 참
- 수식1 -ge 수식2 : 수식1이 크거나 같으면 참
- 수식1 -lt 수식2 : 수식1이 작으면 참
- 수식1 -le 수식2 : 수식1이 작거나 같으면 참
- !수식 : 수식이 거짓이라면 참


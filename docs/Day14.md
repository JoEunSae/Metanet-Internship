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



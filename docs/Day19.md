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

#### SELinux Default 모드 설정
- /etc/selinux/config 파일 수정하면 booting시 적용


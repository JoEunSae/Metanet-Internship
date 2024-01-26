# Day36

## Azure 시작하기

### Azure가입하고 구독 할당
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/9071ea9b-e5c4-4d13-8243-5a49f6e76ffc)

### Azure 지리,지역,영역
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/5d9a3d97-ed43-4cb2-9c63-69c25bf84940)

### Azure 구독,리소스 그룹, 리소스
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/f76f5631-a5bc-4cd1-bf56-b68783b6f1fd)


#### 리소스 그룹

- 리소스 그룹 생성
- 리소스 생성

#### Cloud Shell
- Azure 리소스를 관리하기 위한 대화형 인증 브라우저 액세스 터미널
-  Bash나 PowerShell 작업 방식에 가장 적합한 셸 환경을 유연하게 선택

#### 태그
- 리소스를 보다 정교하게 필터링하고 리소스 사용량 보고서를 생성한다.

#### 리소스 이동하기
- 리소스는 필요에 따라 다른 리소스 그룹, 다른 구독, 다른 지역으로 이동할 수 있다.
- 특정 구독에서 더 이상 비용을 지불할 수 없는 경우 리소스를 비용을 지불할 수 있는 다른 구독으로 이동
- 구독 간 이동은 양쪽 구독이 동일한 Microsoft Entra ID 테넌트에 연결된 경우만 가능

#### 리소스와 리소스 그룹 보호하기
- 읽기전용 잠금 : 수정과 삭제 모두 불가능
- 삭제 금지 : 삭제만 불가능

## Azure 사용자와 그룹, 액세스 관리

### Microsoft Entra ID와 구독
- 팀의 구성원이 로그인하고 권한에 따라 리소스를 액세스할 수 있게 해주는 Microsoft Azure의 ID와 액세스 관리 서비스이다.

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/be546679-f8ce-4ea4-9a12-d935a7de47bd)

#### Microsoft Entra ID와 테넌트
- 테넌트 : Microsoft Entra ID의 사용자와 그룹 같은 보안 주체를 제공하는 디렉터리 전용 인스턴스
- 테넌트는 하나 이상의 구독과 연결될 수 있다. (1:N)
- 기본 디렉터리 : Azure에 로그인하면 자동으로 만들어지는 테넌트

#### 구독
- Azure 구독은 Azure 계정과 연결된 클라우드 리소스의 논리적인 관리 단위이며 비용을 청구하는 단위
- 액세스 제어의 경계
- 반드시 하나의 Entra ID 테넌트에 연결돼야 한다.

### 사용자와 그룹

#### Azure 사용자
- 사용자 계증은 Microsoft Entra ID 테넌트에서 만든 사용자 개체

#### 외부 사용자 초대하기

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/696fe0ea-c1f8-491e-b74e-1733a84a12b8)
- 초대 후 해당 메일에서 Accept하면 게스트로 참여 가능

#### Azure 그룹
- 그룹을 통해 리소스 권한을 할당하고 그룹 멤버십을 관리해 사용자에게 권한을 부여하거나 제거하는 방식
- 그룹 유형
  - 보안그룹
  - Microsoft 365

### 역할 기반 액세스 제어(RBAC)
- RBAC를 사용하면 사용자가 액세스할 수 있는 영역과 Azure 리소스, 이 리소스로 할 수 있는 작업을 지정할 수 있다.
- 관리 그룹 또는 구독, 리소스 그룹, 리소스 단위로 액세스 제어를 할 수 있다.

#### 역할 종류
- 소유자 : 할당된 사용 권한 제어 범위 내에서 모든 Azure 리소스를 완전히 관리할 수 있는 권한을 가지며 다른 사용자 계정에 액세스 권한을 할당할 수 있다. 
- 기여자 : 할당된 사용 권한 제어 범위 내에서 모든 Azure 리소스를 완전히 관리할 수 있지만 다른 사용자 계정에 액세스 권한을 할당하지 못한다.
- 독자 : 하락된 사용 권한 제어 범위 내에서 모든 Azure 리소스의 정보만 확인할 수 있으며 변경할 수는 없다.

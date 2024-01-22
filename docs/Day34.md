# Day34

## OpenStack
- 오픈소스 기반의 클라우드 OS

### 하이퍼바이저

- 물리 서버를 가상화 환경으로 만드는 기술
- 1대의 호스트 컴퓨터에서 다수의 운영체체를 동시에 실행하기 위한 논리적 플랫폼
- 유형
  - Native(Bear-metal) : Xen, KVM, VMware ESXi/vSphere, MS Hyper-V 등
  - Hosted : qemu, VMware Workstation/Server, Oracle VirtualBox, MS Virtual PC/Virtual Server 등
 
#### VMware 클라우드 플랫폼
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/6c46a588-fa1f-4028-8ea9-d849f377f3b4)

기타 오픈 소스기반의 클라우드 프로젝트
- 클라우드 스택
- 오픈네뷸라
- 유칼립투스 등

### OpenStack Project
- Nova(openstack compute)
  - 이 서비스는 모든 클러스터 노드 컴퓨터에 설치됩니다.
  - 인스턴스 (프로세서, 메모리, 블록 장치, 네트워크)의 추상화 수준을 관리합니다.
  - 하이퍼바이저(KVM)을 통해 인스턴스의 라이프 사이클을 관리합니다.
  - 가상머신, 베어메탈 서버 생성을 지원하며 (ironic 사용을 통해) 시스템 컨테이너에 대한 지원이 제한적입니다.
  - 해당 서비스를 제공하기 위해 기존 Linux 서버 위에 데몬 세트로 실행됩니다.
- Neutron(openstack networking)
  - 네트워크 연결을 담당합니다.
  - 사용자는 가상 네트워크 및 가상 라우터를 생성하고 floating IP 기능을 통해 인터넷 공급자(IP) 주소를 설정할 수 있습니다.
  - 이 메커니즘 덕분에 인스턴스는 외부로부터 고정 IP 주소를 얻을 수 있습니다.
  - 네트워크 부하분산 서비스와 방화벽, VPN 등의 기능을 모듈로 설치하여 이용할 수 있습니다.
- Keystone(openstack identification)
  - 클라우드 운영 체제의 통합 인증 시스템으로 작동합니다.
  - 사용자 계정의 유효성과 OpenStack 프로젝트 및 역할에 대한 사용자의 일치 여부를 확인합니다.
  - 다른 서비스에 액세스하기 위한 토큰을 제공합니다.
- Glance(openstack image service)
  - 인스턴스의 이미지를 관리하며 인스턴스를 실행하기 위한 템플릿으로 사용할 수 있습니다.
  - 백업과 스냅 샷 생성 기능을 제공합니다.
  - vhd, vmdk, vdi, iso, qcow2 및 ami를 포함한 다양한 형식을 지원합니다.
- Cinder(openstack block storage)
  - 인스턴스를 실행하여 사용할 수 있는 블록 스토리지를 관리합니다.
  - 인스턴스를 위한 영구 데이터 스토리지이며, 스냅 샷을 사용할 수 있습니다.
  - 데이터 저장 및 복원 또는 복제 대부분의 경우 GNU / Linux 서버 기반의 데이터 스토리지는 Cinder와 함께 사용됩니다.
- Swift(openstack object storage)
  - 객체 저장소이며, 사용자가 파일을 저장할 수 있습니다.
  - 분산 아키텍쳐를 갖추고 있어 장애 조치를 위한 수평 확장 및 복제가 가능합니다.
- Heat(openstack orchestration)
  -  AWS CloudFormation 형식의 템플릿을 사용하여 다른 모든 OpenStack을 관리합니다.
  -  대부분의 유형의 리소스(가상 머신, 볼륨, 유동 IP, 사용자, 보안 그룹 등)을 생성 할 수 있습니다.
  -  Ceilometer의 데이터를 사용하여 응용 프로그램 스케일링을 자동으로 만들 수 있습니다.

### openstack 사용사례




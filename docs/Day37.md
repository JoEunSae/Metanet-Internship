# Day37

## Azure

### 가상 네트워크
- SDN과 클라우드의 이점을 통해 뛰어난 확장성
- 프라이빗 네트워크
- 가용성
- 효율성 제공
- 안전한 통신을 위한 트래픽 격리
- 하이브리드 연결
- 기본 outbound 인터넷 가능
- 인바운드 공용IP 주소나 

#### 서브넷
- 네트워크 성능과 속도가 향상된다.
- 네트워크 정체를 줄인다.
- 네트워크 보안을 향상시킨다.
- 네트워크가 비대해지지 않게 한다.
- 관리가 용이하다.

#### 가상 네트워크 만들기

1. 기본사항

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/bf7f698b-ddbe-41a2-9367-42b153eeb299)

2. IP주소

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/90b03c28-bedc-4ace-a079-ae12223d617a)

3. 서브넷 추가

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/22efb2b0-523e-4352-b952-d7139bb6f771)

### Azure Virtual Machine

#### 가상 머신 유형
- Azure 가상 머신 : Azure에서 호스팅 하는 가장 많이 사용하는 일반적인 형태의 가상 머신을 만들 때 사용하는 옵션
- 사전 설정 구성이 포함된 Azure 가상 머신 : 워크로드에 기반한 사전 설정이 포함된 가상 머신을 만들 때 사용하는 옵션
- Azure Arc 가상 머신 : Hyvrid형태로 관리 (op-premise)
- Azure VMware 솔루션 가상 머신 : Azure VMware Solution 프라이빗 클라우드를 만들어 Azure Arc에 온보딩한 후 AVS 가상 머신을 만듭니다.

#### 네트워킹 요소
- 공용 IP 주소 : 공용 Ip 주소와 네트워크 인터페이스를 만들고 서로 연결해야 인터넷 통신이 가능
- 네트워크 보안 그룹 : 가상 머신의 인바운드 및 아웃바운드 트래피을 필터링 하는데 사용
- 네트워크 인터페이스 : NIC역할에 해당
- 가상 네트워크

#### 가상 디스크
- 운영체제 디스크 : VM을 만들 때 운영체제 이미지가 사전 설치된 디스크
- 임시 디스크 : 애플리케이션과 프로세스의 동작에 필요한 단기 저장소로 사용되며 페이징 파일이나 스왑 파일, SQL Server tempdb 등의 데이터를 저장하는데 필요
- 데이터 디스크 : 성능에 민감한 애플리케이션이나 웹 서버의 웹사이트 소스나 데이터베이스 서버의 데이터베이스 파일처럼 애플리케이션 데이터나 사용자가 유지해야 하는 데이터를 저장해야 할 경우 사용

#### 가상머신 만들기

1. 기본사항 설정

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/0e9a30e7-9b34-4c5b-a213-c0ff3c730b13)

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/0e3ddae9-b7b1-4eb7-a1f9-f768c563f4da)

2. 네트워킹

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/351bbb85-5f77-46e0-bd4c-0a3eb1314d94)

3. 멀웨어 방지 프로그램 설치

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/79acf4be-81ad-49d6-9cb6-5f2897054119)

4. RDP다운로드 하고 VM 연결

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/61d94030-bde1-44de-a3ae-4acb3d2df100)

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/fd233b16-cb79-471b-9dee-1d0c5e84bd3e)

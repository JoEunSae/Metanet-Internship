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

#### 프론트/백 서버 만들기

1. Window11을 프론트 서버로 사용, 이전 VM과 다르게 인바운드 포트 허용

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/da20772b-2e25-4c26-9806-58dc00093cd8)

2. 새 디스크 추가

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/62786688-fa3c-4866-afbc-b21036ea5d60)

3. 모니터링 설정 후 만들기

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/60adbfab-01b6-4c99-9d30-aec19cb488f9)

4. window서버에 접속해서

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/9c7a4074-134f-41ab-8c9e-24347c1820fb)

- 웹 서버 역할 설치 `Install-WindowsFeature -Name Web-Server -IncloudManagementTools`
- Deafult.html만들기 `Set-Content -Path "C:\inetpub\wwwroot\Default.htm" -Value "Running Jarvis built on Copilot from host $($env:computername) !"`

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/cf801915-9e53-43fe-86e8-733ed1a1f267)


5. ubuntu linux를 back서버로 생성 (ssh공개키 방식, 공용 인바운드 포트 없음)

6. window terminal에서 back-end서버로 ssh 접속 `ssh -i .ssh/goodbird-key.pem goodbird@172.16.1.5`

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/5092c82f-cd5f-4840-b26e-c059579d133b)

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/b23533de-bf12-44e8-9513-b440cd658b5f)

### Storage

#### 스토리지 개요
- 비정형 데이터 : 데이터가 개체로 존재하며 구조화되지 않아서 연산이 불가능한 데이터 ex) 문서,동영상,이미지 등의 이진 파일
- 반정형 데이터 : 스키마에 해당하는 메타데이터와 데이터가 함께 제공되며 연산 불가능 ex) HTML이나 XML, JSON, YAML 형식 데이터
- 정형 데이터 : 고정된 칼럼에 저장되거나 행과 열에 의해 데이터 속성이 구분되는 데이터 ex) RDBMS 테이블, 스프레드시트

#### Azure 스토리지 특징
- 중복성 보장
- 보안
- 확장성
- 마이크로소프트가 관리
- 유연한 접근성
- 개발과 관리의 편리성

#### 스토리지 계정 유형
- 블록 Blob : 더 작은 개체 데이터를 저장하는 블록 Blob과 추가 Blob 전용 스토리지 계정, 더 빠른 트랜잭션 속도가 필요하거나 일관성 높은 짧은 대기 시간이 필요한 시나리오에 적합
- 파일 공유 : 엔터프라이즈 또는 고성능 애플리케이션에 적합하며 SMB 및 NFS 파일 공유를 모두 지원해야 하는 경우 사용
- 페이지 Blob : 임의 읽기/쓰기 작업이 필요하거나 범위 기반 업데이트가 포함된 파일에 대해 대기 시간이 짧고, 일관적인 높은 성능을 제공해야 할 경우 사용

#### 중복 옵션

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/e8d598b3-0f07-49f8-a6ac-bf36e40a2a9c)

- LRS : 데이터 센터 내에 3번 동기 복사 **동일 리전 하나의 AZ에서**
- ZRS : 3개의 가용성 영역에서 동기 복사 **동일 리전 여러 AZ에서**
- GRS : LRS + 보조 지역 데이터 센터 내에 비동기 복사 후, 보조 지역 내에서 LRS를 사용해 3번 동기 복사 **다른 리전에 하나의 AZ에**
- GZRS : ZRS + 보조 지역 데이터 센터 내에 비동기 복사 후, 보조 지역 내에서 LRS를 사용해 3번 동기 복사 **다른 리전에 여러 AZ에**

#### 스토리지 계정 만들기

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/814c3d1b-3d2f-4405-aea9-cf90d5e37a60)

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/229757da-fbde-4805-a63e-f0ef506ce110)

#### 컨테이너(Blob) 스토리지
- 구조화되지 않은 대량의 비정형 데이터를 저장하기 위한 개체 스토리지 솔루션이다.
- Blobs라는 이름에서 컨테이너로 변경

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/9834cbc4-9093-443e-95ec-baf2bc1d7fcb)


#### 테이블 서비스
- 스키마 없는 키/값 저장소로 설계되었으며 구조화된 NoSQL 데이터용 저장소

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/5d3c8032-37cc-4bd6-9275-2fe1e374c088)


#### 큐 스토리지
- 대규모 비동기 메시지 처리가 필요한 서비스나 애플리케이션에 사용

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/eb4496c1-5079-43cb-93d4-cfc29b9998fc)



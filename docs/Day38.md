# Day38

## 가상 머신 크기 조정과 가용성 구현

### 가상 머신의 크기 

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/9f01540d-2944-4308-a9e6-4e441d592530)

- 서비스를 제공하는 가상 머신의 사용률이 전반적으로 낮은 경우(크기를 줄여 비용을 절약할 수 있음)
- 가상 머신을 늘리지 않고도 크기를 상향 조정해서 서비스 요청을 충분히 소화할 수 있는 경우

### 가상 머신 가용성 구현
- 가용성은 서버와 네트워크, 프로그램 등의 정보 시스템이 정상적으로 사용 가능한 정도를 말한다.
- uptime + downtime

#### 다운타임 시나리오
- 계획되지 않은 하드웨어 유지 관리
- 계획된 유지 관리
- 예측하지 못한 다운타임


#### 가용성 집합
- 단일 데이터 센터에서 가상 머신의 중복성과 가용성을 제공하는 서비스

#### 가용성 영역
- 가용성 영역은 하나 이상의 데이터 센터로 구성된 3개 이상의 영역을 왕복 대기 시간이 2ms 미만인 고성능 네트워크로 연결

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/135bafae-9728-4548-be23-535504d26cb6)


## Azure의 부하 분산 서비스
- 대량의 네트워크 트래픽을 응답 가능한 여러 서버에 효율적으로 분산시켜, 안정적인 서비스를 제공해야 할 때 사용하는 필수 네트워킹 서비스

### Application Gateway(L7)
- 프런트 엔드 IP주소
- HTTP/HTTPS 수신기
- 라우팅 규칙
- 백 엔드 설정
- 상태 프로브
- 백 엔드 풀
- WAF

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/b615b7d5-79a8-4075-9d45-0bcf85f7d47d)

### Nat Gateway
- 조직 네트워크에 연결된 장비들은 프라이빗 IP를 부여하고 인터넷 통신이 필요한 경우만 지정한 공용 IP에 매핑시켜 인터넷의 대상 리소스와 통신을 가능하게 만드는 것
- 가상 네트워크 리소스의 아웃바운드 인터넷 액세스가 필요할 때 VNet의 프라이빗 IP를 공용 IP 주소로 변환하는 Azure NAT 게이트워에 서비스 제공
- NAT 게이트 웨이에 표준 SKU 공용 IP나 공용 IP 접두사, 또는 두가지를 함께 구성하고 하나 이상의 서브넷에 연결하면, 가상 네트워크에서 인터넷으로 트래픽 흐름이 마들어지고, 이 흐름에 대한 응답으로 리턴 트래픽이 허용된다.

### Azure 부하 분산 장치(L4)
- 애플리케이션 게이트웨이처럼 프런트 엔드로 들어오는 인바운드 트래픽을 백엔드 풀의 리소스에 분산시킨다.
- 부산 알고리즘과 규칙, 상태 프로브를 사용해 결정

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/11d733a1-504a-415e-8e7c-15fc9552809b)

## 가상 머신 탄력성 구현

### VMSS(가상 머신 확장 집합)
- VM을 미리 프로비전할 필요 없이 부하 분산된 동일한 설정의 VM 그룹을 만들어 애플리케이션에 고가용성과 탄력성 제공
- 한 곳에서 자동/수동 크기 조정을 포함하여 VM 집합을 관리, 구성하고 업데이트할 수 있다.
- AWS의 autoscaling group과 유사

### VMSS 배포하기

1. 기본 사항

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/47ff1462-8be7-4ee5-a77d-5b126d918d41)

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/870093cf-aadd-4df8-b167-27236813a319)

2. 디스크

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/c0f1a63c-d739-47be-aac2-4062c382aef2)

3. 네트워킹

- vnet과 subnet생성

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/311159aa-ad29-41a9-ace2-cad887f17e76)

- 부하 분산 장치 생성

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/0f44ba06-880b-4767-813a-c70cc62573a1)

4. 확장 중

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/45f5ace0-0808-4ec3-ba2d-5ca52232dd12)

5. 관리

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/77e834ba-b5e6-4aee-8c7a-51af1ed69492)

#### VMSS의 각 VM 인스턴스에 데이터 디스크 연결과 프라이데이 프런트 엔드 웹 서비스 구성을 자동화와 autoscaling이 되는지 확인

1. 디스크 드라이브 및 웹 서비스 구성하는 스크립트
```
#Setup Data Disk
#Get-Disk | Where-Object IsOffline -EQ $true | Set-Disk -IsOffline $false
Get-Disk | Where-Object PartitionStyle -EQ 'RAW' | Initialize-Disk
New-Partition -DiskNumber 2 -UseMaximumSize -DriveLetter X
Format-Volume -DriveLetter X -FileSystem NTFS -NewFileSystemLabel webdata -Confirm:$false

#Setup IIS
Install-WindowsFeature -Name Web-Server -IncludeManagementTools

#Create Default.html
Set-Content -Path "C:\inetpub\wwwroot\Default.htm" -Value "Running FRIDAY Web Service from host $($env:computername) !"
```

2. 스토리지 계정 만들기

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/3e3e5c4b-eb57-44b8-b8ab-6a301449f262)

3. Blob 컨테이너 생성

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/82b6612d-1edc-4a67-ae58-7a73f2052426)

4. blob 아까 생성한 스크립트 업로드

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/7937896c-8f74-4a9a-9a7d-e8cc2389675f)

5. vmss에 확장 프로그램으로 custom script extension설치

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/8b0b59f5-2ba8-45ba-804d-9ed395a11662)

6. vmss확장 중 탭에서 수동으로 vm수 2개로 변경

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/ccdbce55-6315-4046-be47-c8c6c1bdabd5)

7. 오버 프로비저닝으로 3개 vm 생성중

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/bc667ee6-edb5-4f66-b01c-9d1e5606b425)

8. 원격 데스크톱 연결은 위해 vmss 인바운드 규칙 443과 3389허용

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/9e9a816e-ac84-43a5-93c0-918191261245)

9. 원격 데스크톱으로 vm접속

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/c73737e5-da2f-46bc-90c0-177c110fc3f5)

10. 추가된 디스크 확인

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/ce2a0296-20e6-460e-9eb9-3843735de6bc)

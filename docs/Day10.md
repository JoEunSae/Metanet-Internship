# Day10

### 지난시간 복습 진행

**VPC Peering은 1대1 연결이기 때문에 여러 VPC를 연결 할 경우 Transit Gateway로 연결한다.**

---

### Route 53

### Route 53의 라우팅 정책



** 인터넷을 사용하기 위해서는 고유한 IP주소를 가지고 있어야한다. 사설 IP주소를 공유기를 통해 


---

## 2주간 내용으로 Workshop진행

### 1. 클라우드 네트워크 실습한 내용을 설계도로 표현하여 제출하시오.
- 제출 방법: 공유 폴더 / 설계도 제출 ppt에 본인이름 장표로 캡처해서 제출
(S3,AMI,ec2 endpoint,VPC/subnet/routing table/igw/peering/SG/NCAL/ALB/ASG…)

![사진](../images/아키텍처.PNG)

### 2. 본인 prod-VPC를 구축(10.1X.0.0/16) 구축 후
490303288721 소유의 버지니아 리전/vpc-bb5ca5c6 VPC와 Peering 후 172.31.19.47 인스턴스의
user1/abc123으로 접속하라.

- 본인 VPC생성하고 상대방 VPCID와 계정로 Peering요청 요청이 수락되면 상대방 서브넷 주소 라우팅 테이블에 추가
- EC2인스턴스에 접속하여 "ssh 사용자이름@프라이빗IP" 를 통해 상대방 VPC에 접속.


### 3. 탄력적인 인프라 구축하기
- AMI 생성을 위한 ec2 생성 : Advanced 옵션에 user_data를 붙여 넣어 ec2생성-→AMI 만들고 ec2삭제
- ALB 생성 / Target Group 구성
- 시작 템플릿 작성 (내 AMI로)
- ASG 생성
- 부하 테스트

![사진](../images/3번아키텍처.png)





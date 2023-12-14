# Day8

**CIDR(Classless Inter-Domain Routing)** : 인터넷상의 데이터 라우팅 효율성을 향상시키는 IP 주소 할당 방법 

---

## AWS VPC 실습 진행

VPC2개 생성

![사진](../images/VPC생성.png)

2개의 EC2를 생성하는데 하나는 VPC public subnet을 기반으로<br>
하나는 VPC private subnet을 기반으로

이후 2개의 VPC 피어링진행

![사진](../images/피어링.png)

이후 public EC2의 **서브넷 라우팅 테이블**에 private 주소 추가<br>
반대로 private에도 public 주소 추가

![사진](../images/서브넷라우팅테이블1.png)

![사진](../images/서브넷라우팅테이블2.png)

public에서 private으로 접속해 ping을 보내기 위한 인바운드 규칙 추가

![사진](../images/인바운드규칙.png)

ICMP 프로토콜을 추가해 ping을 보낼 수 있게 포트를 열어준다.

![사진](../images/ping.png)

이후 public subnet에서 private에 Ping이 정상적으로 가는걸 확인할 수 있다.

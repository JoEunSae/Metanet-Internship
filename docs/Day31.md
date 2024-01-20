# Day31

## 프로젝트 이어서 진행

1. Nginx-Export가 전달해주는 metric에서 원하는 조건에 경고를 받기 위한 rule설정

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/6dd4032b-8213-4d16-b005-78a3cfaf97f0)
- `expr: nginx_http_requests_total{instance="192.168.49.10:9113", job="nginx"} > 1000`nginx서버에 누적 1000번이상의 request가 요청 되었을 경우 경고를 주는 rule설정

2. prometheus의 alerts에 들어가 rule 설정 확인
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/24da3826-0207-4f41-970a-351201423cf4)

3. 테스트를 위해 nginx웹 서버에 트래픽을 주는 apache-banch설치 후 서버에 요청
- `sudo apt-get install -y apache2-utils`
- `ab -n 10000 -c 10 http://192.168.49.10/`로 nginx에 10000번 request

4. Inactive에서 rule규칙에 해당되면 pending -> Firing상태로 전환된다.
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/215ebd7d-80ca-4538-b38a-2baa7bb577ee)

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/06bd3ff3-4fdb-426d-bd77-7d75ca44536b)

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/4a2a2dd7-81a6-47a8-9b87-3bc24a72f196)

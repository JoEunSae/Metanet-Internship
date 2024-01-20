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

5. 이러한 경고를 slack을 통해 메시지를 받기 위해 alertmanager와 slack연동
- 연동할 slack의 토근을 생성하기 위해 chanel생성

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/33ab7f82-f2f2-48a3-866b-0a563f5790c0)

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/828445c4-3764-49d7-9a09-72b84b397fbe)

- values.yml파일에 slack정보 설정
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/d039e34e-0ecf-4a36-8c86-0c7403ab2b91)
- `slack_api_url`에 slack 토큰 url지정

6. 연동되면 alertmananger가 보내는 경고를 확인할 수 있다.

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/2c3598fc-cc08-406f-a940-b22aba0eeeda)

7. Grafana Dashboard로 모니러팅 하기 위한 prometheus grafana연동

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/1503a3a3-b086-40c4-b082-70da239e512a)


8. 똑같은 방버법으로 이번에는 Node-Export target으로 추가
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/4d42db02-f6e3-480f-8ec2-0c2bf1e11015)

9. Grafana Dashboard에 추가

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/0333652d-1602-4d17-b20c-2cfd6a5a9566)

10. cpu에 부하 테스트를 위해 `stress --cpu 3`수행

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/2c067434-0978-43f8-98b1-f104dc96a413)





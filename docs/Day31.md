# Day31

## 프로젝트 이어서 진행

1. Nginx-Export가 전달해주는 metric에서 원하는 조건에 경고를 받기 위한 rule설정

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/6dd4032b-8213-4d16-b005-78a3cfaf97f0)
- `expr: nginx_http_requests_total{instance="192.168.49.10:9113", job="nginx"} > 1000`nginx서버에 누적 1000번이상의 request가 요청 되었을 경우 경고를 주는 rule설정

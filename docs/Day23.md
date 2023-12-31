# Day23



**yml파일을 편하게 작성하기 위해 vscode설치**
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/3c17a715-016c-493c-aba7-23c12a6f4201)

### compose.yml파일로 컨테이너 실행시켜 wordpress, mysql 연동하기

1. vscode로 docker-compose.yml파일 작성

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/54cacc0e-bf2b-4e9c-b49f-1282a25a73e5)

2. `docker-compose up -d`로 컨테이너 실행

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/e7aa2163-bebb-4e9f-a31c-3f3130d95070)

3. 해당 경로로 접근

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/51abb8f5-6e52-471e-9180-43e2e3295c88)

### Prometheus로 모니터링하기

**프로메테우스: 정보수집,모니터링**

**Prometheus Node Exporter는 하드웨어의 상태와 커널 관련 메트릭을 수집하는 메트릭 수집기**

1. Prometheus Node Exporter설치

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/e5dd7e3e-5cfc-43d6-94d7-f95d4f84f1ba)

2. centOS에서 Node Export 설치 `tar xvzf node_exporter-1.7.0.linux-amd64.tar.gz`

3. Node Export실행 ./node_exporter

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/64b93b85-c1fa-450a-8a1d-116f5d37e5c8)


4. Node Export가 보내는 정보를 받을 ubuntu에 prometheus 컨테이너 실행 `docker run -d -p 9090:9090 prom/prometheus`

5. centos에서 `curl http://localhost:9100/metrics`로 메트릭 확인

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/a0541a4b-8d1b-4451-bca3-b7b8d66d2d81)

6.  `docker cp awesome_stonebraker:/etc/prometheus/prometheus.yml .`

7.  복사한 prometheus.yml파일 수정

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/d7275b1b-2891-4d71-b8b1-d960478d3d77)

8. `docker cp prometheus.yml  awesome_stonebraker:/etc/prometheus/prometheus.yml`로 수정한 파일 다시 붙여넣어준다.

9.  `sudo firewall-cmd --add-port=9100/tcp --permanent` 로 방화벽을 해제 해준고 `sudo firewall-cmd --reload`로 방화벽 reload

10.  unbuntu에서도 `curl http://192.168.56.11:9100/metrics`로 메트릭 확인 가능

11.  해당 ip로 접근해서 target확인

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/42695ef4-ebe7-4b6d-a8ab-71a6731cde7b)

12. 시스템에서 현재 사용 중이지 않은(free) 메모리의 양을 바이트 단위로 표시

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/f17cb79a-e915-4f18-a25f-fc3891d2edbc)


### Grafana
프로메테우스에 쌓여있는 데이터를 보다 좋은 UI로 확인하기 위해서 사용


1. `docker run -d --name=grafana -p 3000:3000 grafana/grafana` grafana컨테이너 실행


2. prometheus와 grafana연결
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/b662aa3e-73cb-44d6-8ccc-c485104e205c)

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/7d06f1fb-33b8-4df5-a223-8747054f3b7e)

3. grafana UI로 모니터링

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/f76e02dd-9ed5-4d7e-87d6-ff3c1a488153)


#### compose.yml로 grafana와 prometheus 컨테이너 실행하기

1. docker-compose.yml파일 작성

```yml
version: '3'
services:
  grafana:
    image: grafana/grafana
    container_name: grafana
    restart: always
    ports:
      - '3000:3000'
    volumes:
      - gra-vol:/var/lib/grafana
    networks:
      - mynet
    depends_on:
      - prometheus
    # environment:
    #   - GF_SECURITY_ADMIN_PASSWOD=admin

  
  prometheus:
    image: prom/prometheus
    container_name: prometheus
    user: root
    ports:
      - 9090:9090
    networks:
      - mynet
    volumes:
      - pro-vol:/prometheus

volumes:
  gra-vol: {}
  pro-vol: {}

networks:
  mynet:
    external: true
```

3. `docker-compose up -d`로 컨테이너 실행

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/112b1d9d-f32a-4200-8ebe-380951f57763)
![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/20d63816-ef9a-45a6-b73a-0bcfb485e44c)


### nginx, nginx-prometheus-exporter, prometheus, grafana 연동하기

**nginx의 정보를 nginx-prometheus-exporter를 사용하여 prometheus에 전달하여 확인한다 좀더 정리된 화면으로 확인하기 위해 prometheus와 grafana를 연동하여 모너터링 한다.**


1. nginx 컨테이너 실행 `docker run --rm -p 8080:80 nginx`

2. `docker run -p 9113:9113 nginx/nginx-prometheus-exporter:1.0.0 --nginx.scrape-uri=http://192.168.56.10:8080/stub_status`로 nginx의 정보를 전달할 nginx-prometheus-exporter 컨테이너 구동

3.  `docker cp elegant_villani:/etc/nginx/nginx.conf/default.conf .` default.conf파일을 가져와 아래 부분을 추가해준다.

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/e751c742-df6b-44c0-8c9a-eeb8182cd780)

4. `vi prometheus.yml` yml파일도 수정

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/245fda75-6f8a-40d2-ad55-8a3012fc541c)

5. prometheus접속해서 matric확인

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/85e639e1-6226-454c-bafe-e09f705de5e5)

6. grafana도 연동해서 확인

![image](https://github.com/JoEunSae/Metanet-Internship/assets/83803199/bd1cbe68-8839-44dc-80c7-d65e1769a678)




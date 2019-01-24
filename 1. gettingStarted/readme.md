# Telegraf - InfluxDB - Grafana 모니터링 기본
TIG를 사용한 가장 기본적인 구성을 시작해 보겠습니다. 서버 한대에 Telegraf 에이전트, InfluxDB, Grafana를 몰아넣고 어떻게 설치하며 구성하는지 살펴봅니다.
테스트 OS는 리눅스 [Ubuntu 16.04 LTS] 입니다.
<br>
<img src=https://github.com/chupark/TIG_Monitoring/blob/master/1.%20gettingStarted/img/1arc.png />
## 1. InfluxDB
InfluxDB는 Telegraf 에이전트로 수집하는 데이터를 저장하기 위한 Time Series Database Management System (TSDB) 입니다
### 1.1. InfluxDB 

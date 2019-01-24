# Telegraf - InfluxDB - Grafana 모니터링 기본
TIG를 사용한 가장 기본적인 구성을 시작해 보겠습니다. 서버 한대에 Telegraf 에이전트, InfluxDB, Grafana를 몰아넣고 어떻게 설치하며 구성하는지 살펴봅니다.
테스트 OS는 리눅스 [Ubuntu 16.04 LTS] 입니다.<br>
<img src=https://github.com/chupark/TIG_Monitoring/blob/master/1.%20gettingStarted/img/1arc.png />

## 1. InfluxDB
InfluxDB는 Telegraf 에이전트로 수집하는 데이터를 저장하기 위한 Time Series Database Management System (TSDB) 입니다 <br>
트렌드 조사에 따르면 현재 가장 인기있는 TSDB 입니다. InfluxDB는 저장 및 조회 성능, 저장 공간 효율성, 유연한 확장 가능 등의 장점이 있지만, 아쉽게도 오픈소스 버전에서는 클러스터링 등의 고급 기능을 사용할 수 없습니다. 하지만 IoT 장비 등 엄청난 양의 데이터가 쏟아지는게 아니라면 InfluxDB로 충분히 처리가 가능합니다.

<img src=https://github.com/chupark/TIG_Monitoring/blob/master/1.%20gettingStarted/img/tsdbTrend.png />
출처 : https://db-engines.com/en/ranking_trend/time+series+dbms
<br>
### 1.1. InfluxDB 

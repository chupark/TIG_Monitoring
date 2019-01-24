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

### 1.1. InfluxDB 설치
인터넷이 되는 환경이라면 InfluxDB 설치는 매우 간단합니다. InfluxData에서 제공하는 <a href='https://portal.influxdata.com/downloads/'>다운로드</a> 페이지에서 바로 다운로드 및 설치가 가능합니다.

````bash
wget https://dl.influxdata.com/influxdb/releases/influxdb_1.7.3_amd64.deb
sudo dpkg -i influxdb_1.7.3_amd64.deb
````

## 2. Telegraf
Telegraf는 TICK Stack의 일부이며, 메트릭을 수집하고 보고하는 플러그인 기반 서버 에이전트 입니다. Telegraf는 Docker 같은 컨테이너 혹은 시스템에서 직접 다양한 메트릭, 이벤트 및 로그를 찾으며, 타사 API에서 메트릭을 가져올 수 있는 다양한 <a href='https://github.com/influxdata/telegraf/tree/master/plugins/inputs'>input 플러그인</a>을 제공합니다. 또한 InfluxDB, Kafka등 다양한 <a href='https://github.com/influxdata/telegraf/tree/master/plugins/outputs'>output 플러그인</a>을 가지고 있습니다.

### 2.1. Telegraf 설치
````bash
wget https://dl.influxdata.com/telegraf/releases/telegraf_1.9.3-1_amd64.deb
sudo dpkg -i telegraf_1.9.3-1_amd64.deb
````

## 3. Grafana
Grafana는 DBMS에 저장된 메트릭을 조회하고, 시각화하고, 경고하고, 이해할 수 있게 해줍니다. 대시보드를 꾸미기 위한 다양한 플러그인과 여러 기능등을 제공합니다.

### 3.1. Grafana 설치
````bash
wget https://dl.grafana.com/oss/release/grafana_5.4.2_amd64.deb
sudo apt-get install -y adduser libfontconfig
sudo dpkg -i grafana_5.4.2_amd64.deb
````


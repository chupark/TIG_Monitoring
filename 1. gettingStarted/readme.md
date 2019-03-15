# Telegraf - InfluxDB - Grafana 모니터링 기본
TIG를 사용한 가장 기본적인 구성을 시작해 보겠습니다. 서버 한대에 Telegraf 에이전트, InfluxDB, Grafana를 몰아넣고 어떻게 설치하며 구성하는지 살펴봅니다.
테스트 OS는 리눅스 [Ubuntu 16.04 LTS] 입니다.<br>
<img src=https://github.com/chupark/TIG_Monitoring/blob/master/1.%20gettingStarted/img/1arc.png />

<br/>

## 1. InfluxDB
InfluxDB는 Telegraf 에이전트로 수집하는 데이터를 저장하기 위한 Time Series Database Management System (TSDB) 입니다 <br>
트렌드 조사에 따르면 현재 가장 인기있는 TSDB 입니다. InfluxDB는 저장 및 조회 성능, 저장 공간 효율성, 유연한 확장 가능 등의 장점이 있지만, 아쉽게도 오픈소스 버전에서는 클러스터링 등의 고급 기능을 사용할 수 없습니다. 하지만 IoT 장비 등 엄청난 양의 데이터가 쏟아지는게 아니라면 InfluxDB로 충분히 처리가 가능합니다.

<img src=https://github.com/chupark/TIG_Monitoring/blob/master/1.%20gettingStarted/img/tsdbTrend.png />
출처 : https://db-engines.com/en/ranking_trend/time+series+dbms

### 1.1. InfluxDB 설치
인터넷이 되는 환경이라면 InfluxDB 설치는 매우 간단합니다. InfluxData에서 제공하는 <a href='https://portal.influxdata.com/downloads/'>다운로드</a> 페이지에서 바로 다운로드 및 설치가 가능합니다.

````bash
wget https://dl.influxdata.com/influxdb/releases/influxdb_1.7.3_amd64.deb
sudo dpkg -i influxdb_1.7.3_amd64.deb
````
<img src= 'https://github.com/chupark/TIG_Monitoring/blob/master/1.%20gettingStarted/img/%EB%85%B9%ED%99%94_2019_01_24_10_11_55_661.gif' />

<br/>

## 2. Telegraf
Telegraf는 TICK Stack의 일부이며, 메트릭을 수집하고 보고하는 플러그인 기반 서버 에이전트 입니다. Telegraf는 Docker 같은 컨테이너 혹은 시스템에서 직접 다양한 메트릭, 이벤트 및 로그를 찾으며, 타사 API에서 메트릭을 가져올 수 있는 다양한 <a href='https://github.com/influxdata/telegraf/tree/master/plugins/inputs'>input 플러그인</a>을 제공합니다. 또한 InfluxDB, Kafka등 다양한 <a href='https://github.com/influxdata/telegraf/tree/master/plugins/outputs'>output 플러그인</a>을 가지고 있습니다.

### 2.1. Telegraf 설치
````bash
wget https://dl.influxdata.com/telegraf/releases/telegraf_1.9.3-1_amd64.deb
sudo dpkg -i telegraf_1.9.3-1_amd64.deb
````
<img src='https://github.com/chupark/TIG_Monitoring/blob/master/1.%20gettingStarted/img/%EB%85%B9%ED%99%94_2019_01_24_10_14_07_746.gif' />

<br/>

## 3. Grafana
Grafana는 DBMS에 저장된 메트릭을 조회하고, 시각화하고, 경고하고, 이해할 수 있게 해줍니다. 대시보드를 꾸미기 위한 다양한 플러그인과 여러 기능등을 제공합니다.

### 3.1. Grafana 설치
````bash
wget https://dl.grafana.com/oss/release/grafana_5.4.2_amd64.deb
sudo apt-get install -y adduser libfontconfig
sudo dpkg -i grafana_5.4.2_amd64.deb
````
<img src='https://github.com/chupark/TIG_Monitoring/blob/master/1.%20gettingStarted/img/%EB%85%B9%ED%99%94_2019_01_24_10_18_23_912.gif' />

### 3.2. Grafana 접속
Grafana에 접속하기 위해선 3000포트가 열려있어야 합니다. http://서버ip:3000 에 접속하여 로그인 합니다.
초기 계정 정보는 id/pw : admin/admin 입니다.<br/>
<img src='https://github.com/chupark/TIG_Monitoring/blob/master/1.%20gettingStarted/img/grafana_login1.png'/>
<br/>
<br/>
안내에 따라 비밀번호를 변경 후 로그인 합니다.
<img src='https://github.com/chupark/TIG_Monitoring/blob/master/1.%20gettingStarted/img/grafana_login2.png'/>

### 3.3. 데이터 소스 연결
Grafana 대시보드에 그래프를 그리기 위해 데이터 소스 연결이 필요합니다. InfluxDB를 사용하므로 InfluxDB 데이터소스 연결을 필요로 합니다. <br/>
<img src='https://github.com/chupark/TIG_Monitoring/blob/master/1.%20gettingStarted/img/%EB%85%B9%ED%99%94_2019_03_15_14_58_30_259.gif'/>
<br/>
<br/>

### 3.4. 대시보드 추가
그래프를 그릴 대시보드를 추가합니다. 대시보드의 디렉터리를 만들고, 이름을 설정할 수 있습니다. <br/>
<img src='https://github.com/chupark/TIG_Monitoring/blob/master/1.%20gettingStarted/img/%EB%85%B9%ED%99%94_2019_03_15_14_59_32_542.gif'/>
<br/>
<br/>

### 3.5. 그래프를 추가하여 이름 변경
대시보드에 그래프를 추가하여 이름을 원하는대로 변경할 수 있습니다. 아래 그림에선 그래프의 이름을 CPU로 설정 합니다. <br/>
<img src='https://github.com/chupark/TIG_Monitoring/blob/master/1.%20gettingStarted/img/%EB%85%B9%ED%99%94_2019_03_15_15_00_15_623.gif'/>
<br/>
<br/>

### 3.6. 데이터 쿼리
#### 3.6.1. 쿼리 작성
그래프에서 사용할 데이터 소스 (InfluxDB-Test)를 선택 후 쿼리를 작성합니다. <br/>
<img src='https://github.com/chupark/TIG_Monitoring/blob/master/1.%20gettingStarted/img/%EB%85%B9%ED%99%94_2019_03_15_15_00_42_779.gif'/>
<br/>
<br/>

#### 3.6.2. 같은 그래프에 새로운 쿼리 작성
Add Query 버튼을 클릭하여 여러개의 쿼리를 추가하여 그래프를 만들 수 있습니다.<br/>
<img src='https://github.com/chupark/TIG_Monitoring/blob/master/1.%20gettingStarted/img/%EB%85%B9%ED%99%94_2019_03_15_15_02_27_396.gif'/>
<br/>
<br/>

### 3.7. 그래프 꾸미기
#### 3.7.1. 그래프 y축 데이터 단위 설정
Unit을 변경하여 Y축에 나타내는 데이터위 단위를 설정할 수 있습니다. <br/>
<img src='https://github.com/chupark/TIG_Monitoring/blob/master/1.%20gettingStarted/img/%EB%85%B9%ED%99%94_2019_03_15_15_03_31_56.gif' />
<br/>
<br/>

#### 3.7.2. 그래프에 데이터 값 표시
Legend 탭에서 그래프에 데이터를 표시할 수 있습니다. <br/>
<img src='https://github.com/chupark/TIG_Monitoring/blob/master/1.%20gettingStarted/img/%EB%85%B9%ED%99%94_2019_03_15_15_04_06_762.gif' />
<br/>
<br/>

### 3.8. 데이터 새로고침 주기 설정 및 저장
데이터 새로고침 주기와 현재 설정을 저장합니다. 저장시 바뀐 내용을 입력할 수 있습니다.<br/>
<img src='https://github.com/chupark/TIG_Monitoring/blob/master/1.%20gettingStarted/img/%EB%85%B9%ED%99%94_2019_03_15_15_05_00_620.gif' />

정리 필요

# InfluxDB 
InfluxDB는 시계열 데이터베이스 중 하나로, 쿼리 방법 등 많은 부분이 RDB와 비슷하지만 모든 Row가 Time이라고 불리는 고유한 시간값을 가진다.
InfluxDB는 사용자 ID, 게시글 등 관계형 데이터를 저장하는것이 아닌 시스템 로그등 지속적으로 수집되는 값들을 시간차원에서 쉽게 다룰 수 있게 해준다.

## 설치 문서 참조
url 여기에

## 용어 설명
- Database : RDB의 그것
- measurement : Database 안에 저장되는 측정 값들, 예를 들어 log 라는 Database에 로그들을 저장할 때 app1, app2, app3 이런식으로 measurement를 줄 수 있다.
- Tag : RDB의 index라고 볼 수 있다. Tag는 Key와 Value가 있다.
    - Tag Key : Hostname, Region 등 RDB의 index를 가지는 Column
    - Tag Value : server1, server2 // Korea, China등 말 그대로 Tag Key의 값 row
- Field : 측정값들 Index를 가지지 않는다. Tag와 마찬가지로 Key와 Value가 있다
    - Field Key : CPU, Memory 등 RDB의 index가 없는 Column
    - Field Value : 100, 10 // 100, 10 등 Field Key의 값 row

set, series, point등 더 추가 

## 데이터 타입
- Float : Field vaules IEEE-754-64-bit floating-point numbers
- Integer : Field vaules Signed 64-bit integers
- String : Measurements, tag keys, tag values, field keys, field values 에 사용 가능, 최대 길이 64kb
- Boolean : Field vaules [ t || T || true || True || TRUE ]
- Timestamp : Timestamps [ f || F || false || False || FALSE ]

## 라인 프로토콜
influxdb에 데이터를 insert 시키기 위한 프로토콜 반드시 지켜야함
```
<measurement>[,<tag_key>=<tag_value>[,<tag_key>=<tag_value>.....]] <field_key>=<field_value>[,<field_key>=<field_value>...] [<timestamp>]
```
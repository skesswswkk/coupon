# 단일 서버로 4,000/TPS 이상 커버 가능 선착순 쿠폰 시스템


## 사용기술
- Java 17, Spring Boot 3.1, MySQL, Redis, Gradle, Locust, Promethous, Grafana

## 시나리오
- 이벤트 기간내에(ex 2023-11-03일 오후 1시 ~ 2023-11-04일 오후 1시) 발급이 가능합니다.
- 선착순 이벤트는 유저당 1번의 쿠폰 발급만 가능합니다.
- 선착순 쿠폰의 최대 쿠폰 발급 수량을 설정할 수 있어야합니다.

## 프로그램 주요 기능

### 쿠폰 발급 검증
- 발급 기한
- 발급 수량
- 중복 발급

### 쿠폰 발급 수량 관리
- Redis Set기반 재고 관리

### 비동기 쿠폰 발급
- Redis List (발급 Queue)
- Queue Polling Scheduler 

## 성능 및 결과

### server spec
- coupon-api, coupon-consumer -> t2.medium (2core, 4G) 
- Mysql -> db.t3.micro (free-tier)
- Redis -> cache.t3.micro	(free-tier)

### Load Test
- Runtime : 5m  
- Number of Users : 5,000

### Request Statics
- Total Requests : 1,696,253
- Failed Requests : 1,315
- Failure rate : 0.077%   
- RPS : 4958  
  
### Response Statics
- p50 : 900 ms  
- p70 : 1200 ms  
- p90 : 1500 ms  
- p90 : 2000 ms  
- p99 : 3600 ms  
- max : 14000 ms

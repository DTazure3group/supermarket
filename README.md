# 3 Team Project
![rentbook](https://user-images.githubusercontent.com/89369983/131526770-d23daef7-0e18-4dff-8c56-419204bfd670.PNG)
## 도서 대여관리 시스템   

# Table of contents

- [도서 대여 관리 시스템](#---)
  - [서비스 시나리오](#서비스-시나리오)
  - [체크포인트](#체크포인트)
  - [분석/설계](#분석설계)
  - [구현:](#구현)
    - [DDD 의 적용](#ddd-의-적용)
    - [폴리글랏 퍼시스턴스](#폴리글랏-퍼시스턴스)
    - [폴리글랏 프로그래밍](#폴리글랏-프로그래밍)
    - [동기식 호출 과 Fallback 처리](#동기식-호출-과-Fallback-처리)
    - [비동기식 호출 과 Eventual Consistency](#비동기식-호출-과-Eventual-Consistency)
  - [운영](#운영)
    - [CI/CD 설정](#cicd설정)
    - [동기식 호출 / 서킷 브레이킹 / 장애격리](#동기식-호출-서킷-브레이킹-장애격리)
    - [오토스케일 아웃](#오토스케일-아웃)
    - [무정지 재배포](#무정지-재배포)


# 서비스 시나리오

기능적 요구사항

A. 대여
1. 고객이 서적 대여 시 이미 대여중인 상태의 서적은 대여  할수 없다
2. 고객이 서적 대여 시 반납일은 대여일로 부터 7일 후로 자동 설정된다  
3. 고객이 서적 반납 시 해당 서적은 대여 가능한 상태로 변경 된다 
4. 고객이 반납일 보다 지연되면 고객에게 지연 카톡 알람 메세지를 보낸다

B. 매장 & 서적 
1. 관리자는 대여 서적 정보를 등록/삭제/수정 관리 할수 있다.
3. 관리자는 매장을 등록/삭제/수정 관리 할수 있다 
 
 C. 고객
 1. 고객은 회원 가입할수 있다
 2. 고객은 적럽금을 예치할수 있다  


비기능적 요구사항
1. 트랜잭션
    1. 고객 적립금이 서적 대여 금액 보다 적다면 서적 대여는 불가하다  Sync 호출 
1. 장애격리
    1. 상점관리 기능이 수행되지 않더라도 서적 대여 기능은 365일 24시간 받을 수 있어야 한다  Async (event-driven), Eventual Consistency
    1. 대여시스템이 과중되면 사용자를 잠시동안 받지 않고 대여 진행을 잠시후에 하도록 유도한다  Circuit breaker, fallback
1. 성능
    1. 관리자는 매장 관리에서 대여현황을 조회 할 수 있어야 한다  CQRS
    1. 반납 지연 되면 대상 고객에게 카톡 등으로 알림을 줄 수 있어야 한다  Event driven


# 분석/설계


## AS-IS 조직 (Horizontally-Aligned)
![asis](https://user-images.githubusercontent.com/89369983/132091689-4094136c-c6fa-477e-b614-b478eed1fa0f.PNG)

## TO-BE 조직 (Vertically-Aligned)
![tobe](https://user-images.githubusercontent.com/89369983/132091699-2f0f9164-55da-49d5-a35f-dc6eba7eed19.PNG)

## Event Storming 결과
* MSAEz 로 모델링한 이벤트스토밍 결과:  http://msaez.io/#/storming/


### 이벤트 도출
![Event 도출](https://user-images.githubusercontent.com/33479996/132121070-a56d6e5a-d292-4e3d-8118-05c0b602e945.PNG)


### 부적격 이벤트 탈락
TBD


### 액터, 커맨드 부착하여 읽기 좋게
TBD

### 어그리게잇으로 묶기
TBD



### 바운디드 컨텍스트로 묶기

TBD



### 폴리시 부착 (괄호는 수행주체, 폴리시 부착을 둘째단계에서 해놔도 상관 없음. 전체 연계가 초기에 드러남)

TBD

### 폴리시의 이동과 컨텍스트 매핑 (점선은 Pub/Sub, 실선은 Req/Resp)

TBD

### 완성된 1차 모형

TBD

### 1차 완성본에 대한 기능적/비기능적 요구사항을 커버하는지 검증
TBD

### 모델 수정

TBD

### 비기능 요구사항에 대한 검증

TBD



## 헥사고날 아키텍처 다이어그램 도출
    
TBD



# 구현

TBD

# 운영

TBD


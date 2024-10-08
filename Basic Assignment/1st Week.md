> # Preview
---
### 시작하기 전에 알고 있으면 좋은 개념
함수: 프로그램 소스 코드에서 일정한 동작을 수행하는 코드들 (엑셀함수랑 똑같은 거!)

- SQL을 처음 접한다면?

일단 실행해보고 ⇒ 쿼리문을 완성하는 것에 초점을 맞추기


> # 1-1. BigQuery 기초 지식
---
### 데이터 저장 형태
- Database: 데이터의 저장소
- Table: 데이터가 저장된 공간
- Database>Table>Row(행,가로)&Column(열,세로)

### 데이터가 저장되는 장소
- DBMS(Database Management System)에 저장 (MySQL, Oracle, PostgreSQL 등)
- MySQL, Oracle, PostgreSQL과 같은 데이터베이스의 특징: OLTP
  - OLTP(Online Transaction Processing)란?
      - 거래를 하기 위해 사용되는 데이터베이스
      - 데이터가 무결하다: 보류, 중간 상태가 없다.
      - 데이터의 추가(INSERT), 데이터의 변경(UPDATE)이 많이 발생.

### SQL(Structurer Query Language)
- SQL: 데이터베이스에서 ***데이터를 가지고 올 때 사용**하는 언어

### 데이블에 저장된 데이터의 형태
| 구조 | 모양 | 의미 |
|:---:|:---:|:---:|
| 행(Row) | 가로 | 하나의 Row가 하나의 고유한 데이터 |
| 열(Column) | 세로 | 각 데이터의 특정 속성 값 |

*위 표에서 '열'은 '구조, 모양, 의미', '행'은 '행, 열'

### OLAP와 데이터 웨어하우스(DW)의 등장
OLTP의 한계: 속도, 기능부족

OLAP: Online Analytical Processing
- 분석을 위한 기능 제공

데이터 웨어하우스
- 데이터를 한곳에 모아서 저정
- 여러 곳에 저장된 데이터 예시: Database, 웹(크롤링), 파일, API의 결과 등


> # 1-2. BigQuery 환경 설정
---
### BigQuery의 환경 구성 요소
1) 프로젝트: 하나의 프로젝트에 여러 데이터셋이 존재
2) 데이터셋: 하나의 데이터셋에 다양한 테이블이 존재
3) 테이블: 행과 열로 이루어진 데이터가 저장
*프로젝트>데이터셋>테이블

### BigQuery 실행 결과
![image](https://github.com/user-attachments/assets/d84a4010-6726-4e0e-af32-507c062952bf)
--
![image](https://github.com/user-attachments/assets/bd0c0feb-05b8-4851-9f61-19cbeab8de5d)
Battle 테이블에는 파티션이 있기 때문에 모양이 다르다!


> # 2-1. 데이터 활용 Overview
---
### 데이터를 활용하는 과정
<img src="https://github.com/user-attachments/assets/ff45ebf1-cb3c-45d0-8a8c-47aec906a4aa" width="640" height="480"/>
출처: https://developnote.tistory.com/75 [범범범즈의 개발 노트:티스토리]
__*주황색 박스 안 부분이 SQL로 처리할 수 있는 부분!__

원하는 데이터를 탐색할 때, 단일 자료와 다량의 자료를 연결해서 조건(필터링), 추출, 변환, 요약 과정을 거쳐야한다.

SQL을 통해 데이터 탐색&데이터 결과 검증을 진행한다.

- 문제 정의 시

MECE: 중복이 없고, 상호 배제적이다.

- 지표 정의 시

Metric: 지표 또는 성과를 나타내는 값, 데이터를 측정하거나 분석하기 위해 정의된 계산이나 집계


> # 2-2. 저장된 데이터 확인하기 (데이터베이스, 데이터 웨어하우스, ERD)
---
### SQL 쿼리를 작성하기 전에
- 데이터가 어떻게 저장되어 있는지 생각해보기
- 어떤 데이터가 저장되어 있는지 생각해보기
- 각 컬럼의 의미는 무엇인지 생각하기

### 데이터를 추출하기 전에
- 데이터 웨어하우스에 **데이터가 어떻게 저장**되어 있는지 확인하기

### ERD
- ERD(Entity Relationship Diagram): 데이터베이스 구조를 한 눈에 알아보기 위해 사용.
![image](https://github.com/user-attachments/assets/dbe540fc-f946-4cda-898f-a44c498b6bca)

*ERD가 없다면? 모든 데이터베이스를 보면서 어떤 테이블과 컬럼이 존재하는지, 다른 테이블과 연결할 때 어떤 컬럼끼리 연결하는지, 각 컬럼의 값이 의미하는 것은 무엇인지 파악하기

### 포켓몬 세상엔 어떤 데이터가 존재할까요?
- 포켓몬, 트레이너, 트레이너가 잡은 포켓몬, 트레이너가 도전한 유저 배틀 ...

### 이커머스 산업에는 어떤 데이터가 존재할까요?
- 상품, 유저, 주문, 장바구니에 담은 물건, 웹페이지 접근 수

### ERD 예시
![image](https://github.com/user-attachments/assets/283819a0-ad5a-4153-86e5-5628c99fe51b)

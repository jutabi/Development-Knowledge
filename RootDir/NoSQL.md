# NoSQL
- SQL을 사용하지 않는 DBMS
- 관계형 모델을 사용하지 않는다. (주로 클러스터링하여 사용)
- 스키마 없이 동작한다.
- 대부분이 오픈소스이다.

## 1. 특징
### 1.1 CAP
- Eric Brewer 에 의해 발표된 분산 컴퓨팅 이론
- Consistency, Availability, Partitioning 세가지 특징을 가지며 이중 두가지만 만족할 수 있다는 이론
#### - Consistency
- 모든 노드(클라이언트)가 동시에 데이터를 조회했을 때 같은 결과값을 갖는다.
#### - Availability
- 모든 노드(클라이언트)는 언제나 읽기와 쓰기가 가능하다.
    - 성공하거나 실패하거나 모든 요청에 대한 응답을 한다.
#### - Partition Tolerance
- 시스템은 장애가 일어나더라도 정상적인 서비스 수행이 가능해야 한다.
    - 데이터가 손실되거나 시스템의 일부에 장애가 있어도 전체 시스템은 항상 정상 작동하여아 한다.
#### - 종류
- 2개의 속성만을 가질 수 있음으로 CA, CP, AP 타입으로 나눌 수 있다.
- 하지만 클러스터링 환경에서 Partition Tolerance 특징은 필수적인 요소이기에 대부분은 CP, AP 타입
- CP
    - 데이터의 무결성을 만족, 시스템 일부의 오류를 허용하기 위해 쿼리 응답시 지연 발생 가능
- AP
    - 서비스 가용성을 만족, 성능을 위해 데이터 무결성을 희생, 쿼리 응답시 지연이 없지만 무결성을 보장하지 않음
    
### 1.2 분산 구조 (클러스터링)
- 기존의 RDBMS와는 다르게 여러 장치들을 클러스터해 (수평적 확장) 데이터를 처리한다.
- 분산형 구조를 통해 데이터를 여러 서버에 분산하여 저장하는 방식이다.
- 특정 서버에 문제가 생겨도 전체 서비스에는 영향을 주지 않는다.
### 1.3 Schema-less
- 관계형 데이터베이스와 다르게 스키마를 사용하지 않는다.
- 데이터 구조를 미리 정의할 필요가 없고 변경이 가능하여 비형식 데이터의 저장에 용이하다.
### 1.4 No relationship
- 테이블간의 관계가 없다. 외래키 같은 설정이 불가능하여 JOIN연산도 불가능하다.
    - join 연산을 가능하게 할 수는 있다.
### 1.5 No ORM
- 기존의 RDBMS는 저장소 내에 저장되는 형태와 테이블의 형태가 달라 ORM이 필요하였다. 
하지만 NoSQL은 저장소 내의 구조를 상관하지 않고 바로 저장하게되어 ORM이 필요하지 않다.

## 2. 종류
### - Key-Value
- 키와 값의 쌍으로 구성된 데이터가 저장된다.
    - 데이터에 접근하기 위한 Key
    - 모든 데이터를 수용할 수 있는 Value
- 쿼리 사용이 불가능하여 키값으로 데이터를 불러와 서비스 내에서 처리해야 한다.
> Amazon Dynamo DB, Redis ...
### - Document
- JSON, XML같은 Collection 데이터 모델 구조를 사용한다.
- 키와 도큐먼트의 쌍으로 데이터가 저장된다.
    - Key-Value 구조의 Value와 다른 점은 계층적 형태인 도큐먼트로 저장된다.
- ORM이 필요없다. 객체를 도큐먼트로 저장할 수 있기 때문
> MongoDB, CouchDB, MarkLogic ...
### - Column-family (Wide Columnar Store or Big table)
- Key 값을 가지고 그 Key는 Row, Column-family, Column-name을 가진다.
    - Row: 키 값
    - Column-family: 연관된 데이터들
    - Column-name: 이름
> HBase, Cassandra ...
### - Graph
- 그래프로 데이터를 표현하기 위해 고안됨
- 데이터들의 관계를 표현한다.
# RDB와 NoSQL에서의 클러스터링/레플리케이션 방식

### 클러스터링

여러 개의 DB를 **수평적인** 구조로 구축하는 방식

- **동기 방식**으로 노드들 간의 데이터를 동기화

### 레플리케이션

여러 개의 DB를 이용하여 **수직적(Master-Slave)** 구조를 활용하여 DB의 부하를 분산 시키는 기술

- Master : INSERT, UPDATE, DELETE
- Slave : SELECT

### 샤딩

**데이터를 조각내 분산 저장하는 데이터 처리 기법**

- 같은 테이블 스키마를 가진 데이터를 다수의 데이터베이스에 분산하여 저장하는 방법
- Sharding Key : 나눠진 Shard 중 어떤 shard를 선택할 지 결정하는 키, 결정방식에 따라 Sharding 방법이 나누어짐

# 클러스터링

## RDB의 클러스터링(MySQL)

![image](https://github.com/everyware-ie/CS/assets/102847513/304002ae-895d-4f25-b3ab-b813942ecf28)

1. 1개의 노드에 쓰기 트랜잭션이 수행되고, COMMIT을 실행한다.
2. 실제 디스크에 내용을 쓰기 전에 **다른 노드로 데이터의 복제를 요청한다**.
3. 다른 노드에서 복제 요청을 수락했다는 신호(OK)를 보내고, 디스크에 쓰기를 시작한다.
4. 다른 노드로부터 신호(OK)를 받으면 실제 디스크에 데이터를 저장한다.

### 특징

- 데이터가 전체 노드에 **일관성**있게 저장됨
- **모든 노드가 마스터 노드**로 작동하며, 특정 노드에 장애가 나더라도 서비스에 큰 문제 없음
- 데이터 디스크 저장 전, 모든 노드에 데이터 복제 요청을 보내기 때문에 **replication에 비해 쓰기 성능이 떨어짐**
- LOCK 문제가 생기거나 슬로우 쿼리 들이 많이 발생할 때 장애를 다른 노드로 전파시킬 가능성 높음
- 하나의 클러스터에서 유지할 수 있는 노드의 수에 한계가 있어(전체 노드가 많아지면 시간 오래걸리기 때문), **횡적 스케일링의 한계** 올 수 있음

## NoSQL의 클러스터링(MongoDB)

![image](https://github.com/everyware-ie/CS/assets/102847513/56fb00ac-e50a-4904-8b55-fa343dac2611)

1. 쿼리가 참조하는 컬렉션의 Chunk metadata를 Config Server로부터 가져와 router의 메모리에 캐시한다.
2. 쿼리의 조건에서 Sharding Key 조건을 찾는다.
2-1.Sharding Key 존재할 경우 : 해당 Sharding Key가 포함된 Chunk 정보를 router의 캐시에 검색하여 Shard서버로만 사용자 쿼리를 요청
2-2. Sharding Key 없을 경우 : 모든 Shard 서버로 쿼리를 요청한다.
3. 쿼리를 전송한 대상 Shard 서버로부터 쿼리 결과가 도착하면 결과를 병합하여 사용자에게 결과를 반환한다.

### 특징

- Mongodb는 직접 특정 Shard에 접근할 수 없음
- Query Router에 명령을 하고, Query Router가 Shard에 접근하는 방식(Config Server정보기반으로 data chunk 위치를 찾아가는 것도 이때 수행됨)
    - **query router** : 쿼리를 받아 각 샤드로 보내주는 역할, **데이터 저장되어 있진않고 router 역할만 수행**
    - **shard** : 실제 데이터가 저장되는 **저장소**
    - **config** : 어떤 shard가 어떤 데이터(data chunk)를 가지고 있는지, data chunk들을 어떻게 분산해서 저장하며 관리하라 지 알 수 있음
- 성능 문제를 위해 shard 여러개를 두고 분산처리
- Query Router는 Shard정보를 찾는 부분의 성능을 위해 **Config Server의 metadata를 cache로 저장**해둔다.
    - metadata : 데이터가 저장되어 있는 shard 정보 및 sharding key 정보
    

# 레플리케이션

## RDB의 레플리케이션(MySQL)

![image](https://github.com/everyware-ie/CS/assets/102847513/64720492-eff9-4232-8367-b10b10ee6195)

1. Master node는 데이터를 저장하고, 트랜잭션에 대한 로그 BIN LOG에 저장
2. Slave node는 BIN LOG 복사(IO Thread가 수행)
3. Replay Log에 기록됨
4. SQL Thread가 읽어와 하나씩 수행하여 Data File에 저장

### 특징

- **master / slaves** 로 구성 (single point of failure 해결)
    - **master DBMS** : 웹서버로 부터 데이터 등록/수정/삭제 요청시 바이너리로그(Binarylog)를 생성하여 Slave 서버로 전달 (**DML 처리만 수행**)
    - **slave DBMS** : Master DBMS로 부터 전달받은 바이너리로그(Binarylog)를 데이터로 반영 (**read만 수행, 여러대 가능**)
- 방식이 단순하여 **신뢰도 높음**
- 데이터 복제가 동기방식이 아닌 비동기방식, master node에 적용한 데이터 변경사항이 slave에 반영될 때까지 일정시간 걸림 => **일시적 데이터 불일치성 발생 가능**

## NoSQL의 레플리케이션(MongoDB)

![image](https://github.com/everyware-ie/CS/assets/102847513/14f6fe98-d2b6-47db-a0ae-afc97f457cad)

- **Primary node / Secondary node** 로 구성
    - Primary node : 모든 쓰기 작업 수행, 기본적으로 읽기 작업도 Primary 몫
- 노드 간 **heartbeat**을 통해 상태체크
    - ***heartbeat***란 내가 살아있다는 것을 나타내거나, 다른 것이 살아있는지 점검 하는 메시지
- Primary node 사용할 수 없는 경우(장애나 네트워크 이슈) 적격한 Secondary node는 새로운 Primary 노드 선택을 위한 투표 개최 => **홀수 노드 구성이 좋다**
    - 짝수로 구성하게 되면 홀수로 구성한 경우와 다르지 않아 서버 낭비로 이어짐, 쿼럼(Quorum) 구성이 어려울 수 있음

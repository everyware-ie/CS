# Hash

### Hash를 왜 사용할까?

- ArrayList는 내부 인덱스를 사용하여 검색이 한번에 이루어지기 때문에 빠른 검색 속도 보장
    
    하지만 데이터의 추가/삭제시 많은 데이터가 밀리거나 당겨지기 때문에 많은 시간이 소요됨
    
- LinkedList는 추가/삭제시 인근 노드들의 참조값만 수정해주기 때문에 빠른 처리가 가능
    
    하지만 데이터를 검색할 경우 처음부터 순회 검색을 해야하기 때문에 데이터의 수가 많아질수록 효율이 떨어짐
    

→ 이러한 한계를 극복하기 위해서 제시된 방법이 Hash이다.

Hash는 내부적으로 배열을 사용하여 데이터를 저장하기 때문에 빠른 검색속도를 갖는다.

또한 데이터 추가/삭제시 기존 데이터를 밀어내거나 당기는 작업이 필요없도록 특별한 알고리즘을 이용하여 데이터와 연관된 고유한 숫자를 만들어 낸 뒤 이를 인덱스로 사용

→ 특정 데이터가 저장되는 인덱스를 그 데이터만의 고유한 위치로 정해서 데이터 추가/삭제시 데이터의 이동이 없도록 만들어진 구조

Hash가 뭐냐 그걸 알기 전에 알아둬야할 세 가지

### Hash Method

→ 특별한 알고리즘 사용한다했는데 이 알고리즘을 구현한 메소드를 Hash Method 라고 하며 Hash Method에 의해 반환된 데이터의 고유 숫자값을 Hash Code 라고 한다.

- 자바에서는 Object 클래스의 hashCode() 메소드를 이용해서 모든 객체의 Hash Code를 쉽게 구할 수 있음
- Hash Method를 이용해서 데이터를 Hash Table에 저장하고 검색하는 기법을 Hashing이라고 함

### Hash Table

→ 키 값의 연산에 의해 직접 접근이 가능한 데이터 구조

해시 테이블은 키와 값을 함께 저장해 둔 데이터 구조. 이는 데이터가 행과 열로 구성된 표에 저장되는 것과 유사.

하지만 테이블에 데이터를 저장할 때 위치는 무작위로 지정되어 작성되며 따라서 중간에 여유 공간이 발생할 수 있음

여기서 key 값이 Hash Method를 통해 얻어지는 값임

![Untitled](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2Ff9e49553-f95a-4ed5-9f7b-9dc32df4ba98%2FUntitled.png?table=block&id=ac732c25-5499-4265-9375-9e6d4e370416&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=1740&userId=&cache=v2)

### Hashing

→ 해시 함수에서 해시를 출력하고, 해시 테이블에 저장하는 과정까지의 행위를 말함.

![Untitled](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2Fb027df31-705a-4c8a-8e5c-06c88a7cb097%2FUntitled.png?table=block&id=23b48440-8edf-4d3e-8a8a-3439f98cdc2b&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=1540&userId=&cache=v2)

### Hash 장단점

장점

- 데이터 저장, 검색 속도가 빠름
- hash는 키에 대한 데이터가 있는지 확인이 쉬움

단점

- 일반적으로 저장공간이 많이 필요
- 여러 키에 해당하는 주소가 동일한 경우 충돌을 해결하기 위한 별도 자료구조 필요

### 주요 용도

- 검색이 많이 필요한 경우
- 저장, 삭제, 읽기가 빈번한 경우
- 캐시 구현

### 충돌

만약 다른 키가 있는데 이 키의 첫 번째 문자가 동일하다면 인덱스는 동일하게 반환될 것임. 그럼 배열에서 같은 장소에 저장되고, 이전에 저장된 정보는 사라지게 됨. 이를 충돌(Collision)이 발생했다고 한다.

충돌이 발생하는 이유

→ 함수 알고리즘의 성능이 좋지못하거나 저장되는 데이터 양이 해시 테이블의 크기보다 클 때 발생

### 충돌 해결하기

1. Chaining 기법
    - 해시 테이블 저장공간 외의 공간을 활용하는 기법
    - 충돌이 발생했을 때 연결 리스트 자료구조를 사용해서 해결하는 방법
    
    ![Untitled](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2F27b68dbb-4fb6-4d4d-be39-e24da0676da3%2FUntitled.png?table=block&id=81ab33f2-6491-45f3-8cfd-b483f534375f&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=850&userId=&cache=v2)
    
2. Linear Probing 기법
    - 해시 테이블 저장공간 안에서 충돌 문제를 해결하는 기법
    - 충돌이 발생했을 때, 해당 해시 주소(index)의 다음 주소부터 맨 처음까지 순회하며 빈 공간을 찾는 방식
    - 저장공간 활용도를 높이기 위한 기법
    

### 시간 복잡도

충돌이 없는 일반적인 경우는 O(1), 최악의 경우, 즉 모든 index에서 충돌이 발생할 경우는 O(n)
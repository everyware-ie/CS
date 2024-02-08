# 페이징

### 메모리 할당

- 운영체제가 새 프로세스를 실행시키거나 실행 중인 프로세스가 메모리를 필요로 할 때, 물리 메모리를 할당해줘야 함.
- 프로세스의 실행은 할당된 물리 메모리에서 이루어짐

→ 올리는 것은 좋은데 어디에 어떻게 올려야 할까?

### 메모리 할당 기법

연속 vs 불연속 (Process partitioning)

- 연속: 프로세스가 메모리 내에 인접되어 연속되게 하나의 블록을 차지하도록 배치
- 불연속(분산): 프로세스가 페이지나 세그먼트 단위로 나뉘어 분산 배치되는 방법

가변 vs 고정 (Memory partitioning)

- 가변: 프로세스의 크기에 맞게 메모리가 분할
- 고정: 프로세스의 크기에 상관없이 메모리가 같은 크기로 나뉨

![Untitled](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2Fc2d75ebb-4929-4cf6-b3d2-08734a09fb92%2FUntitled.png?table=block&id=5bff0ea2-2eb5-44d4-b0a9-350c1117f637&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=2000&userId=&cache=v2)

단편화는 세그먼테이션에서 했다 치고,

→ **연속 메모리 할당과 세그먼테이션에서 입출력이 반복되다보면 단편화가 발생함 (외부 단편화)**

관리 자체도 더 힘들어짐. ex) 책장 정리

그래서 등장한게

### 페이징(Paging)

→ 고정-분할 방식을 이용한 가상 메모리 관리 기법

페이지와 페이지 프레임

- 프로세스의 주소 공간을 0번지부터 동일한 크기의 페이지로 나눔
    - 코드, 데이터, 스택 등 프로세스의 구성 요소에 상관없이 고정 크기로 분할한 단위
- 물리 메모리 역시 0번지부터 페이지 크기로 나누고, 프레임이라고 부름
- 페이지의 크기는 주로 4KB. 운영체제마다 다르긴 한데 대부분 2n
- 페이지 테이블 → 각 페이지에 대해 페이지 번호와 프레임 번호를 1:1로 저장하는 테이블

![Untitled](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2F43dc9160-538e-49f7-a12f-7f493cdeb682%2FUntitled.png?table=block&id=56f274f9-a82f-49ef-a5f9-6dfc07dd856d&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=1250&userId=&cache=v2)

### 페이징 장점

- 용이한 구현
    - 메모리를 0번지부터 고정 크기로 단순히 분할하기 때문
- 높은 이식성
    - 페이징 메모리 관리를 위해 CPU에 의존하는 것 없음
- 높은 융통성
    - 시스템에 따라 응용에 따라 페이지 크기를 다르게 설정 가능
- 메모리 활용과 시간 오버헤드면에서 우수
    - 외부 단편화 없음
    - 내부 단편화는 발생하지만 매우 작음
    - 홀 선택 알고리즘을 실행할 필요없음

### 페이징 단점

- 내부 단편화의 발생
    
    → 페이지 한 칸을 할당 받았는데 그곳을 다 못채우는 것
    
- 페이지 구조에서 최대 단편화의 크기는 (단일 페이지 크기 - 1) * 페이지 개수
- 하지만 외부 단편화 해결에 드는 비용에 비하면 매우 적은 비용

### 주소 변환

페이징에서는 가장 주소를 VA=<P,O>로 표현

- VA: Virtual Address(가상 주소)
- P: Page number(페이지 번호)(PN)
- O: Offset, distance (페이지의 처음 위치에서 해당 주소까지의 거리)

물리 주소는 PA=<F,O>

- PA: Physical Address(물리 주소)
- F: Frame number(프레임 번호)(PFN)
- O: Offset, distance

PTE(Page Table Entry) = 2^(VA-O)

ex) 페이지 크기가 10B일때, 가상 주소 32번지는? → <3,2>

**페이지 주소의 물리주소 변환**
![Untitled](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2F093355c6-69c5-44e5-b01d-7da649a1940b%2FUntitled.png?table=block&id=39e8a70b-97c6-4abf-b8ea-e2aef39f2b9c&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=2000&userId=&cache=v2)
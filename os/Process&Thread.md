# 프로세스와 쓰레드

## 프로세스(Process)

- 실행파일이 메모리에 로딩되어 실행되는 상태
- 프로그램들은 메모리에 올라가야 실행될 수 있음 (실행 중인 프로그램 = 프로세스)
- CPU에 의해서 현재 실행되고 있는 프로그램
- 주기억 장치에 상주된 프로그램이 CPU에 의해서 처리되는 상태
- PCB(Process Control Block)의 존재로서 명시되는 것

### 다중 프로그래밍

- 여러 프로세스들이 메모리에 동시에 있을 수 있음
- 여러 프로그램을 동시에 실행
- 프로세스들은 상호 독립적인 메모리 공간에서 실행
    
    ![Untitled](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2F4f9023b1-ec3f-4a1c-9776-ae54eefdae44%2FUntitled.png?table=block&id=7466fb76-cd85-4cdc-b4f7-a3ce84a7565d&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=2000&userId=&cache=v2)
    

### 다중 인스턴스

- 하나의 프로그램은 여러 프로세스가 될 수 있음
- 같은 프로그램이어도, 실행될 때마다 독립된 프로세스 생성

### Loading

→ 실행파일이 메모리에 올라가는 과정

- 로더(Loader): 메모리에 Load(적재) 해주는 것

![Untitled](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2F209f5936-d74c-4f90-b8b0-b62a843f9ce7%2FUntitled.png?table=block&id=b634ca21-ef42-4f1d-8d28-f849bc06c027&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=2000&userId=&cache=v2)

- 절대 로더
    - 항상 고정된 위치에만 로딩
- 재배치 로더
    - 프로그램이 여러 개 실행되다보면 메모리 위치 상에 충돌이 있을 수 있음
    - 주기억 장치의 상태에 따라 목적 프로그램을 주기억 장치 임의공간에 적재
- 동적 적재
    - 필요한 부분만 주기억 장치에 적재하고 나머지는 보조기억장치에 저장

이런 로더들이 있다는 가볍게

## 프로세스의 생명주기

![Untitled](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2Fbb6825ac-9e5b-49b2-9176-7b7bb3479d41%2FUntitled.png?table=block&id=d14cdb62-5316-4885-9c14-eee7ab0bd274&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=2000&userId=&cache=v2)

| 생성 상태 | 프로그램을 메모리에 가져와 실행 준비가 완료된 상태 | 메모리 할당, 프로세스 제어 블록 생성 |
| --- | --- | --- |
| 준비 상태 | 실행을 기다리는 모든 프로세스가 자기 차례를 기다리는 상태. 실행될 프로세스를 CPU 스케줄러가 선택 | dispatch: 준비 → 실행 |
| 실행 상태 | 선택된 프로세스가 타임 슬라이스를 얻어 CPU를 사용하는 상태. 프로세스 사이의 문맥 교환이 일어남 | timeout: 실행 → 준비
exit: 실행 → 완료
block: 실행 → 대기 |
| 대기 상태 | 실행 상태에 있는 프로세스가 입출력을 요청하면 입출력이 완료될 때까지 기다리는 상태. 입출력이 완료되면 준비 상태로 | wakeup: 대기 → 준비 |
| 완료 상태 | 프로세스가 종료된 상태. 사용하던 모든 데이터가 정리됨. 정상 종료인 exit와 비정상 종료인 abort를 포함 | 메모리 삭제, 프로세스 제어 블록 삭제 |

## Process Control Block(PCB)

- 운영체제가 프로세스를 제어하기 위해 프로세스의 상태 정보를 저장하는 자료구조
- 프로세스마다 고유의 PCB가 생성됨(프로세스가 종료되면 폐기)

**PCB 구조**

![Untitled](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2Fb6c42067-cabe-4f41-b036-e572d3afd4e6%2FUntitled.png?table=block&id=061b056f-785a-4405-bb03-b6edaf324205&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=960&userId=&cache=v2)

이러한 정보들을 프로세스의 Context라고 함.

## Context switching(문맥 교환)

- 메모리에 프로세스가 여러 개 있다고 해도 CPU는 한번에 하나만 처리
    - 어떻게 여러 개의 프로세스를 동시에 처리할 수 있을까?

- Time-slicing(시분할)
    - 프로세스들에게 번갈아가며 CPU를 사용하게하자
        - 실제로 동시에 실행되는건 아님
        - 예를들면 크롬이 올라갔다가 메모장이 올라갔다가 이런 식
    - 어떤 순서로 번갈아가며 작업하게 할 것인가? → **스케줄링**
    - 어떻게 번갈아 가게 하지? → **Context switching**

→ **Context switching이란 한 프로세스에서 다른 프로세스로 CPU를 넘겨주는 과정**

![Untitled](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2F4cb296e3-e276-4003-a032-bb9f785abb18%2FUntitled.png?table=block&id=fb5a364f-ab0b-4d1a-92a3-2b5d29770bbf&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=960&userId=&cache=v2)

## Thread(쓰레드)

### 프로세스의 문제점

- 프로세스 생성의 오버헤드, context switching의 오버헤드가 큼.
- 프로세스간의 통신이 어려움
    - 프로세스들은 완전히 독립적인 주소 공간을 가지고 있어 서로 다른 프로세스끼리 개입 불가
    - 프로세스 간의 통신을 위해서 Shared memory, socket, message queue등 별도의 방법이 필요
- 멀티태스킹 생각하면됨

### 쓰레드

- 프로세스를 사용하는 문제점을 해결하기 위해 고안
- 프로세스보다 더 작은 실행단위, 현대 운영체제가 작업을 스케줄링 하는 단위

![Untitled](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2F79fc442e-8b1b-49a0-b9f5-38db40113ecf%2FUntitled.png?table=block&id=f073f4f1-2e9c-4f59-a8fe-9aae967a1e75&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=960&userId=&cache=v2)

### 프로세스는 쓰레드들의 컨테이너

- 쓰레드는 곧 함수, 프로세스는 반드시 1개 이상의 쓰레드로 구성
- 프로세스가 생성될 때 운영체제에 의해 자동으로 1개의 쓰레드 생성: 메인 쓰레드
- 하나의 컨테이너가 여러 개의 쓰레드를 가질 수도 있음: 멀티 쓰레드
- 그리고 각 쓰레드 별로 TCB(Thread control block)이 생성되고, 이 TCP는 PCB에 등록
- 프로세스는 쓰레드들의 공유 공간 제공
    - 모든 쓰레드는 프로세스의 코드, 데이터, 힙을 공유
    - 단 스택은 쓰레드별 별도의 공간 사용

이해하기 쉬운게 은행과 창구

새로운 은행을 만든다 vs 새로운 창구를 만든다

## 멀티 프로세스

- 멀티 프로세스는 운영체제에서 하나의 응용 프로그램에 대해 동시에 여러 개의 프로세스를 실행할 수 있게 하는 기술을 말함. 보통 하나의 프로그램 실행에 대해 하나의 프로세스가 메모리에 생성되지만, 부가적인 기능을 위해 여러개의 프로세스를 생성하는 것.
- 멀티 프로세스 내부를 보면, 하나의 부모 프로세스가 여러 개의 자식 프로세스를 생성함으로서 다중 프로세스를 구성하는 구조
- 다만, 통신이 가능할 뿐이지, 부모 프로세스와 자식 프로세스는 엄연히 서로 다른 프로세스로 독립적으로 실행되며, 독립적인 메모리 공간을 가지고 있어 서로 다른 작업을 수행. 대표적인 예로 웹 브라우저의 상단 탭이나 새 창 각 브라우저 탭은 같은 브라우저 프로그램 실행이지만, 각기 다른 사이트 실행을 행하기 때문.

### 장점

- 안전성
- 병렬성(여러 개의 CPU코어)
- 확장성
    - 멀티 프로세스는 각 프로세스가 독립적이므로, 새로운 기능이나 모듈을 추가하거나 수정할때 다른 프로세스에 영향을 주지 않음. 그래서 시스템의 규모를 쉽게 확장할 수 있음.

### 단점

- Context Switching Overhead
- 자원 공유 비효율성

## 멀티 쓰레드

- 스레드는 하나의 프로세스 내에 있는 실행 흐름. 그리고 멀티 스레드는 하나의 프로세스 안에 여러개의 스레드가 있는 것. 따라서 하나의 프로그램에서 두가지 이상의 동작을 동시에 처리하도록 하는 행위가 가능해짐.
- 웹 서버가 대표적인 멀티 스레드 응용 프로그램. 사용자가 서버 데이터베이스에 자료를 요청하는 동안 브라우저의 다른 기능을 이용할 수 있는 이유도 바로 멀티 스레드 기능 덕분. 즉, 하나의 스레드가 지연되더라도, 다른 스레드는 작업을 지속할 수 있게 됨.

### 장점

- 프로세스보다 가벼움
- 자원의 효율성
- Context Switching 비용 감소
- 응답 시간 단축

### 단점

- 안정성 문제
- 동기화로 인한 성능 저하
    - 여러 개의 스레드가 공유 자원에 동시에 접근할 수 있기 때문에 자원 변경으로 인한 의도되지 않은 버그
- 데드락 (원형 포크)
- Context switching overhead 그래도

## 쓰레드 세이프(Thread Safe)란?

- **멀티 쓰레드 프로그래밍에서, 어떤 공유 자원에 여러 쓰레드가 동시에 접근해도, 프로그램 실행에 문제가 없는 상태를 의미.**
- **Thread Safe 를 지키기 위한 네 가지 방법**
    - **Mutual exclusion (상호 배제)**
    - **Atomic operation (원자 연산)**
    - **Thread-local storage (쓰레드 지역 저장소)**
    - **Re-entrancy (재진입성)**

### **Mutual exclusion (상호 배제)**

- 공유자원에 하나의 Thread 만 접근할 수 있도록, 세마포어/뮤텍스로 락을 통제하는 방법
    - 일반적으로 많이 사용되는 방식

### **Atomic operation (원자 연산)**

- 공유자원에 원자적으로 접근하는 방법입니다.
- Atomic
    - 공유 자원 변경에 필요한 연산을 원자적으로 분리한 뒤,
    - 실제로 데이터의 변경이 이루어지는 시점에 Lock 을 걸고,
    - 데이터를 변경하는 시간 동안, 다른 쓰레드의 접근이 불가능하도록 하는 방법.

### **Thread-local storage (쓰레드 지역 저장소)**

- 공유 자원의 사용을 최대한 줄이고, 각각의 쓰레드에서만 접근 가능한 저장소들을 사용함으로써 동시 접근을 막는 방법
- 일반적으로 공유상태를 피할 수 없을 때 사용하는 방식

### **Re-entrancy (재진입성)**

- 쓰레드 호출과 상관 없이 프로그램에 문제가 없도록 작성하는 방법
# 동기화

## Race Condition(경쟁상태)

공유 자원에 대해 여러 프로세스가 동시에 접근을 시도할 때, 타이밍이나 순서 등이 결과값에 영향을 줄 수 있는 상태

→ 공유 자원에 여러 프로세스가 동시에 접근할 때 자료의 일관성을 해치는 결과가 나타날 수 있음.

### 발생하는 경우

- 커널 코드 실행 중에 인터럽트가 발생할 경우
    
    커널모드에서 데이터를 로드하여 작업을 하던 도중 인터럽트가 발생하여 같은 데이터를 조작하는 경우에 발생 가능
    
    → 커널모드에서 작업을 수행하는 동안 인터럽트를 disable시켜 인터럽트가 CPU제어권을 가져가지 못하도록하여 해결 가능
    
- 프로세스가 시스템 콜을 하여 커널모드로 진입해서 작업을 수행하는 도중에 Context Switch가 발생할 경우
    
    프로세스1이 커널모드에서 데이터를 조작하던 도중 시간이 초가되어 CPU 제어권이 프로세스2로 넘어가 같은 데이터를 조작하는 경우
    
    → 프로세스가 커널모드에서 작업을 하는 경우에는 시간이 초과되더라도 CPU 제어권이 다른 프로세스에게 넘어가지 않도록하여 해결 가능
    
- 멀티 프로세스에서 공유 메모리 내의 커널 데이터에 접근할 경우
    
    멀티프로세스 환경에서 2개의 CPU가 동시에 커널 내부의 공유 데이터에 접근하여 조작하는 경우에 발생
    
    → 커널 내부에 있는 각 공유데이터에 접근할 때마다 그 데이터에 대해 Lock/Unlock하여 해결 가능
    

## 동기화(Synchronization)

- 공유자원에 대해 다수가 동시에 접근할 때 공유데이터가 훼손되는 문제의 해결책
- 공유 데이터를 접근하고자 하는 다수의 프로세스 또는 쓰레드가 충돌 없이 공유 데이터에 접근하기 위해 상호 협력하는 것
    - 한 프로세스/스레드가 공유 데이터를 배타적 독점적으로 접근 == 동시에 접근하는 것이 아니라 차례대로, 순서대로 접근

## 임계영역이란(Critical section)

임계 영역이란 한 순간 반드시 프로세스 하나만 진입해야 하는데, 프로그램에서 임계 자원을 이용하는 부분으로 공유 자원의 독점을 보장하는 코드 영역을 의미. 임계 구역은 지정된 시간이 지난 후 종료됨.

공유되는 자원, 즉 동시 접근하려고 하는 그 자원에서 문제가 발생하지 않게 독점을 보장해줘야하는 영역을 임계 영역이라고 함.

## 임계영역이 지녀야하는 조건

1. 상호 배제(Mutual exclusion)
    
    → 하나의 프로세스가 임계 영역에 들어가 있다면 다른 프로세스는 들어갈 수 없어야한다.
    
2. 진행(Progress)
    
    → 임계영역에 들어간 프로세스가 없는 상태에서 들어가려 하는 프로세스가 여러 개라면 어느 것이 들어갈지 결정해주어야 한다.
    
3. 한정대기(Bounded waiting)
    
    → 다른 프로세스의 기아를 방지하기 위해, 한 번 임계구역에 들어간 프로세스는 다음번 임계영역에 들어갈 때 제한을 두어야한다.
    

## 동기화 3대장

- locks 방식 : 뮤텍스(mutex), 스핀락(spinlock)
    - 상호배제가 되도록 만들어진 락 활용
    - Mutex는 동기화 대상이 only 1개일 때 사용
    - 락을 소유한 스레드만이 임계구역 진입
    - 락을 소유하지 않은 스레드는 락이 풀릴 때까지 대기
    - 둘의 차이는 sleep-wait(큐존재), busy-wait
- wait-signal 방식: 세마포어(semaphore)
    - n개 자원을 사용하려는 m개 멀티스레드의 원활한 관리
        
        → 카운터를 활용
        
    - 자원을 소유하지 못한 스레드는 대기(wait)
    - 자원들 다 사용한 스레드는 알림(signal)

## Mutex(사실 Mutex 자체가 Mutual Exclusion의 줄임말)

- 잠김/열림 중 한 상태를 가지는 락 변수 이용
    - 한 스레드만 임계구역에 진입시킴, 다른 스레드는 큐에 대기
    - sleep-waiting lock 기법
- 구성 요소
    1. 락 변수
    - true/false 중 한 값
    - true: 락을 잠근다. 락을 소유한다.
    - false: 락을 연다. 락을 해제한다.
    1. 대기 큐
    - 락이 열리기를 기다리는 스레드 큐
    1. 연산
    - lock 연산(임계구역의 entry 코드)
        - 락이 잠김 상태(lock = true)이면, 현재 스레드를 Block 상태로 만들고 대기 큐에 삽입
        - 락이 열린 상태이면, 락을 잠그고 임계구역 진입
    - unlock 연산(임계구역의 exit 코드)
        - lock = false, 락을 열린 상태로 변경
        - 대기 큐에서 기다리는 스레드 하나 깨움
            
            ![Untitled](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2Fc279f3f9-e117-422f-b94c-ff418adc4b5f%2FUntitled.png?table=block&id=58d91fa0-5e8e-4a58-b66c-f7c727030f85&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=860&userId=&cache=v2)
            

## Spinlock

- Mutex와 거의 똑같음
- Mutex의 non-blocking 모델(Busy-waiting)
    - 락이 잠겨있을 때 블록되지 않고 락이 풀릴 때까지 검사 코드 실행
        
        → 큐가 아닌 while loop로 대기
        
- 단일 CPU(단일 코어)를 가진 운영체제에서 비효율적, 멀티 코어에 적함
    - 단일 코어 CPU에서 의미 없는 CPU 시간 낭비
    - 스핀락을 검사하는 스레드의 타임 슬라이스가 끝날 때까지 다른 스레드 실행 안됨, 다른 스레드의 실행 기회 뺏음.
- 락을 소유한 다른 스레드가 실행되어야 락이 풀림
- 임계구역의 실행 시간이 짧은 경우 효과적
    
    ![Untitled](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2F60931415-8097-41fe-a683-b4204a4ce7a0%2FUntitled.png?table=block&id=ecdb48e0-e3fd-47ca-a87e-b94c9d64f8bc&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=770&userId=&cache=v2)
    

## Mutex vs Spinlock

1. 락이 잠기는 시간이 긴 경우: 뮤텍스
    - 락을 얻지 못했을 때, CPU를 다른 스레드에게 양보하는 것이 효율적
    - 락이 잠기는 시간이 짧은 경우: 스핀락이 효율적
2. 단일 CPU를 가진 시스템: 큐텍스
    - 단일 CPU에서 스핀락은 크게 의미 없음
3. 멀티 코어(멀티 CPU)를 가진 시스템: 스핀락
    - 잠자고 깨는 컨텍스트 스위칭 없이 바로 자원 사용
    - 임계구역은 가능한 짧게 작성하므로
4. 사용자 응용프로그램: 뮤텍스, 커널코드: 스핀락
    - 커널코드나 인터럽트 서비스 루틴을 빨리 실행해야 하고, 인터럽트 서비스 루틴 내에서 잠잘 수 없기 때문
5. 스핀락을 사용하면 기아 발생 가능
    - 스핀락은 무한 경쟁 방식이어서 기아가 발생 가능
    - 락을 소유한 스레드가 락을 풀지 않고 계속 실행하거나 종료해버린 경우, 코딩이 잘못된 경우

## 세마포어

- n개의 공유 자원을 다수 스레드가 공유하여 사용하도록 돕는 자원 관리 기법
    - 보다 다수의 자원을 다수의 프로세스/스레드 대상으로
        - ex) n개의 프린터가 있는 경우, 프린터를 사용하고자 하는 다수 스레드의 프린터 관리
    - 세마포어는 동시에 여러 개의 프로세스/스레드가 임계 구역에 접근할 수 있도록 카운터를 가지고 있는 입구 → **일정 수가 초과하면 못들어감**
- 구성 요소
    1. 자원: n개
    2. 대기 큐: 자원을 할당받지 못한 스레드들이 대기하는 큐
    3. counter 변수
        - 사용 가능한 자원의 개수를 나타내는 정수형 전역 변수
        - n으로 초기화(counter = n)
    4. P/V 연산
        - P 연산 (wait 연산): 자원 요청 시 실행하는 연산(자원 사용 허가를 얻는 과정)
        - V 연산 (signal 연산): 자원 반환 시 실행하는 연산(자원 사용이 끝났음을 알리는 과정)

## P 연산과 V 연산

- P/V를 wait/signal로 표기하기도 함
    - P 연산: 자원 사용을 허가하는 과정, 사용가능 자원 수 1 감소(counter—)
    - V 연산: 자원 사용을 마치는 과정, 사용 가능 자원 수 1 증가(count++)
- 세마포어 종류 2가지 → busy-wait, sleep-wait

![Untitled](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2Fc71baf22-2da3-4aae-b328-1fc39792cec8%2FUntitled.png?table=block&id=1eb631aa-0dad-4e3e-9af9-018d4ae5b9dc&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=1060&userId=&cache=v2)

![Untitled](https://melodic-droplet-c1f.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F3c793912-0294-456e-ba59-f7da91aea06d%2F7260178f-2ff5-4d75-b508-deb698eaadb1%2FUntitled.png?table=block&id=8e0b2129-e775-468c-81ee-6dea52eb4d77&spaceId=3c793912-0294-456e-ba59-f7da91aea06d&width=1060&userId=&cache=v2)

## 뮤텍스와 세마포어의 차이점

- 가장 큰 차이점은 동기화 대상의 개수
    - 뮤텍스는 동기화 대상이 only 1개일 때 사용
    - Semaphore는 동기화 대상이 1개 이상일 때 사용
- 세마포어는 뮤텍스가 될 수 있지만, 뮤텍스는 세마포어가 될 수 없음
    - 뮤텍스는 0,1로 이루어진 이진 상태를 가지므로 Binary Semaphore
- 뮤텍스는 자원 소유 가능 + 책임을 지는 반면, 세마포어는 자원 소유 불가
    - 뮤텍스는 상태 0,1 뿐이므로 Lock 가질 수 있음
- 뮤텍스는 소유하고 있는 스레드만이 현재 뮤텍스를 해제할 수 있음
    - 반면, 세마포어는 세마포어를 소유하지 않는 스레드가 세마포어를 해제할 수 있음
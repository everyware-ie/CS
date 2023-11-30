## Deque
![Alt text](image-11.png)
덱(Deque)은 어떤 쪽으로 입력하고 어떤 쪽으로 출력하느냐에 따라서 스택으로 사용할 수도 있고, 큐로도 사용할 수 있는 자료구조를 의미한다.  

- 연속적인 메모리를 기반으로 하는 '시퀀스 컨테이너'이다. 따라서, 임의 접근 반복자 제공.
- 크기가 가변적이다. (선언 후에 변경할 수 있다)
- 중간 요소가 삽입, 삭제될 때, 요소들을 앞/뒤로 밀 수 있으므로 vector보다는 좋은 성능을 갖음. 그래도, 앞/뒤에서의 삽입/삭제 성능은 좋지만 중간에서는 좋지 않다.

## 분류
한쪽으로만 입력 가능하도록 설정한 덱을 scroll 이라고 하며, 한쪽으로만 출력 가능하도록 설정한 덱을 shelf라고 한다.

## 시간 복잡도
삽입/삭제- 원소를 앞/뒤에 삽입하는 경우 : O(1)
탐색- 원소를 탐색하는 경우 : O(1) (index 접근)

## 장점
- 데이터의 삽입과 삭제가 빠르다.
- 크기가 가변적이다.
- 앞, 뒤에서 데이터를 삽입/삭제할 수 있다.
- index로 임의 원소 접근이 가능하다.
- 새로운 원소 삽입 시에, 메모리를 재할당하고 복사하지 않고 새로운 단위의 메모리 블록을 할당하여 삽입한다.

## 단점
- deque의 중간에서의 삽입과 삭제가 어렵다.구현이 어렵다.

## Java에서의 Deque
자바에서 덱은 인터페이스로 구현되어있다.  
그렇기에 이를 구현해주는 클래스를 같이 쓰는데

### 추가
- addFirst(): 덱의 앞쪽에 엘리먼트를 삽입. 용량 제한이 있는 덱의 경우, 용걍을 초과하면 예외가 발생
- offerFirst(): addFirst()와 같으나 정상적으로 삽입되면 true가 용량 제한에 걸리는 경우에는 false를 리턴
- addLast(): 덱의 마지막 쪽에 엘리먼트 삽입. 용량 제한이 있는 경우 초과시 예외 발생
- add(): addLast와 동일
- offerLast(): addLast와 같고, offerFirst처럼 true false를 리턴
- offer(): offerLast()와 동일
- push(): addFirst()와 동일
- pop(): removeFirst()와 동일

### 삭제
- deque.removeFirst(): 덱의 앞에서 제거, 비어있으면 예외
- deque.remove(): removeFirst()와 동일
- deque.poll(): 덱의 앞에서 제거, 비어있으면 null 리턴
- deque.pollFirst(): poll()과 동일
- deque.removeLast(): 덱의 뒤에서 제거, 비어있으면 예외
- deque.pollLast(): 덱의 뒤에서 제거, 비어있으면 null 리턴

### 데이터를 찾아서 삭제
- removeFirstOccurrence(): 덱의 앞쪽에서부터 찾아서 첫 번째 데이터를 삭제
- removeLastOccurrence(): 덱의 뒤쪽에서부터 찾아서 첫 번째 데이터를 삭제
- remove(): first랑 같음

### 조회
- deque.getFirst(): 첫 번째 엘리먼트를 확인, 비어있으면 예외
- deque.peekFirst(): 첫 번째 엘리먼트를 확인, 비어있으면 null 리턴
- deque.peek(): peekFirst()와 동일
- deque.getLast(): 마지막 엘리먼트를 확인, 비어있으면 예외
- deque.peekLast(): 마지막 엘리먼트를 확인, 비어있으면 null 리턴
- deque.contain(Object o) Object 인자와 동일한 엘리먼트가 포함되어 있는지 확인
- deque.size(): 덱에 들어있는 엘리먼트의 개수
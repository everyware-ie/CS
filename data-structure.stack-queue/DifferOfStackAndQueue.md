## 스택

![image](https://github.com/everyware-ie/CS/assets/88030920/e3376dd2-3db2-4530-8083-0cad7e3cb02d)!
책을 쌓아올리는 형태의 자료구조

후입선출(LIFO, Last In First Out)

### 특징

- 스택의 내부 데이터는 top을 통해서만 접근할 수 있다(top은 마지막을 의미)
- 데이터를 삽입할 때는 top위에 쌓게 됨, 삽입 연산 ‘push’
- 데이터를 삭제할 때는 top에 위치한 데이터를 삭제함, 삭제 연산 ‘pop’

### 활용예시

- 웹 브라우저 방문기록 (뒤로가기)
- 실행취소 (undo)
- 역순 문자열 만들기
- 후위 표기법 계산
- 수식의 괄호 연산

## 큐

![image](https://github.com/everyware-ie/CS/assets/88030920/4f001b1f-ee8d-4fc1-8c68-9d16559f9f88)

‘줄을 서서 기다린다’라는 사전적 의미를 지니고 있다

선입선출 (FIFO, First In First Out)

### 특징

- 스택과 달리 삽입, 삭제가 다른 방향에서 이루어짐
- 삭제 연산만 수행되는 곳을 프론트(front), 삽입 연산만 수행되는 곳을 리어(rear)라고 함
    - 프론트(front)에서 이루어지는 삭제 연산을 디큐(dnQueue)
    - 리어(rear)에서 이루어지는 삽입 연산을 인큐(enQueue)

### 활용예시

- 일상 생활에서 줄을 서서 기다려야 하는 모든 행동
- 프로세스 관리
- 너비 우선 탐색(BFS, Breadth-First Search) 구현
- 캐시(Cache) 구현
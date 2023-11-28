### 원리

1. 메인 큐와 임시 큐를 준비
2. 메인 큐에 1개의 원소가 남을 때까지 dequeue하고 임시 큐에 넣음
3. 마지막 남은 1개의 원소는 result라는 변수에 저장
4. 임시큐에 남아있는 원소들을 다시 메인 큐로 이동
5. result 리턴
   
```java
import java.util.LinkedList;
   import java.util.Queue;

class QueueToStack {
private Queue<Integer> mainQueue;
private Queue<Integer> tempQueue;

    public QueueToStack() {
        mainQueue = new LinkedList<>();
        tempQueue = new LinkedList<>();
    }

    public void push(int x) {
        mainQueue.add(x);
    }

    public int pop() {
        while (mainQueue.size() > 1) {
            tempQueue.add(mainQueue.remove());
        }

        int result = mainQueue.remove();

        // Swap mainQueue and tempQueue
        Queue<Integer> temp = mainQueue;
        mainQueue = tempQueue;
        tempQueue = temp;

        return result;
    }

    public int top() {
        while (mainQueue.size() > 1) {
            tempQueue.add(mainQueue.remove());
        }

        int result = mainQueue.element();

        // Swap mainQueue and tempQueue
        Queue<Integer> temp = mainQueue;
        mainQueue = tempQueue;
        tempQueue = temp;

        return result;
    }

    public boolean isEmpty() {
        return mainQueue.isEmpty();
    }

    public static void main(String[] args) {
        QueueToStack stack = new QueueToStack();
        stack.push(1);
        stack.push(2);
        stack.push(3);

        System.out.println(stack.pop()); // 3
        System.out.println(stack.top()); // 2
        System.out.println(stack.pop()); // 2
        System.out.println(stack.isEmpty()); // false
    }
}
```
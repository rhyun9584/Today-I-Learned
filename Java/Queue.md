# Queue
```java
import java.util.Queue;
import java.util.LinkedList;

Queue<Integer> queue = new LinkedList<>();
```
java에서는 `Queue` 자료형은 인터페이스다. 그 구현체로는 `LinkedList`를 활용한다. 

### 주요 메소드
- `queue.add(e)` or `queue.offer(e)`: enqueue
- `queue.remove()` or `queue.poll()`: dequeue
- `queue.element()` or `queue.peek()`: 큐의 첫 요소 확인(삭제 X)
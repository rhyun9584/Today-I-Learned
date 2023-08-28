# Priority Queue
```java
import java.util.PriorityQueue;

// 최소힙
PriorityQueue<Integer> queue = new PriorityQueue<>();
// 최대힙
PriorityQueue<Integer> queue = new PriorityQueue<>(Comparator.reverseOrder());
```
가장 기본적인 사용 방법

## Priority Queue with `Comparator`
```java
PriorityQueue<int[]> queue = new PriorityQueue<>(new Comparator() {
    @Override
    public int compare(int[] o1, int[] o2) {
        if (o1[0] == o2[0]) { return o1[1] - o2[1] };
        return o1[0] - o2[0];
    }
});
```
Priority Queue에 넣을 원소 타입이 `Comparable` 인터페이스를 상속하고 있지 않다면, 해당 자료구조에 **어떻게 각 원소의 우선순위를 비교할 것인지** 그 방법을 `Comparator` 객체를 생성하고 `compare()`라는 리턴 자료형 `int`의 메소드를 정의하여 알려주어야 한다.<br>

[`Comparable` 인터페이스 정보](https://docs.oracle.com/javase/8/docs/api/java/lang/Comparable.html)<br>
-> 이 Document에서 `Comparable` 인터페이스를 상속하고 있는 자료구조를 확인할 수 있다.

`compare()` 메소드의 경우 매개변수로 두 개의 객체를 받는데, 결과 값이 음수라면 첫 번째 매개변수가 더 선순위이며 결과 값이 양수라면 두 번째 매개변수가 더 선순위이다.
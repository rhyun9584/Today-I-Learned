# Appendix B. 자바 8 람다와 인터페이스 스펙 변화

## B.1 람다가 도입된 이유
규모가 커져가는 데이터를 처리하기 위한 방법이 필요했다. 이 때 멀티코어 프로세서들이 등장하면서 병렬화 프로그래밍에 대한 필요성이 생기기 시작했다.

이에 대응하기 위해 자바 8에서는 병렬화를 위해 컬렉션(배열, List, Set, Map)을 강화했고, 이러한 컬렉션을 더 효율적으로 사용하기 위해 스트림(Stream)을 강화했다.

스트림을 효율적으로 사용하기 위해 함수형 프로그래밍이, 다시 함수형 프로그래밍을 위해 람다가, 또 람다를 위해 인터페이스의 변화가 수반됐다.

## B.2 람다란 무엇인가?
람다란 한 마디로 코드 블록이다.
```java
// 람다 적용 전 코드
public class B001 {
    public static void main(String[] args) {
        Runnable r = new Runnable() {
            public void run() {
                System.out.println("Hello Lambda!");
            }
        };

        r.run();
    }
}
```
```java
// 람다 적용 후 코드
public class B002 {
    public static void main(String[] args) {
        Runnable r = () -> {
            System.out.println("Hello Lambda!");
        };

        r.run();
    }
}
```
`Runnable` 타입으로 참조 변수 `r`을 만들고 있으니, `new Runnable()`은 컴파일러가 알아낼 수 있어서 생략 가능하다.<br>
`public void run()` 메소드가 단순히 `()`로 변경될 수 있는 이유는, `Runnable` 인터페이스가 가진 추상 메소드가 `run()` 하나뿐이기 때문이다.

## B.3 함수형 인터페이스
추상 메소드를 하나만 갖는 인터페이스를 자바 8부터는 **함수형 인터페이스**라고 한다. 이런 함수형 인터페이스만을 람다식으로 변경할 수 있다.
```java
public class B005 {
    public static void main(String[] args) {
        MyFunctionalInterface mfi = (int a) -> {return a*a; };

        int b = mfi.runSomething(5);
    }
}

@FunctionalInterface
interface MyFunctionalInterface {
    public abstract int runSomething(int count);
}
```
`@FunctionalInterface` 어노테이션을 붙이면, 컴파일 시 컴파일러가 해당 인터페이스가 함수형 인터페이스의 조건에 맞는지 검사한다. 즉, **단 하나의 추상 메소드만을 갖고 있는지 확인한다.**

## B.4 메소드 호출 인자로 람다 사용
람다식을 변수에 저장하는 것이 가능하다면 당연히 메소드의 인자로도 사용할 수 있다.
```java
public class B008 {
    public static void main(String[] args) {
        doIt(a -> a*a);
    }

    public static void doIt(MyFunctionalInterface mfi) {
        int b = mfi.runSomething(5);
    }
}
```

## B.5 메소드 반환값으로 람다 사용
```java
public class B009 {
    public static void main(String[] args) {
        MyFunctionalInterface mfi = todo();

        int result = mfi.runSomething(3);
    }

    public static MyFunctionalInterface todo() {
        return num -> num * num;
    }
}
```
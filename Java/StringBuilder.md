# `StringBuilder`
java의 `String`은 불변성을 갖는다. <br>
불변성을 갖는다는 것은 `+`와 같은 연산자로 `String` 객체에 값을 변경하게 되면, 해당 객체의 값을 실제로 변경하는 것이 아니라 새로운 객체를 생성한다는 의미이다.

`String`의 불변성으로 인해 얻는 좋은 점이 많지만, 문자열에 변형을 가하는 연산이 많을수록 메모리 소모량이 커지는 단점이 발생한다.

이를 해결하기 위해 사용하는 것이 `StringBuilder`이다.<br>
`String`과 다르게 가변성을 가져 `append()`나 `delete()`같은 메소드를 활용해 문자열을 변형하는 연산의 수행에 있어 더욱 효율적이다.

### import
```java
import java.util.StringBuilder;
```
### 기본 사용법
```java
StringBuilder sb = new StringBuilder();
sb.append("a").append("b");
```
`append()` 메소드의 경우 리턴 값이 `StringBuilder`이므로 위와 같이 메소드 체인의 형태로 사용이 가능하다.

### 주요 메소드
- `StringBuilder append(String s)`: `StringBuilder` 뒤에 값을 붙임
- `StringBuilder delete(int start, int end)`: 특정 인덱스의 범위 값을 삭제
- `StringBuilder insert(int offset, any primitive of char[])`: 문자 삽입
- `StringBuilder replace(int start, int end, String s)`: 특정 범위의 문자열을 치환
- `StringBuilder reverse()`: 순서를 뒤집음
- `StringBuilder setCharAt(int index, char ch)`: 특정 위치의 문자를 치환
- `int indexOf(String s)`: 값이 어느 인덱스에 위치하는지 확인
- `int length()`: 길이 반환

### 기타
`StringBuilder`와 유사하게 `StringBuffer`가 존재한다.<br>
가장 큰 차이점은 **동기화 유무**로 `StringBuffer`의 경우 동기화를 지원하여 멀티 쓰레드 환경에서 안전하게 사용할 수 있다.<br>
그 대신 `StringBuilder`는 싱글 쓰레드거나 동기화를 고려하지 않아도 되는 경우 사용하면 `StringBuffer`보다 좋은 성능을 보인다.
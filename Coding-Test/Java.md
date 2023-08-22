# JAVA 코딩테스트 준비
- [입력값 받기](#입력값-받기)
- [StringBuilder](#stringbuilder)
- [ArrayList to Array](#arraylist-to-array)
- [String to char array](#string-to-char)
- [2차원 배열 선언](#2차원-배열-선언)

## 입력값 받기
`BufferedReader`를 활용한다.<br>
자바에서 `Scanner`보다 빠른 성능으로 입력을 받기 위해 사용한다.

### import
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.StringTokenizer;
```

### 기본 사용법
```java
BufferedReader bf = new BufferedReader(new InputStreamReader(System.in));
```
`InputStreamReader` 객체를 만들어 인자로 넣어 초기화한다.

```java
String s = bf.readLine();
int i = Integer.parseInt(bf.readLine());
```

`readLine()` 메소드를 사용하여 입력을 읽어들이는데, 기본 반환 값의 자료형이 `String`이기 때문에 다른 타입으로 입력을 받고자 한다면 형변환이 필요하다.

```java
String s = bf.readLine();
StringTokenizer st = new StringTokenizer(s);

int a = Integer.parseInt(st.nextToken());
int b = Integer.parseInt(st.nextToken());
```
`1 2 3 4`와 같이 공백으로 구분하여 입력 값이 주어지는 경우, 위와 같이 `StringTokenizer`를 활용하여 쪼갤 수 있다.

## `StringBuilder`
java의 `String`은 불변성을 갖는다. <br>
불변성을 갖는다는 것은 `+`와 같은 연산자로 `String` 객체에 값을 변경하게 되면 이미 있는 객체의 값을 변경하는 것이 아니라 새로운 객체를 생성한다는 의미이다.

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
- `StringBuilder setCharAt(int indxe, char ch)`: 특정 위치의 문자를 치환
- `int indexOf(String s)`: 값이 어느 인덱스에 위치하는지 확인
- `int length()`: 길이 반환

## ArrayList to Array
`List<T>` 객체를 `int[]`나 `String[]` 형 array로 변환하는 방법

### `List<Integer>` to `int[]`
```java
List<Integer> intList = new ArrayList<>();

int[] arr = intList.stream().mapToInt(i -> i).toArray();
```

### `List<String>` to `String[]`
```java
List<String> strList = new ArrayList<>();

String[] arr = strList.toArray(new String[0]);
```

## `String` to `char[]`
`String` 문자열 객체를 한 글자씩 쪼갠 `char`의 array 형태로 바꾸어 for문을 작성
```java
String str = "abcde";
for (char ch : str.toCharArray()){
    ...
}
```

## 2차원 배열 선언
### 정수의 2차원 배열 선언
```java
// 2차원 배열 틀 선언
List<Integer>[] graph = new ArrayList[n+1];

// 각 행 초기화
for (int i = 1; i < n+1; i++){
    graph[i] = new ArrayList<>();
}
```
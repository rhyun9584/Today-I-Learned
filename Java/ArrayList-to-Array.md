# ArrayList to Array
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
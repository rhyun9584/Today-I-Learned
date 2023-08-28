# `String` to `char[]`
`String` 문자열 객체를 한 글자씩 쪼갠 `char`의 array 형태로 바꾸어 for문을 작성
```java
String str = "abcde";
for (char ch : str.toCharArray()){
    ...
}
```
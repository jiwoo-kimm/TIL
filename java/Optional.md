# Optional
- 지네릭 클래스로, T타입의 객체를 감싸는 래퍼 클래스
- `null` 체크를 위한 if문 대신 자체 메소드 사용
- 더 간결하고 안전한 코드

## 생성

1. `of()`: 매개변수가 `null`이면 `NullPointerException` 발생
```java
Optional<String> opt = Optional.of("abc");
```
2. `ofNullable()`: 매개변수가 `null`일 가능성이 있는 경우 사용
```java
Optional<String> opt = Optional.ofNullable(null);
```
3. `empty()`: 초기화는 `null` 대입보다 메소드 사용
```java
Optional<String> opt = Optional.<String>empty();
```


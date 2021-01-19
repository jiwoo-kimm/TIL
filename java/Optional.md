# Optional
- 지네릭 클래스로, T타입의 객체를 감싸는 래퍼 클래스
- `null` 체크를 위한 if문 대신 자체 메소드 사용
- 더 간결하고 안전한 코드

## 생성

#### `of()`
매개변수가 `null`이면 `NullPointerException` 발생
```java
Optional<String> opt = Optional.of("abc");
```

#### `ofNullable()`
매개변수가 `null`일 가능성이 있는 경우 사용
```java
Optional<String> opt = Optional.ofNullable(null);
```
#### `empty()`
초기화는 `null` 대입보다 메소드 사용
```java
Optional<String> opt = Optional.<String>empty();
```

## 값 불러오기

#### `get()`
값이 `null`이면 `NoSuchElementException` 발생
```java
String str = opt.get();
```
#### `orElse(T value)`
값이 `null`일 때 대체값으로 value 리턴
```java
String str = opt.orElse("someValue");
```
#### `orElseGet(Supplier other)`
값이 `null`일 때 대체값을 리턴하는 람다식 지정
```java
String str = opt.orElseGet(String::new);
```
#### `orElseThrow(Supplier exceptionSupplier)`
값이 `null`일 때 지정된 예외 발생
```java
String str = opt.orElseThrow(NullPointerException::new);
```

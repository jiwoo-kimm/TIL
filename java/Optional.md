# Optional
- 지네릭 클래스로, T타입의 객체를 감싸는 래퍼 클래스
- `null` 체크를 위한 if문 대신 자체 메소드 사용
- 더 간결하고 안전한 코드

<br>

## 생성

#### 1. `of()`
- 매개변수가 `null`이면 `NullPointerException` 발생
```java
Optional<String> opt = Optional.of("abc");
```

#### 2. `ofNullable()`
- 매개변수가 `null`일 가능성이 있는 경우 사용
```java
Optional<String> opt = Optional.ofNullable(null);
```
#### 3. `empty()`
- 초기화는 `null` 대입보다 메소드 사용
- `null`과 `empty()`는 동일하게 취급
```java
Optional<String> opt = Optional.<String>empty();
Optional<String> opt2 = null;
opt.equals(opt2);   // true
```

<br>

## 값 불러오기

#### 1. `get()`
- 값이 `null`이면 `NoSuchElementException` 발생
```java
String str = opt.get();
```
#### 2. `orElse(T value)`
- 값이 `null`일 때 대체값으로 value 리턴
```java
String str = opt.orElse("someValue");
```
#### 3. `orElseGet(Supplier other)`
- 값이 `null`일 때 대체값을 리턴하는 람다식 지정
```java
String str = opt.orElseGet(String::new);
```
#### 4. `orElseThrow(Supplier exceptionSupplier)`
- 값이 `null`일 때 지정된 예외 발생
```java
String str = opt.orElseThrow(NullPointerException::new);
```
#### 5. `isPresent()`
- 값이 있으면 true 없으면 false 리턴
```java
if (Optional.ofNullable(str).isPresent())
  System.out.println(str);
```
#### 6. `ifPresent(Consumer<T> block)`
- 값이 있으면 block 람다식을 수행하고 없으면 아무 일도 하지 않음
```java
Optional.ofNullable(str).ifPresent(System.out::println)
```

<br>

## 기본형 Optional
- `OptionalInt`, `OptionalLong`, `OptionalDouble`

### 값 불러오기
```java
OptionalInt opt = Optional.of(0);
int val = opt.getAsInt();
```

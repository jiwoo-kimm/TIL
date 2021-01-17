# Stream
- 데이터 소스를 추상화하고, 데이터를 다루는 주요 메소드들을 정의해놓은 API
- 코드가 간결해지며 재사용성이 높아짐

## 특징
- 일회용이다.
- 데이터 소스를 변경하지 않는다.
  - 필요하다면 작업 결과를 배열이나 컬렉션으로 반환할 수 있다.
  ```java
  List<String> sorted = stream.sorted().collect(Collectors.toList());
  ```
- 작업을 내부 반복으로 처리한다.
  - 반복문을 메소드의 내부에 숨길 수 있다.
  ```java
  stream.forEach(System.out::println);
  ```
  
## [연산](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/stream/Stream.html)

```
중간연산: 연산 결과가 stream → 연속해서 연산 가능
최종연산: 연산 결과가 stream이 아님 → stream의 요소를 소모하므로 한 번만 가능
```
- 중간 연산은 최종 연산 호출 시까지 지연되었다가 한 시점에 차례로 소모
- `parallel()`: 병렬 연산 수행
- `sequential()`: 순차 연산 수행 (기본값)

## 타입
- `Stream<T>`가 기본 타입
- 오토박싱&언박싱으로 인한 비효율을 줄이기 위해 `IntStream`, `LongStream`, `DoubleStream` 제공

## 생성

### Collection
```java
Stream<T> Collection.stream()
```
- Collection 클래스에 메소드 정의
- Collection의 모든 자손은 해당 컬렉션을 소스로 하는 stream 생성 가능
```java
List<Integer> list = Arrays.asList(1,2,3,4,5);
Stream<Integer> stream = list.stream();
```

### Array
```java
Stream<T> Stream.of(T... values)
Stream<T> Array.stream(T[])
```
- Stream과 Arrays 클래스에 static 메소드 정의
```java
Stream<String> stream = Stream.of("a", "b", "C");
Stream<String> stream = Stream.of(new String[]{"a", "b", "c");
Stream<String> stream = Arrays.stream(new String[]{"a", "b", "c"});
```

### 특정 범위의 정수
```java
IntStream.range(int begin, int end);        // [begin, end)
IntStream.rangeClosed(int begin, int end);  // [begin, end]
```
- int, long 타입 생성 가능

### 난수
```java
IntStream ints(long streamSize);  // 크기만 지정
IntStream ints(int begin, int end);   // 범위만 지정
IntStream ints(long streamSize, int begin, int end);    // 크기와 범위 지정
```
- Random 클래스에 메소드 정의
- int, long, double 타입 생성 가능
- `streamSize`를 생략하면 무한스트림이 생성되어 `limit()`으로 갯수 지정

## Lambda


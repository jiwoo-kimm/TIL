# Stream
- 데이터 소스를 추상화하고, 데이터를 다루는 주요 메소드들을 정의해놓은 API
- 코드가 간결해지며 재사용성이 높아짐

## 특징
- 일회용이다.
- 데이터 소스를 변경하지 않는다.
  - 필요하다면 작업 결과를 배열이나 컬렉션으로 반환할 수 있다.
- 작업을 내부 반복으로 처리한다.
  - 반복문을 메소드의 내부에 숨길 수 있다.

## 타입
- `Stream<T>`가 기본 타입
- 오토박싱&언박싱으로 인한 비효율을 줄이기 위해 `IntStream`, `LongStream`, `DoubleStream` 제공

<br>

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

### 빈 스트림
```java
Stream emptyStream = Stream.empty();
```

<br>

## [연산](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/stream/Stream.html)

```
중간연산: 연산 결과가 stream → 연속해서 연산 가능
최종연산: 연산 결과가 stream이 아님 → stream의 요소를 소모하므로 한 번만 가능
```
```
parallel(): 병렬 연산 수행
sequential(): 순차 연산 수행 (기본값)
```

### 중간연산
- 최종 연산 호출 시까지 지연되었다가 한 시점에 차례로 소모

#### 자르기

- `skip(long n)`: 처음부터 n개의 요소 스킵
- `limit(long size)`: size만큼의 요소를 가진 stream 반환

#### 걸러내기

- `filter(Predicate<? super T> predicate)`: predicate(조건)에 맞지 않는 요소 제거
- `distinct()`: 중복된 요소 제거

#### 정렬

- `sorted()`: 기본 정렬 기준에 따라 요소 정렬
- `sorted(Comparator<? super T> comparator)`: comparator 또는 람다식에 따라 요소 정렬

+) `Comparator` interface의 정렬 메소드 [참고](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/Comparator.html)

#### 변환

```java
Stream<R> map(Function<? super T, ? extends R> mapper)
```
- 원하는 특정 형태로 요소를 변환
- T 타입을 R 타입으로 변환해서 반환하는 Function을 매개변수로 지정

```java
DoubleStream mapToDouble(ToDoubleFunction<? super T> mapper)
IntStream mapToInt(ToIntFunction<? super T> mapper)
LongStream mapToLong(ToLongFunction<? super T> mapper)
```
- `Stream<T>` 타입이 아닌 기본형 stream으로 변환
  - `Stream<String>` → `IntStream`: `mapToInt(Integer::parseInt)`
  - `Stream<Integer>` → `IntStream`: `mapToInt(Integer::intValue)`

```java
Stream<U> mapToObj(IntFunction<? extends U> mapper)
Stream<Integer> boxed()
```
- 기본형 stream을 `Stream<T>`타입으로 변환

```java
Stream<R> flatMap(Function<? super T,? extends Stream<? extends R>> mapper)
```
- `Stream<T[]>`를 `Stream<T>`로 변환

#### 조회

```java
Stream<T> peek(Consumer<? super T> action)
```
- stream의 소모 없이 action을 통해 연산 결과 확인 가능

### 최종연산

#### 기본형 Stream 추가 메소드
```java
int sum()
OptionalDouble average()
OptionalInt max()
OptionalInt min()
IntSummaryStatistics summaryStatistics()  // 스트림 소모 한 번으로 위의 값들을 얻을 수 있음
```

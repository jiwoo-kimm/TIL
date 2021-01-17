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
중간연산: 연산 결과가 스트림 → 연속해서 연산 가능
최종연산: 연산 결과가 스트림이 아님 → 스트림의 요소를 소모하므로 한 번만 가능
```
- 중간 연산은 최종 연산 호출 시까지 지연되었다가 한 시점에 차례로 소모
- `parallel()`: 병렬 연산 수행
- `sequential()`: 순차 연산 수행 (기본값)

## 타입
- `Stream<T>`가 기본 타입
- 오토박싱&언박싱으로 인한 비효율을 줄이기 위해 `IntStream`, `LongStream`, `DoubleStream` 제공



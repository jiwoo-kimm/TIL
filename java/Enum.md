# Enum

- 향상된 열거형
```java
enum Direction {  EAST, WEST  }
```
       내부적   ↓   구현 방식
```java
enum Direction {
  static final Direction EAST = new Direction("EAST");
  static final Direction WEST = new Direction("WEST");
  
  private String name;
  
  private Direction(String name)  { this.name = name; }
}
```
- enum 상수 간 비교
  - 가능: `==`, `equals()`, `compareTo()`
  - 불가능: `>`, `<`
  - 실제 값이 같아도 타입이 다르면 다른 값으로 인식

## Enum class

- `java.lang.Enum`

### Method

|메소드|설명|
|--|--|
|`Class<E> getDeclaringClass()`|enum의 class 객체 리턴|
|`String name()`|enum 상수의 이름을 문자열로 리턴|
|`int ordinal()`|enum 상수가 정의된 순서 리턴|
|`T valueOf(Class<T> enumType, String name)`|enumType에서 name과 일치하는 enum 상수 반환|

### Additional Field

- 불연속적인 enum 상수 값 지정
- 여러 값 지정 가능
- 값에 해당하는 필드와 생성자 필요
- enum의 생성자는 묵시적으로 private
```java
enum Direction {
  EAST(1, ">"), SOUTH(5, "V"), WEST(-1, "<"), NORTH(10, "^");
  
  private final int value;
  private final String symbol;
  
  Direction(int value, String symbol) {
    this.value = value;
    this.symbol = symbol;
  }
  
  public int getValue() { return value; }
  public String getSymbol() { return symbol; }
}
```

### Abstract Method

- 각 enum 상수에 따라 달라지는 메소드 구현을 위해 추상 메소드 선언
- 각 enum 상수가 공통된 필드에 접근할 수 있도록 접근 제어자 설정
```java
enum Transportation {
  BUS(100) {  int fare(int distance) {  return distance * BASIC_FARE; }},
  TRAIN(150) {  int fare(int distance) {  return distance * BASIC_FARE; }},
  AIRPLANE(300) {  int fare(int distance) {  return distance * BASIC_FARE; }};
  
  abstract int fare(int distance);
  
  protected final int BASIC_FARE;
  
  Transportation(int basicFare) { BASIC_FARE = basicFARE; }
  
  public int getBasicFare() { return BASIC_FARE; }
}
```


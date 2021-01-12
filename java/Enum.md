# Enum

- 향상된 열거형
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

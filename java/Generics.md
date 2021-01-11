# Generics

- 객체의 타입을 컴파일 시에 체크해주는 기능
- 타입 안정성 증가
- 형변환의 번거로움 감소

<br>

## 용어

```java
class Box<T> {}
```
- `Box<T>`: Generic class
- `T`: Type parameter
- `Box`: Raw type

```java
Box<String> b = new Box<String>();
```
- `String`: Parameterized type

<br>

## 제한

### Static field & method

```java
class Box<T> {
  static T item;  // ERROR
  static int compare(T t1, T t2) { ... }  // ERROR
}
```
- 대입된 타입의 종류에 관계 없이 동일한 것이어야 하기 때문
- 단, 메소드 선언부에 type parameter가 명시된 `Generic method`는 허용

### Generic type array

```java
class Box<T> {
  T[] itemArr;  // OK
  T[] toARray() {
    T[] tmpArr = new T[itemArr.length]; // ERROR
    ...
  }
}
```
- Generic type array 참조변수 선언은 가능
- `new` 연산자를 사용한 Generic type array 생성은 불가능
- 컴파일 시점에 T가 어떤 타입인지 모르기 때문

### instanceOf

- `new` 연산자와 같은 이유로 `T`를 `instanceOf`의 피연산자로 사용 불가능

<br>

## Type parameter

- Type parameter에 `extends`를 사용해서 허용타입 명시
```java
class FruitBox<T extends Fruit> {
  ArrayList<T> list = new ArrayList<>();
}
```
- interface도 구현한 클래스를 허용해야 할 경우
```java
class FruitBox<T extends Fruit & Eatable> { ... }
```

<br>

## 와일드카드

- Generic type parameter가 다른 것만으로는 메소드 오버로딩 성립 X
- 컴파일러가 컴파일할 때 Generic type을 사용하고 제거해버리기 때문

||기능|
|---|---|
|`<? extends T>`|와일드 카드의 상한 제한. T와 그 자손들만 가능|
|`<? super T>`|와일드 카드의 하한 제한. T와 그 조상들만 가능|
|`<?>`|`<? extends Object>`와 같은 의미|

<br>

## Generic Method

- 메소드의 선언부에 generic type이 선언된 메소드
- 이때 generic type T는 메소드의 지역 변수처럼, 메소드 내에서만 지역적으로 사용
```java
static <T> void sort(List<T> list, Comparator<? super T> c) { ... }
```

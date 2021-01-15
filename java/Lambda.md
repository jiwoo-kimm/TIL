# Lambda

## Lambda Expression
- 메소드를 하나의 식으로 표현한 것
- Anonymous function
- 메소드를 변수처럼 다룰 수 있음
- 익명 객체

```
리턴타입 메소드이름 (매개변수) { 문장들 }

          ↓

(매개변수) -> { 문장들 }
```
<br>

## Functional Interface
- 인터페이스를 구현한 익명 객체는 람다식으로 대체 가능
- `@FunctionalInterface`
  - 인터페이스에 하나의 추상 메소드가 올바르게 정의되었는지 확인
  - 람다식과 인터페이스의 메소드를 연결
- 람다식(익명 객체)은 오직 함수형 인터페이스로만 형변환 가능
- 람다식 내에서 참조하는 객체는 final이 붙지 않아도 상수로 간주


### java.util.function
||메소드|매개변수|리턴값|설명|
|--|--|--|--|--|
|java.lang.Runnable|void run()|X|X||
|Supplier<T>|T get()|X|O||
|Consumer<T>|void accept(T)|O|X||
|Function<T,R>|R apply(T)|O|O||
|Predicate<T>|boolean test(T)|O|O|조건식 표현에 사용|
|UnaryOperator<T>|T apply(T)|O|O|Function과 달리 매개변수와 결과 타입 일치|
  
### 매개변수가 두 개인 함수형 인터페이스
||메소드|매개변수|리턴값|설명|
|--|--|--|--|--|
|BiConsumer<T,U>|void accept(T, U)|O|X||
|BiPredicate<T,U>|boolean test(T, U)|O|O|조건식 표현에 사용|
|BiFunction<T,U,R>|R apply(T, U)|O|O||
|BinaryOperator<T>|T apply(T, T)|O|O|BiFunction과 달리 매개변수와 결과 타입 일치|

### Collection framework
|인터페이스|메소드|설명|
|--|--|--|
|Collection|boolean removeIf(Predicate<E> filter)|조건에 맞는 요소 삭제|
|List|void replaceAll(UnaryOperator<E> operator)|모든 요소를 변환하여 대체|
|Iterable|void forEach(Consumer<T> action)|모든 요소에 action 수행|
|Map|V compute(K key, BiFunction<K,V,V> f)|지정된 키의 값에 f 수행|
||V computeIfAbsent(K key, Function<K,V> f)|키가 없으면 f 수행 후 추가|
||V computeIfPresent(K, key, BiFunction<K,V,V> f)|지정된 키가 있을 때 f 수행|
||V merge(K key, V, value, BiFunction<V,V,V> f)|모든 요소에 병합 f 수행|
||void forEach(BiConsumer<K,V> action)|모든 요소에 action 수행|
||void replaceAll(BiFunction<K,V,V> f)|모든 요소에 치환 f 수행|

###  기본형 함수형 인터페이스
||메소드|매개변수|리턴값|설명|
|--|--|--|--|--|
|DoubleToIntFunction|int applyAsInt(double d)|O|O|AToBFunction -> A입력 B출력|
|ToIntFunction<T>|int applyAsInt(T value)|O|O|ToBFunction -> 지네릭입력 B출력|
|IntFunction<R>|R apply(T, U)|O|O|AFunction -> A입력 지네릭출력|
|ObjIntConsumer<T>|void accept(T, U)|O|X|ObjAConsumer -> T,A 입력|

<br>

## Function의 합성
|메소드|설명|
|--|--|
|default <V> Function<T,V> andThen(Function<R,V> after)|f -> g|
|default <V> Function<V,R> compose(Function<R,V> before)|g -> f|
|static <T> Function<T,T> identity()|항등 함수 (f(x)=x)|
          
<br>

## Predicate의 결합
|메소드|설명|
|--|--|
|and()|&&|
|or()|\|\||
|negate()|부정|
|isEqual()|boolean result = Predicate.isEqual(str1).test(str2);|

<br>

## 메소드 참조
|종류|람다|메소드 참조|
|--|--|--|
|static 메소드 참조|(x) -> ClassName.method(x)|ClassName::method|
|인스턴스 메소드 참조|(obj, x) -> obj.method(x)|ClassName::method|
|특정 객체 인스턴스 메소드 참조|(x) -> obj.method(x)|obj::method|

```java
BiFunction<Integer, String, MyClass> bf = (i, s) -> new MyClass(i, s);
BiFunction<Integer, String, MyClass> bf2 = MyClass::new;

Function<Integer, int[]> f = x -> new int[x];
Function<Integer, int[]> f2 = int[]::new;
```

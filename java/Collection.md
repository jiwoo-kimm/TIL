# JAVA Collection
- A collection is an object that represents a **group of objects**
- A collections framework is a **unified architecture for representing and manipulating collections**, enabling collections to be manipulated independently of implementation details

<details closed>
<summary>List</summary>
  
## List

### ArrayList

- array based list
- bad for add, remove operations
- best for sequential add, remove operations
- high accessability to a random element

### LinkedList

- link based list
- good for add, remove operations
- bad accessability to a random element

</details>
<details closed>
<summary>Stack</summary>
  
## Stack

- extends `Vector` class
- implements `Serializable`, `Cloneable`, `Iterable<E>`, `Collection<E>`, `List<E>`, `RandomAccess` interface

### Methods

|Method|Description|Returns|Throws|
|--|--|--|--|
|`empty()`|Tests if this stack is empty|true or false||
|`push(E)`|Pushes an item onto the top of this stack|the item argument||
|`pop()`|Removes the object at the top of this stack|the object at the top of this stack|`EmptyStackException` on empty stack|
|`peek()`|Looks at the object at the top of this stack without removing it from the stack|the object at the top of this stack|`EmptyStackException` on empty stack|
|`search(O)`|Finds the 1-based position where an object is on this stack|- the distance from the top of the stack of the occurrence nearest the top of the stack<br>- the topmost item on the stack is considered to be at distance 1<br>- the return value -1 indicates that the object is not on the stack||

1. `add()` vs `push()`

||`add()`|`push()`|
|--|--|--|
|구현 클래스|`java.util.Vector`|`java.util.Stack`|
|반환값|boolean|element|

2. `remove()` vs `pop()`

||`remove()`|`pop()`|
|--|--|--|
|구현 클래스|`java.util.Vector`|`java.util.Stack`|
|파라미터|index|element|
|반환값|element|element|
|예외|`ArrayIndexOutOfBoundsException`|`EmptyStackException`|

#### `Stack` 클래스에 직접 구현된 `push()`, `pop()`를 사용함으로써 `Stack`임을 명확히 하는 것이 바람직하다.

</details>
<details closed>
<summary>Set</summary>
  
## Set

- A collection that contains no duplicate elements
- permits the null element

### HashSet

- implements `Set` interface, backed by a hash table
- no guarantees as to the iteration order of the set
- O(1)

### LinkedHashSet

- Hash table & Linked list implementation of Set interface, with predictable iteration order
- extends `HashSet` class
- maintains a doubly-linked list running through all of its entries
- linked list ordering defined by `insertion-order`
- O(1)

### TreeSet

- `NavigableSet` implementation based on a `TreeMap`, a Red-Black tree
- extends `AbstractSet` class, offering additional [methods](https://docs.oracle.com/javase/7/docs/api/java/util/TreeSet.html)
- ordered using their natural ordering, or by a Comparator
- O(log n) for the basic operations

</details>
<details closed>
<summary>Map</summary>

## Map

### HashMap

- Hash table based implementation of the Map interface
- O(1) for search operations

### TreeMap

- A Red-Black tree based NavigableMap implementation
- sorted according to the natural ordering of its keys, or by a Comparator
- O(log n) time cost for the containsKey, get, put and remove operations
- best for range search, sorting operations

</details>
<details closed>
<summary>ListIterator</summary>

## ListIterator
- Iterator + 양방향 조회기능추가
- List interface 구현한 collections에서 사용 가능

### Method

|Method|Description|Returns|Throws|
|--|--|--|--|
|`hasNext()`|Returns true if this list iterator has more elements when traversing the list in the forward direction|||
|`hasPrevious()`|Returns true if this list iterator has more elements when traversing the list in the reverse direction.|||
|`next()`|Returns the next element in the list and advances the cursor position|the next element on the list|`NoSuchElementException` if the iteration has no next element|
|`previous()`|Returns the previous element in the list and moves the cursor position backwards|the previous element on the list|`NoSuchElementException` if the iteration has no previous element|
|`remove()`|Removes from the list the last element that was returned by next() or previous()||- `UnsupportedOperationException` if the remove operation is not supported by this list iterator<br>- `IllegalStateException` if neither next nor previous have been called, or remove or add have been called after the last call to next or previous|
  
</details>
<details closed>
<summary>Comparable & Comparator</summary>
  
## Comparable & Comparator
* 기본적인 Java Object는 `Comparable interface`가 구현되어 있음
* `sort()` 메소드는 내부적으로 해당 클래스의 `compareTo()` 메소드 호출

### Comparable
* 기본 정렬기준을 구현
* Class에 `Comparable interface` 구현 후 `compareTo()` 메소드 오버라이딩

#### `compareTo()`
* 현재 object가 먼저면 `음수` 리턴
* 비교 object가 먼저면 `양수` 리턴
* 같은 순서면 `0` 리턴

```java
public class MyClass implements Comparable<MyClass> {

  public int num;
  public String str;
  
  public int compareTo(MyClass o){
    int result = this.num.compareTo(o.num);
    // int result = this.num - o.num;
    if (result == 0){
      result = this.str.compareTo(o.str);
    }
    return result;
  }
}
```

### Comparator
* 기존 `Comparable` 정의와 다른 기준으로 정렬하고자 할 때 사용
* `sort()`의 두번째 parameter로 `Comparator` 구현체를 전달

```java
Arrays.sort(arr, new Comparator<MyClass>() {
  @Override
  public int compare(MyClass o1, MyClass o2) {
    return o1.str.compareTo(o2.str);
  }
});
```
</details>

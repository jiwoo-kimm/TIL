# JAVA Collections
- A collection is an object that represents a **group of objects**
- A collections framework is a **unified architecture for representing and manipulating collections**, enabling collections to be manipulated independently of implementation details

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

<br>

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
- ordered using their natural ordering, or by a `comparator`
- O(log n) for the basic operations

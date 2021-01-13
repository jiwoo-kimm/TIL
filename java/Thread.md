# Thread

## Status

|Status|Explanation|
|--|--|
|NEW|thread 생성 후 start() 호출 전 상태|
|RUNNABLE|실행 중 or 실행 가능한 상태|
|BLOCKED|동기화블럭에 대해서 일시정지되어 lock이 풀릴 때까지 기다리는 상태|
|WAITING|작업이 종료되지는 않았지만 unrunnable 일시정지된 상태|
|TIMED_WAITING|정해진 시간만큼 unrunnable 일시정지된 상태|
|TERMINATED|작업이 종료된 상태|

## Implementation

||`implements Runnable`|`extends Thread`|
|--|--|--|
|`run()`|implement|override|
|instance|`Thread t = new MyThread();`|`Thread t = new Thread(new MyThread());`|
|Thread class method|객체에서 직접 호출|`static Thread currentThread()`를 통해 접근|

## Lock

### ReentrantLock
- 가장 일반적인 배타 lock
- 재진입이 가능한 lock

### ReentrantReadWriteLock
- 읽기에는 공유적이고 쓰기에는 배타적인 lock

### StampedLock
- ReentrantReadWriteLock에 낙관적 읽기 lock 추가
- 무조건 읽기 lock을 걸지 않고, 쓰기와 읽기가 충돌할 때만 쓰기가 끝난 후에 읽기 lock 걸음
- lock을 걸거나 해지할 때 `stamp`(long 타입의 정수값) 사용

### Condition
- thread 종류에 따라 wait & notify를 다르게 주기 위한 클래스
- `Condition c = lock.newCondition();`

|Object|Condition|
|--|--|
|wait()|await()<br>awaitUninterruptibly()|
|wait(long timeout)|await(long time, TimeUnit unit)<br>awaitNanos(long nanosTimeout)<br>awaitUnit(Date deadline)|
|notify()|signal()|
|notifyAll()|signalAll()|

## volatile
- 멀티 코어 프로세서에서 코어 간 변수 값 불일치를 해결하기 위한 키워드
- synchronized block과 같은 효과
- 캐시와 메모리 간 값 동기화
- 크기 4 byte 이상의 값을 원자화

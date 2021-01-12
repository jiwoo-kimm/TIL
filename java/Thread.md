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


**프로세스: 독립된 실행 프로그램의 단위**

**스레드: 프로세스 내의 하나의 실행 흐름**

**동기식/비동기식 프로그래밍**

**싱글 스레드/멀티 스레드**

스레드의 구현: Thread를 상속받거나 Runnable을 Override

thread의 "runnable" 상태를 override(<->"not runable")하고 sleep로 상태를 바꿈

스레드/프로세스의 생애주기: 생성(new)->실행(start)->소멸

join, yield, wait, notify 등으로 스레드의 순서를 조정할 수 있음

**critical section (locking이 필요한 구간)**

> 공유 객체를 사용하는 방식

```java
synchronized(shared_object){
    critical section
}
```

> 공유 함수를 사용하는 방식

```java
synchronized return_type function_name(dataType arguments){
    function
}
```

wait(), notify()


# Process 와 Thread

프로세스(Process)란 cpu에 의해 메모리에 올라가 실행중인 프로그램을 말한다.

자신만의 메모리 공간을 포함한 독립적인 실행공간을 갖고있다.

자바 JVM(Java Virtual Machine)은 주로 하나의 프로세스로 실행되며, 동시에 여러 작업을 수행하기 위헤 멀티 스레드를 지원한다.

Thread란 프로세스 안에서 실질적으로 작업을 실행하는 단위를 말한다.

Java에서는 JVM에 의해 관리가 된다.

한 프로그램에 여러개의 스레드가 존재 가능하며, 스레드가 1개이면 단일 스레드, 2개 이상이면 멀티 스레드 환경이 된다.

---

### Thread 특징
````
쓰레드는 각자 자신의 Stack 영역을 보유한다. ( 최소한 자신의 레지스터 상태를 보유한다 )
쓰레드는 프로세스 내에서 Code, Data, Heap 영역을 공유한다.
````

### Thread State
````
Thread.State NEW : 스레드가 실행 준비가 완료된 상태, 스레드의 첫 시작.
Thread.State RUNNABLE : 스레드가 실행 가능한 상태, 스레드가 대기열에서 실행을 기다리고 있음을 의미.
Thread.State BLOCKED : 스레드가 차단되어 있는 상태, 스레드가 잠금(lock) 습득을 기다리는 상태.
Thread.State WAITING : 스레드가 대기중인 상태, 대기 상태의 스레드는 다른 스레드가 작업을 완료하기를 기다리고 있는 상태이다.
Thread.State TIMED_WAITING : 스레드가 정해진 시간동안 대기하는 상태, WAITING과의 차이는 정해진 시간동안 대기를 한다는 것이다.
Thread.State TERMINATED : 스레드가 종료되거나 죽은 상태, 종료된 스레드는 실행이 완료되었음을 의미한다.
````
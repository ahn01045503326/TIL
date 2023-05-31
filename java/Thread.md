# Thread

---

### Thread 클래스 상속받아 thread 생성
- 실행 스레드로 자신의 콜 스택을 갖춘 독립적인 프로세스
- start() 메서드를 통해 스레드가 시작된다
> - Thread() 일반적인 스레드 객체 생성 -> Thread-n 이런 이름을 가진 스레드가 만들어진다
> - Thread(Runnable target) -> run 메서드를 가지는 객체를 인자값으로 할당하기
> - Thread(Runnable target, String name) -> run 메서드를 가지는 객체와 스레드 이름을 인자값으로 할당하기
> - Thread(String name) -> 스레드 생성하면서 스레드 이름 지어주기

````
public class Test01 extends Thread{
    @Override
    public void run() {
		/* 스레드 실행코드 */
    }
}
````


### Runnable 인터페이스 구현하여 thread 생성하기
- Runnable 인터페이스를 구현한다고 해서 바로 스레드가 되지 않는다
- Thread class 를 통해 스레드가 될 수 있다. (방법 : 객체 참조변수를 인자값으로 하는 Thread 생성)
````
public class Test01 implements Runnable {
    @Override
    public void run() {
		/* 스레드 실행코드 */
    }
}
````

외부 클래스로 스레드2개, 내부 클래스로 스레드 2개, 익명구현 객체로 1개생성

-> 총 5개의 스레드를 실행하는 코드
````
public class Test {
	//내부 클래스 - Thread 상속받기
    class ThirdThread extends Thread{
        @Override
        public void run() {
            System.out.println("3");
        }
    }

	//내부 클래스 - Runnable 구현
    class fourthThread implements Runnable{
        @Override
        public void run() {
            System.out.println("4");
        }
    }

//메인함수
    public static void main(String[] args) {
        Test t = new Test();        
        
        //스레드1
        FirstThread th1 = new FirstThread();
        th1.start();

        //스레드2
        SecondThread sec_thread = new SecondThread();
        Thread th2 = new Thread(sec_thread);
        th2.start();

        //스레드3
        ThirdThread th3 = t.new ThirdThread();
        th3.start();

        //스레드4
        Thread th4 = new Thread(t.new fourthThread());
        th4.start();
//        new Thread(t.new fourthThread()).start();

        /*
        스레드5 - 익명 객체구현객체 방식으로 생성
        	Thread 생성시 인자값으로 Runnable을 구현하는 코드 삽입하기
        */
        Thread th5 = new Thread(
                new Runnable() {
                    @Override
                    public void run() {
                        System.out.println("5");
                    }
                }
        );
        th5.start();
    }
}
````
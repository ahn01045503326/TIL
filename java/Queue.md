# Queue

![img.png](/image/img.png)
Queue는 자료구조의 스택과 반대의 구조라고 생각하면 된다.

큐는 FIFO(First In First Out)의 형태를 가지게 됩니다.

가장 먼저 들어온 데이터가 가장 먼저 나가는 구조를 말한다.

Enqueue : 큐 맨 뒤에 데이터를 추가

Dequeue : 큐 맨 앞쪽의 데이터를 삭제

---

### Queue클래스를 이용해서 구현
````
import java.util.LinkedList;
import java.util.Queue;

public class Main {

    public static void main(String[] args) {
        Queue<Integer> queue = new LinkedList<Integer>();

        queue.offer(1);
        queue.offer(2);
        queue.offer(3);
        queue.offer(4);
        queue.offer(5);

        while(!queue.isEmpty()) {
            System.out.println(queue.poll());
        }

    }

}
````

<br>

### 배열을 이용해서 Queue 구현

- queuelsEmpty() : 큐 안이 비었는지 판단하는 함수
- queueIsFull() : 배열의 최대크기를 벗어나면 안되기에 큐에 더이상 들어갈 공간이 없는지 판단하는 함수
- size() : queue에 현재 들어가 있는 데이터의 개수를 return하는 함수
- push(int value) : 큐 안에 데이터를 집어넣는 함수
- peek() : 큐 안의 데이터들중 가장 먼저 나오는 데이터를 return 하는 함수
- pop() : 큐 안의 데이터들 중 가장 먼저 나올수 있는 데이터를 return 하고 삭제하는 함수

````
public class ArrayQueue {
    int MAX = 1000;
    int front;    //머리 쪽에 위치할 index값, pop할때 참조하는 index
    int rear;    //꼬리 쪽에 위치할 index값, push할때 참조하는 index
    int [] queue;
    public ArrayQueue() {
        front = rear = 0;    //초기값 0
        queue = new int[MAX]; //배열 생성
    }

    public boolean queueisEmpty() { //queue에 아무것도 들어있지 않은지 판단하는 함수
        return front == rear;
    }
    public boolean queueisFull() {    //queue가 가득 차 공간이 없는지 판단하는 함수
        if(rear == MAX-1) {
            return true;
        }else 
            return false;
    }
    public int size() { //queue에 현재 들어가 있는 데이터의 개수를 return
        return front-rear;
    }
    public void push(int value) {
        if(queueisFull()) {
            System.out.println("Queue is Full");
            return;
        }
        queue[rear++] = value; //rear가 위치한 곳에 값을 넣어주고 rear를 증가시킨다.
    }
    public int pop() {
        if(queueisEmpty()) {
            System.out.println("Queue is Empty");
            return -1;
        }
        int popValue = queue[front++];
        return popValue;
    }
    public int peek() {
        if(queueisEmpty()) {
            System.out.println("Queue is Empty");
            return -1;
        }
        int popValue = queue[front];
        return popValue;
    }
}
````
배열로 구현한 Queue는 push pop이 간단하지만 배열의 크기가 유한해 큐의 크기가 다 차버리면 사용할수 없다. 

그러면 LinkedList로 Queue를 구현해야 한다.

<br>

### LinkedList을 이용해서 Queue 구현

````
public class QueueNode {
    int value; //값을 넣음
    QueueNode queueNode; //다음 노드를 가리킴
    public QueueNode(int value) {
        this.value = value;
        queueNode = null;
    }
    public int getValue() {
        return value;
    }
    public QueueNode getNextNode() {
        return queueNode;
    }
    public void setNextNode(QueueNode queueNode) {
        this.queueNode = queueNode;
    }
}

public class QueueNodeManager{ //큐의 기능을 만들 클래스
    QueueNode front,rear;
    public QueueNodeManager() {
        front = rear = null;
    }
    public boolean queueisEmpty() {
        if(front == null  && rear == null) {
            return true;
        }else {
            return false;
        }
    }
    public void push(int value) {
        QueueNode queueNode = new QueueNode(value);
        if(queueisEmpty()) {    //큐안에 데이터가 없으면 첫번째 Node에 front와 rear를 연결
            front = rear = queueNode;
        }else {
            front.setNextNode(queueNode); //큐 안에 데이터가 있으면 front를 다음 노드에 연결 후 front의 값을 마지막 노드로 삽입
            front = queueNode;
        }
    }
    public QueueNode pop() {
        if(queueisEmpty()) {
            System.out.println("Queue is Empty");
            return null;
        }else {
            QueueNode popNode = rear;
            rear = rear.getNextNode();
            return popNode;
        }
    }
    public QueueNode peek() {
        if(queueisEmpty()) {
            System.out.println("Queue is Empty");
            return null;
        }else {
            return rear;
        }
    }
    public int size() {
        QueueNode front2 = front;
        QueueNode rear2 = rear;
        int count = 0;
        while(front2 != rear2 && rear2 !=null) { //큐가 비어있는 경우가 있을수도 있을때도 생각해야함
            count++;
            rear2 = rear2.getNextNode();
        }
        return count;
    }
}
````
LinkedList로 Queue를 만들게 되면 규현은 복잡하지만 큐의 크기도 무한하고 Queue안에 원하는 기능을 넣을수도 있다는 장점이 있다.
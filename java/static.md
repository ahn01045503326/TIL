# static

static 키워드를 사용한 변수나 메소드는 클래스가 메모리에 올라갈 때 자동으로 생성되며 클래스 로딩이 끝나면 바로 사용할 수 있습니다. 

즉, 인스턴스(객체) 생성 없이 바로 사용 가능합니다.

모든 객체가 메모리를 공유한다는 특징이 있고, GC 관리 영역 밖에 있기 때문에 프로그램이 종료될 때까지 메모리에 값이 유지된 채로 존재하게 됩니다.

````
[static을 사용하는 이유]
- static은 자주 변하지 않는 값이나 공통으로 사용되는 값 같은 공용자원에 대한 접근에 있어서 매번 메모리에 로딩하거나 값을 읽어들이는 것보다 일종의 '전역변수'와 같은 개념을 통해 접근하는 것이 비용도 줄이고 효율을 높일 수 있습니다.
- 인스턴스 생성 없이 바로 사용 가능하기 때문에 프로그램 내에서 공통으로 사용되는 데이터들을 관리할 때 이용합니다.
````

---

### static 변수

예를들어 게시물의 좋아요를 누를때마다 좋아요 값을 증가시키는 LikeCount 기능을 구현한다는 가정을 해보자.
````
package study;

public class LikeCount {

    int count;
    //static int count;
 
    public LikeCount() {
        this.count++;
        System.out.println("좋아요 개수 : " + count);
    }
 
    public static void main(String[] args) {
        LikeCount lc1 = new LikeCount();
        LikeCount lc2 = new LikeCount();
 
    }
}
````
위의 예제를 먼저 보면, lc1, lc2 객체가 생성될 때 lc1의 count와 lc2의 count가 서로 다른 메모리를 할당 받게된다.
````
좋아요 개수 : 1
좋아요 개수 : 1

Process finished with exit code 0
````

그러나 아래와 같이 static변수를 사용하면 두 객체가 생성될 때 lc1, lc2 객체는 하나의 메모리를 공유하게 되는 것이다.

````
public class LikeCount {

//    int count;
static int count;

    public LikeCount() {
        this.count++;
        System.out.println("좋아요 개수 : " + count);
    }
 
    public static void main(String[] args) {
        LikeCount lc1 = new LikeCount();
        LikeCount lc2 = new LikeCount();
 
    }
}
````

````
좋아요 개수 : 1
좋아요 개수 : 2

Process finished with exit code 0
````

### static 메소드
static메소드는 객체의 생성 없이 호출이 가능하고, 객체에서는 호출이 불가능하다.또한 static메소드 안에서는 인스턴스 변수 접근이 불가능 하다.

![static메소드1.png](/image/static메소드1.png)

위와 같이 static메소드 안에선 인스턴스 변수는 접근이 불가능하다.

![static메소드2.png](/image/static메소드2.png)

static메소드 안에선 static변수만 접근이 가능한 것을 볼 수 있다.

### 결론
- 인스턴스에 공통적으로 사용해야하는 것에 static을 붙인다. 
  - 인스턴스를 생성하면, 각 인스턴스들은 서로 다른 독립적인 메모리를 할당받기 때문에 서로 다른 값을 유지한다.
  - 경우에 따라 인스턴스들이 공통적인 값이 유지되어야 하는 경우에는 static을 붙인다.

- static이 붙은 멤버변수는 인스턴스를 생성하지 않아도 사용할 수 있다.
  - static이 붙은 멤버변수(클래스변수)는 클래스가 메모리에 올라갈 때 이미 자동적으로 생성되기 때문이다.

- static이 붙은 메소드(함수)에선 인스턴스 변수를 사용할 수 없다.
  - static메소드는 인스턴스 생성 없이 호출 가능한 반면, 인스턴스 변수는 인스턴스를 생성해야만 존재하기 때문에 static이 붙은 메소드를 호출할 때 인스턴스가 생성되어 있을 수도 아닐 수도 있기 때문에 static이 붙은 메소드에서 인스턴스 변수의 사용을 허용하지 않는다.
  - 반대로, 인스턴스변수·메소드에선 static이 붙은 멤버들을 사용하는 것은 가능(인스턴스변수가 존재한다는 것은 static 멤버들은 이미 메모리에 존재한다는 것을 의미하기 때문)

- 메소드 내에서 인스턴스 변수를 사용하지 않는다면, static을 붙이는 것을 고려한다.
  - 메소드 호출시간이 짧아지기 때문에 효율이 높아진다.

- 클래스 설계시 static의 사용지침
  - 클래스의 멤버변수중 모든 인스턴스에 공통된 값을 유지해야하는 것이 있는지 보고 있다면 static을 붙여준다.
  - 작성한 메소드 중 인스턴스 변수를 사용하지 않는 메소드에 대해서 static을 붙일 것을 고려한다.


일반적으로 인스턴스변수와 관련된 작업을 하는 메소드는 인스턴스메소드 (static X)이고,

static변수(클래스변수)와 관련된 작업을 하는 메소드는 클래스메소드 (static O)이다.
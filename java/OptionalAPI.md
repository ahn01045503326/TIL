# Optional API

개발할때 가장 많이 발생하는 예외 중 하나가 NPE(NullPointerException)입니다.

NPE를 피하려면 null 여부 검사를 필연적으로 하게 되는데 만약 null 검사를 해야하는 변수가 많은 경우 코드가 복잡해지고 번거롭습니다. 

하지만 Java8 부터 Optional<T>을 제공하여 null로 인한 예외가 발생하지 않도록 도와주고, Optional 클래스의 메소드를 통해 null을 컨트롤 할 수 있습니다.
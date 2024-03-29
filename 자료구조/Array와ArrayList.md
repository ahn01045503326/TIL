# Array와 ArrayList의 차이점

Array는 크기가 고정적이고, ArrayList는 크기가 가변적입니다.

Array는 초기화 시 메모리에 할당되어 ArrayList보다 속도가 빠르고,

ArrayList는 데이터 추가 및 삭제 시 메모리를 재할당하기 때문에 속도가 Array보다 느립니다.

---

### Array와 LinkedList의 장/단점

Array는 인덱스(index)로 해당 원소(element)에 접근할 수 있어 찾고자 하는 원소의 인덱스 값을 알고 있으면 O(1)에 해당 원소로 접근할 수 있습니다. 즉, RandomAccess가 가능해 속도가 빠르다는 장점이 있습니다.

하지만 삽입 또는 삭제의 과정에서 각 원소들을 shift 해줘야 하는 비용이 생겨 이 경우 시간 복잡도는 O(n)이 된다는 단점이 있습니다.

이 문제점을 해결하기 위한 자료구조가 linkedlist입니다. 각각의 원소들은 자기 자신 다음에 어떤 원소인지만을 기억하고 있기 때문에 이 부분만 다른 값으로 바꿔주면 삽입과 삭제를 O(1)로 해결할 수 있습니다.

하지만LinkedList는 원하는 위치에 한 번에 접근할 수 없다는 단점이 있습니다. 원하는 위치에 삽입을 하고자 하면 원하는 위치를 Search 과정에 있어서 첫번째 원소부터 다 확인해봐야 합니다.

### 정리
````
- Array는 검색이 빠르지만, 삽입, 삭제가 느리다.
- LinkedList는 삽입, 삭제가 빠르지만, 검색이 느리다.
````
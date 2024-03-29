# Index에 대해 설명해주시고, 장/단점

Index란 테이블을 처음부터 끝까지 검색하는 방법인 FTS(Full Table Scan)과는 달리 인덱스를 검색하여 해당 자료의 테이블을 엑세스 하는 방법입니다.

- 예를들어, DB를 책으로 비유하면 데이터는 책의 내용일 것이고, 데이터가 저장된 레코드의 주소는 index 목록에 있는 페이지 번호일 것이다.

인덱스는 항상 정렬된 상태를 유지하기 때문에 원하는 값을 검색하는데 빠르지만, 새로운 값을 추가하거나 삭제, 수정하는 경우에는 쿼리문 실행 속도가 느려집니다.

즉, 인덱스는 데이터의 저장 성능을 희생하고 그대신 데이터의 검색 속도를 높이는 기능이라 할 수 있습니다.

## DBMS는 Index를 어떻게 관리하고 있나요? (Index 자료구조)
````
B+Tree 인덱스 자료구조
- 자식 노드가 2개 이상인 B-Tree를 개선시킨 자료구조이며,
- BTree 리프노드들을 LinkedList로 연결하여 순차 검색을 용이하게 합니다. 해시 테이블보다 나쁜 O(log2N)의 시간복잡도를 갖지만 일반적으로 사용되는 자료구조입니다.

해시 테이블
- 컬럼의 값으로 생성된 해시를 기반으로 인덱스를 구현합니다.
- 시간복잡도가 O(1)이라 검색이 매우 빠릅니다.
- 부등호(<,>)와 같은 연속적인 데이터를 위한 순차 검색이 불가능하기 때문에 사용에 적합하지 않습니다.
````
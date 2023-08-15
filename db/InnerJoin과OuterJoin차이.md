# inner join과 outer join의 차이

### inner join

서로 연관된 내용만 검색하는 조인 방법입니다.

A와 B에 대해 수행하는 것은, A와 B의 교집합을 말합니다. 벤다이어그램으로 그렸을 때 교차되는 부분입니다.

### outer join

한 쪽에는 데이터가 있고 한 쪽에는 데이터가 없는 경우, 데이터가 있는 쪽의 내용을 전부 출력하는 방법입니다.

A와 B에 대해 수행하는 것은, A와 B의 합집합을 말합니다. 벤다이어그램으로 그렸을 때 합집합 부분입니다.

outer join에는 LEFT OUTER JOIN, RIGHT OUTER JOIN, FULL OUTER JOIN이 있습니다.

![join](join.jpeg)
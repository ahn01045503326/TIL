# WHERE IN 구문
- 특정 열(column)에서 원하는 값을 가진 행(row)을 검색하는데 사용되는 SQL 구문
- WHERE IN 절은 WHERE 절과 유사하지만 다른 점은 특정 열에서 값의 집합을 찾아내는 것

---
#### 예를 들어, customers 테이블에서 customer_id 열(column)이 1, 2, 3인 고객 정보를 검색하는 SQL 구문은 다음과 같이 작성할 수 있습니다.
````
SELECT *
FROM customers
WHERE customer_id IN (1, 2, 3);
````
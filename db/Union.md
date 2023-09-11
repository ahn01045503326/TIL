# Union

두 개 이상의 쿼리를 합쳐 하나의 쿼리로 만들어 주는 역할을 한다.

이 때 각 컬럼명은 같아야하며 데이터타입 역시 동일해야한다.

만일 컬럼명이 다른 경우엔 AS를 사용해 컬럼명을 통일시켜주어야 한다.

````
SELECT EXAMPLE_1 FROM EX_TABLE1
UNION
SELECT EXAMPLE_2 AS EXAMPLE_1 FROM EX_TABLE2
````

----

#### Union VS Union All
````
우선 기본적으로 Union은 Union Distinct를 줄여서 쓰는 개념이다. 즉, 중복을 허락하지 않는다.
예를 들어 EX_TABLE1 에서 select 한 값이 'test1', 'test2' 이고 EX_TABLE2에서 select 한 값이 'test1', 'test3'이라고 가정해보자.
이때 union을 써서 두 sql을 합쳐주면 결과는 'test1', 'test2', 'test3'으로 중복을 제거한 결과값을 돌려준다.
하지만 Union all을 사용해 두 sql을 합친다면 결과는 'test1', 'test2', 'test1', 'test3'가 될 것이다.
아무래도 Union의 경우 중복을 제거하는 작업을 시행해주기 때문에 Union all에 비해 처리 속도가 느리다.
그렇기 때문에 중복되어도 크게 이상이 없는 경우에는 되도록 Union all을 사용해주는 것이 좋다.
````
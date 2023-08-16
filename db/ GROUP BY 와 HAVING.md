
### GROUP BY

GROUP BY 는 GROUP BY 명령어를 통해 특정 컬럼을 기준으로 연산한 결과를 집계 키로 정의하여 그룹을 짓는 역할을 합니다.

집합 연산자는 COUNT, SUM, AVG, MAX, MIN 등이 있고, DISTINCT와 같이 중복 데이터를 제거하는 특징이 있습니다.

### HAVING

GROUP BY 절에서 조건을 주려면 WHERE이 아닌, HAVING 절을 사용해야 합니다.

위의 SELECT 실행 순서를 보면 WHERE 절이 GROUP BY 보다 먼저 실행되기 때문에, GROUP BY에 대응되는 HAVING절이 있습니다.

HAVING 은 GROUP BY 뒤에 작성하며, WHERE와 동일한 형식으로 조건을 작성할 수 있습니다.아래는 name 컬럼을 기준으로 그룹화 하는데, 그룹화한 항목의 개수가 1인 데이터들만 조회하는 예제입니다.
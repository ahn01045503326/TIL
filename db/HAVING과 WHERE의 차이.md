# HAVING과 WHERE의 차이

having은 그룹을 필터링 하는데 사용되고, where은 개별 행을 필터링하는데 사용됩니다.

집계 함수(COUNT, SUM, AVG, MAX, MIN 등)는 having절과 함께 사용할 수 있으나,
where절은 사용할 수 없습니다.( 집계함수를 사용할 수 있는 GROUP BY 절보다 WHERE절이 먼저 수행)

having은 그룹화 또는 집계가 발생한 후 필터링하는데 사용되고,
where은 그룹화 또는 집계가 발생하기 전에 필터링하는데 사용됩니다.
# JOIN에서 ON과 WHERE의 차이

ON 이 WHERE 보다 먼저 실행되어 JOIN 을 하기 전에 필터링을 하고 (=ON 조건으로 필터링이 된 레코들간 JOIN이 이뤄진다)

WHERE은 JOIN 을 한 후에 필터링을 합니다. (=JOIN을 한 결과에서 WHERE 조건절로 필터링이 이뤄진다)
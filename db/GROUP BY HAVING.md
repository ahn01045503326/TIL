# WHERE IN 구문
- 중복된 레코드를 출력하려면 GROUP BY와 HAVING을 사용할 수 있습니다. 
- 중복된 레코드를 출력하는 쿼리

---

````
SELECT name, COUNT(*) as count
FROM employees
GROUP BY name
HAVING COUNT(*) > 1;
````
위 쿼리는 table_name에서 column_name이 중복되는 레코드를 찾아 해당 column_name과 중복된 횟수를 출력합니다. GROUP BY 구문으로 column_name을 그룹화하고, HAVING 구문으로 그룹 중에서 COUNT(*)이 1보다 큰 그룹만 출력하도록 조건을 설정합니다.

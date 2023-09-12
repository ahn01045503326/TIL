# 셀프 조인(SELF JOIN)

셀프 조인이란, 동일 데이블 사이의 조인을 말한다.

FROM 절에 동일 테이블이 두 번 이상 나타난다.

같은 테이블끼리 조인하는 것이므로 별칭(ALIAS)을 꼭 사용해야 한다.
````
SELECT   A.EMPNO 사원번호, A.ENAME 사원명, B.ENAME 관리자명
FROM     EMP A, EMP B
WHERE    A.MGR = B.EMPNO
````

---

### 사용 예

사원이라는 테이블에는 사원과 관리자가 모두 하나의 사원 개념으로 동일시하여 같이 입력되어 있다.

셀프조인을 이용해서 "자신과 상위, 차상위 관리자를 같은 줄에 표시하라"는 문제를 셀프 조인을 이용해서 풀 수 있다.

![셀프조인.png](/image/셀프조인.png)

````
SELECT    E1.ENAME 사원, E1.MGR 관리자, E2.MGR 차상위_관리자
FROM      EMP E1, EMP E2
WHERE     E1.MGR = E2.EMPNO
ORDER BY  E2.MGR DESC, E1.MGR, E1.EMPNO
````
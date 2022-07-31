# SQL 기초(3)

IF문을 SQL로 구현하기 1️⃣ (DECODE) 

`SELECT ename, deptno, *DECODE*(deptno, 10, 300, 20, 400, 0) as 보너스 FROM emp;`

*DECODE*(deptno, 10, 300, 20, 400, 0) 

: 부서 번호가 10이면 300을 20이면 400을 나머지 부서 번호는 0을 출력

| IF문 | 설명 |
| --- | --- |
| IF DEPTNO = 10 THEN 300 | 부서 번호가 10번이면 300 출력 |
| ELSE IF DEPTNO = 20 THEN 400 | 그렇지 않고 부서 번호가 20이면 400 출력 |
| ELSE 0 | 위의 조건에 다 해당되지 않는다면 0 출력 |

IF문을 SQL로 구현하기 2️⃣ (CASE)

```sql
SELECT ename, job, sal, CASE WHEN sal >= 3000 THEN 500
                            WHEN sal >= 2000 THEN 300
                            WHEN sal >= 1000 THEN 200
                            ELSE 0 END AS BONUS
FROM emp WHERE job IN ('SALESMAN', 'ANALYST');
```

**CASE문과 DECODE와 다른 점**

**DECODE는 등호(=)만 가능, CASE는 등호(=)와 부등호(> =, < =, >, <)  둘 다 가능**

최댓값 출력하기(MAX)

`SELECT *MAX*(sal) FROM emp;`

`SELECT deptno, *MAX*(sal) FROM emp GROUP BY deptno;`

최소값 출력하기(MIN)

`SELECT *MIN*(sal) FROM emp WHERE job = 'SALESMAN';`

평균값 출력하기(AVG)

`SELECT *AVG*(comm) FROM emp;`

|  | NVL 함수 사용하지 않았을 때 | NVL 함수 사용했을 때 |
| --- | --- | --- |
| SQL | SELECT SUM(comm) FROM emp; | SELECT SUM(NVL(comm, 0)) FROM emp; |
| 결과 | 2200 | 2200 |

NVL 함수를 사용하면 NULL을 0으로 변경하면 SUM 합계를 수행할 때 포함되므로 시간이 더 걸린다.

토탈값 출력하기(SUM)

`SELECT deptno, *SUM*(sal) FROM emp GROUP BY deptno;`

- 그룹 함수로 조건을 줄 때는 WHERE절 대신 HAVING절을 사용해야 한다.
- GROUP BY 절에 컬럼 별칭을 사용하면 에러 발생

건수 출력하기(COUNT) 

`SELECT *COUNT*(empno) FROM emp;`

데이터 분석 함수로 순위 출력하기 (RANK)

```sql
SELECT ename, job, sal,RANK() over (ORDER BY sal DESC) 순위 FROM emp
WHERE job in ('ANALUST', 'MANAGER');
```

데이터 분석 함수로 순위 출력하기(DENSE_RANK)

```sql
SELECT ename, job, sal,RANK() over (ORDER BY sal DESC) AS RANK,
DENSE_RANK() over (ORDER BY sal DESC) AS DENSE_RANK FROM EMP
WHERE job in ('ANALYST', 'MANAGER');
```

RANK : 동일한 값이면 중복 순위를 부여하고, 다음 순위는 해당 개수만큼 건너뛰고 반환한다.

DENSE_RANK : 동일한 값이면 중복 순위를 부여하고, 다음 순위는 중복 순위와 상관없이 순차적으로 반환한다.

ROW_NUMBER : 중복 관계없이 순차적으로 순위를 반환한다.

데이터 분석 함수로 등급 출력하기(NTILE)

```sql
SELECT ename, job, sal,NTILE(4) over (order by sal desc nulls last) 등급 FROM EMP
WHERE job in ('ANALYST', 'MANAGER', 'CLERK');
```

데이터 분석 함수로 순위의 비율 출력하기(CUME_DIST)

```sql
SELECT ename, sal,RANK() over (order by sal desc) as RANK,
DENSE_RANK() over (order by sal desc) as DENSE_RANK,
CUME_DIST() over (order by sal desc) as CUM_DIST
FROM emp;
```

데이터 분석 함수로 데이터를 가로로 출력하기(LISTAGG)

`SELECT deptno, *LISTAGG*(ename, ',') within group (order by ename) as EMPLOYEE FROM emp GROUP BY deptno;`

LISTAGG 함수 : 데이터를 가로로 출력해주는 함수 

LISTAGG에 구분자로 콤마(,)를 설정함 (/)도 가능 

WITHIN GROUP :  ‘~이내의’ - group 다음에 나오는 괄호에 속한 그룹의 데이터를 출력하겠다!

GROUP BY절은 LISTAGG 함수를 사용하려면 필수!

`SELECT job, *LISTAGG*(ename||'('||sal||')', ',') within group (order by ename asc) as employee FROM emp GROUP BY job;`